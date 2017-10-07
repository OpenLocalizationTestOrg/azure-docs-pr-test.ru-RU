---
title: "Учебник. Интеграция Azure Active Directory с Hightail | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="a456e-103">Учебник. Интеграция Azure Active Directory с Hightail</span><span class="sxs-lookup"><span data-stu-id="a456e-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="a456e-104">В этом учебнике вы узнаете, как toointegrate Hightail с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a456e-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a456e-105">Интеграция с Azure AD Hightail предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a456e-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a456e-106">Можно управлять в Azure AD, имеющего доступ tooHightail</span><span class="sxs-lookup"><span data-stu-id="a456e-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="a456e-107">Можно включить на пользователей tooautomatically get вошедшего tooHightail (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a456e-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a456e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a456e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a456e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a456e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a456e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a456e-110">Prerequisites</span></span>

<span data-ttu-id="a456e-111">tooconfigure интеграция Azure AD с Hightail требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a456e-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="a456e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a456e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a456e-113">подписка Hightail с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a456e-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a456e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a456e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a456e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a456e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a456e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a456e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a456e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a456e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a456e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a456e-118">Scenario description</span></span>
<span data-ttu-id="a456e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a456e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a456e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a456e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a456e-121">Добавление Hightail из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a456e-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="a456e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a456e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="a456e-123">Добавление Hightail из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a456e-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="a456e-124">tooconfigure hello интеграции Hightail в Azure AD, вы должны tooadd Hightail из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a456e-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a456e-125">**tooadd Hightail из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a456e-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a456e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a456e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a456e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a456e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a456e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a456e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a456e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a456e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a456e-133">Введите в поле поиска hello **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="a456e-133">In hello search box, type **Hightail**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="a456e-135">В панели результатов hello выберите **Hightail**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a456e-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a456e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a456e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a456e-138">В этом разделе описана настройка и проверка единого входа Azure AD в Hightail с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a456e-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a456e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Hightail является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a456e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="a456e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Hightail должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a456e-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="a456e-141">В Hightail, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a456e-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a456e-142">tooconfigure и теста Azure AD единого входа с Hightail, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a456e-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a456e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a456e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a456e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a456e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a456e-145">**[Создание тестового пользователя Hightail](#creating-a-hightail-test-user)**  -toohave аналог Саймон Britta в Hightail, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a456e-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a456e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a456e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a456e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a456e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a456e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a456e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a456e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Hightail.</span><span class="sxs-lookup"><span data-stu-id="a456e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="a456e-150">**tooconfigure Azure AD единого входа с Hightail, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a456e-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="a456e-151">В hello в hello портала Azure **Hightail** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a456e-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a456e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a456e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="a456e-155">На hello **Hightail доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a456e-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="a456e-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес hello как:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="a456e-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a456e-158">Hello выше значение не является действительным значением.</span><span class="sxs-lookup"><span data-stu-id="a456e-158">hello preceding value is not real value.</span></span> <span data-ttu-id="a456e-159">Значение hello будет обновляться hello фактический URL-адрес ответа, который описывается далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="a456e-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="a456e-160">На hello **URL-адреса и домена Hightail** статьи, при желании tooconfigure приложения hello в **режим, инициируемая SP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a456e-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="a456e-162">а.</span><span class="sxs-lookup"><span data-stu-id="a456e-162">a.</span></span> <span data-ttu-id="a456e-163">Нажмите кнопку hello **Показывать дополнительные параметры URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="a456e-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="a456e-164">b.</span><span class="sxs-lookup"><span data-stu-id="a456e-164">b.</span></span> <span data-ttu-id="a456e-165">В hello **на URL-адрес входа** текстовом поле введите URL-адрес hello как:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="a456e-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="a456e-166">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a456e-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="a456e-168">Hightail приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="a456e-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a456e-169">Выполните настройку следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a456e-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="a456e-170">Вы можете управлять hello значения этих атрибутов из hello **«Атрибутов»** вкладку приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a456e-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="a456e-171">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="a456e-171">hello following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="a456e-173">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a456e-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="a456e-174">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="a456e-174">Attribute Name</span></span> | <span data-ttu-id="a456e-175">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="a456e-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="a456e-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="a456e-176">FirstName</span></span> | <span data-ttu-id="a456e-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a456e-177">user.givenname</span></span> |
    | <span data-ttu-id="a456e-178">LastName</span><span class="sxs-lookup"><span data-stu-id="a456e-178">LastName</span></span> | <span data-ttu-id="a456e-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="a456e-179">user.surname</span></span> |
    | <span data-ttu-id="a456e-180">Email</span><span class="sxs-lookup"><span data-stu-id="a456e-180">Email</span></span> | <span data-ttu-id="a456e-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="a456e-181">user.mail</span></span> |    
    | <span data-ttu-id="a456e-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="a456e-182">UserIdentity</span></span> | <span data-ttu-id="a456e-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="a456e-183">user.mail</span></span> |
    
    <span data-ttu-id="a456e-184">а.</span><span class="sxs-lookup"><span data-stu-id="a456e-184">a.</span></span> <span data-ttu-id="a456e-185">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a456e-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="a456e-188">b.</span><span class="sxs-lookup"><span data-stu-id="a456e-188">b.</span></span> <span data-ttu-id="a456e-189">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="a456e-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="a456e-190">c.</span><span class="sxs-lookup"><span data-stu-id="a456e-190">c.</span></span> <span data-ttu-id="a456e-191">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="a456e-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="a456e-192">d.</span><span class="sxs-lookup"><span data-stu-id="a456e-192">d.</span></span> <span data-ttu-id="a456e-193">Оставьте hello **имен** пустым.</span><span class="sxs-lookup"><span data-stu-id="a456e-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="a456e-194">д.</span><span class="sxs-lookup"><span data-stu-id="a456e-194">e.</span></span> <span data-ttu-id="a456e-195">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a456e-195">Click **Ok**.</span></span>

7. <span data-ttu-id="a456e-196">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a456e-196">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a456e-198">На hello **Hightail конфигурации** щелкните **Настройка Hightail** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a456e-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a456e-199">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a456e-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="a456e-201">Перед настройкой hello единого входа в приложение Hightail, проверьте список разрешенных доменом электронной почты с Hightail команды, чтобы все пользователи, использующие этот домен Здравствуйте, можно воспользоваться единого входа.</span><span class="sxs-lookup"><span data-stu-id="a456e-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="a456e-202">tooget единого входа, настроенному для вашего приложения, необходимо клиента Hightail tooyour toosign вход в систему с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a456e-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="a456e-203">а.</span><span class="sxs-lookup"><span data-stu-id="a456e-203">a.</span></span> <span data-ttu-id="a456e-204">В меню в верхней части hello hello щелкните hello **учетной записи** и выберите **Настройка SAML**.</span><span class="sxs-lookup"><span data-stu-id="a456e-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="a456e-206">b.</span><span class="sxs-lookup"><span data-stu-id="a456e-206">b.</span></span> <span data-ttu-id="a456e-207">Установка флажка hello **включить проверку подлинности SAML**.</span><span class="sxs-lookup"><span data-stu-id="a456e-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="a456e-209">c.</span><span class="sxs-lookup"><span data-stu-id="a456e-209">c.</span></span> <span data-ttu-id="a456e-210">Откройте сертификат в кодировке base-64 в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **SAML сертификат подписи маркера** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a456e-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="a456e-212">d.</span><span class="sxs-lookup"><span data-stu-id="a456e-212">d.</span></span> <span data-ttu-id="a456e-213">В hello **SAML центра (поставщика удостоверений)** текстовое значение hello вставить **SAML единого входа URL-адрес службы** копируется из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a456e-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="a456e-215">д.</span><span class="sxs-lookup"><span data-stu-id="a456e-215">e.</span></span> <span data-ttu-id="a456e-216">При необходимости приложение hello tooconfigure в **режим, инициированный IDP** выберите **«Поставщика удостоверений (IdP) инициировал вход»**.</span><span class="sxs-lookup"><span data-stu-id="a456e-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="a456e-217">Чтобы настроить приложение в **режиме, инициированном поставщиком услуг**, выберите **Service Provider (SP) initiated log in** (Вход, инициированный поставщиком услуг (SP)).</span><span class="sxs-lookup"><span data-stu-id="a456e-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="a456e-219">f.</span><span class="sxs-lookup"><span data-stu-id="a456e-219">f.</span></span> <span data-ttu-id="a456e-220">Скопируйте URL-адрес потребителя SAML hello для экземпляра и вставьте его в **URL-адрес ответа** текстовое поле в **Hightail доменов и URL-адреса** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a456e-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="a456e-221">ж.</span><span class="sxs-lookup"><span data-stu-id="a456e-221">g.</span></span> <span data-ttu-id="a456e-222">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a456e-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a456e-223">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a456e-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a456e-224">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a456e-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a456e-225">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a456e-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a456e-226">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a456e-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="a456e-227">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a456e-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a456e-229">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a456e-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a456e-230">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a456e-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a456e-232">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a456e-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a456e-234">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a456e-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a456e-236">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a456e-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a456e-238">а.</span><span class="sxs-lookup"><span data-stu-id="a456e-238">a.</span></span> <span data-ttu-id="a456e-239">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a456e-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a456e-240">b.</span><span class="sxs-lookup"><span data-stu-id="a456e-240">b.</span></span> <span data-ttu-id="a456e-241">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a456e-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a456e-242">c.</span><span class="sxs-lookup"><span data-stu-id="a456e-242">c.</span></span> <span data-ttu-id="a456e-243">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a456e-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a456e-244">d.</span><span class="sxs-lookup"><span data-stu-id="a456e-244">d.</span></span> <span data-ttu-id="a456e-245">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a456e-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="a456e-246">Создание тестового пользователя Hightail</span><span class="sxs-lookup"><span data-stu-id="a456e-246">Creating a Hightail test user</span></span>

<span data-ttu-id="a456e-247">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Hightail.</span><span class="sxs-lookup"><span data-stu-id="a456e-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="a456e-248">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="a456e-248">There is no action item for you in this section.</span></span> <span data-ttu-id="a456e-249">Hightail поддерживает подготовку пользователей just-in-time на основании пользовательских утверждений hello.</span><span class="sxs-lookup"><span data-stu-id="a456e-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="a456e-250">Если вы настроили hello настраиваемые утверждения, как показано в разделе "hello"  **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  выше пользователя автоматически создается в приложения hello, он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="a456e-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="a456e-251">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Hightail поддержки](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="a456e-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a456e-252">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a456e-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a456e-253">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHightail доступа.</span><span class="sxs-lookup"><span data-stu-id="a456e-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a456e-255">**tooassign tooHightail Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a456e-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="a456e-256">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a456e-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a456e-258">В списке приложений hello выберите **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="a456e-258">In hello applications list, select **Hightail**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="a456e-260">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a456e-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a456e-262">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a456e-262">Click **Add** button.</span></span> <span data-ttu-id="a456e-263">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a456e-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a456e-265">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a456e-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a456e-266">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a456e-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a456e-267">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a456e-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a456e-268">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a456e-268">Testing single sign-on</span></span>

<span data-ttu-id="a456e-269">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="a456e-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a456e-270">При нажатии кнопки hello Hightail плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Hightail приложения.</span><span class="sxs-lookup"><span data-stu-id="a456e-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a456e-271">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a456e-271">Additional resources</span></span>

* [<span data-ttu-id="a456e-272">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a456e-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a456e-273">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a456e-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

