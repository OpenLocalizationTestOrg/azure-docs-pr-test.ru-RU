---
title: "Руководство по интеграции Azure Active Directory с 123ContactForm | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="ea413-103">Руководство по интеграции Azure Active Directory с 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="ea413-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="ea413-104">В этом учебнике вы узнаете, как 123ContactForm toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea413-104">In this tutorial, you learn how toointegrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea413-105">Интеграция с Azure AD 123ContactForm предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ea413-105">Integrating 123ContactForm with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ea413-106">Можно управлять в Azure AD, имеющего доступ too123ContactForm</span><span class="sxs-lookup"><span data-stu-id="ea413-106">You can control in Azure AD who has access too123ContactForm</span></span>
- <span data-ttu-id="ea413-107">Можно включить на пользователей tooautomatically get вошедшего too123ContactForm (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea413-107">You can enable your users tooautomatically get signed-on too123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea413-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ea413-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ea413-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea413-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea413-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea413-110">Prerequisites</span></span>

<span data-ttu-id="ea413-111">tooconfigure интеграция Azure AD с 123ContactForm требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ea413-111">tooconfigure Azure AD integration with 123ContactForm, you need hello following items:</span></span>

- <span data-ttu-id="ea413-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ea413-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea413-113">подписка 123ContactForm с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ea413-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea413-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ea413-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea413-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ea413-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea413-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ea413-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea413-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea413-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea413-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ea413-118">Scenario description</span></span>
<span data-ttu-id="ea413-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ea413-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea413-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ea413-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea413-121">Добавление 123ContactForm из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ea413-121">Adding 123ContactForm from hello gallery</span></span>
2. <span data-ttu-id="ea413-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea413-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-hello-gallery"></a><span data-ttu-id="ea413-123">Добавление 123ContactForm из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ea413-123">Adding 123ContactForm from hello gallery</span></span>
<span data-ttu-id="ea413-124">tooconfigure hello интеграции 123ContactForm в Azure AD, вы должны 123ContactForm tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ea413-124">tooconfigure hello integration of 123ContactForm into Azure AD, you need tooadd 123ContactForm from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ea413-125">**123ContactForm tooadd из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea413-125">**tooadd 123ContactForm from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea413-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ea413-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea413-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ea413-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ea413-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea413-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ea413-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ea413-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ea413-133">Введите в поле поиска hello **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="ea413-133">In hello search box, type **123ContactForm**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="ea413-135">В панели результатов hello выберите **123ContactForm**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ea413-135">In hello results panel, select **123ContactForm**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea413-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea413-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea413-138">В этом разделе описана настройка и проверка единого входа Azure AD в 123ContactForm с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea413-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ea413-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в 123ContactForm является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea413-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 123ContactForm is tooa user in Azure AD.</span></span> <span data-ttu-id="ea413-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в 123ContactForm должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ea413-140">In other words, a link relationship between an Azure AD user and hello related user in 123ContactForm needs toobe established.</span></span>

<span data-ttu-id="ea413-141">В 123ContactForm, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ea413-141">In 123ContactForm, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ea413-142">tooconfigure и теста Azure AD единого входа с 123ContactForm, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ea413-142">tooconfigure and test Azure AD single sign-on with 123ContactForm, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ea413-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ea413-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ea413-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ea413-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea413-145">**[Создание тестового пользователя 123ContactForm](#creating-a-123contactform-test-user)**  -toohave аналог Саймон Britta в 123ContactForm, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ea413-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - toohave a counterpart of Britta Simon in 123ContactForm that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea413-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ea413-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea413-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ea413-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea413-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea413-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea413-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="ea413-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="ea413-150">**tooconfigure Azure AD единого входа с 123ContactForm, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea413-150">**tooconfigure Azure AD single sign-on with 123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea413-151">В hello в hello портала Azure **123ContactForm** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ea413-151">In hello Azure portal, on hello **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ea413-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ea413-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="ea413-155">На hello **123ContactForm URL-адреса и домена** статьи, при желании tooconfigure приложения hello в **режиме, инициированный IDP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea413-155">On hello **123ContactForm Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="ea413-157">а.</span><span class="sxs-lookup"><span data-stu-id="ea413-157">a.</span></span> <span data-ttu-id="ea413-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="ea413-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="ea413-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea413-159">b.</span></span> <span data-ttu-id="ea413-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="ea413-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="ea413-161">При необходимости приложение hello tooconfigure в **режиме, инициируемая SP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea413-161">If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="ea413-163">а.</span><span class="sxs-lookup"><span data-stu-id="ea413-163">a.</span></span> <span data-ttu-id="ea413-164">Нажмите кнопку hello **Показывать дополнительные параметры URL-адреса** параметр</span><span class="sxs-lookup"><span data-stu-id="ea413-164">Click hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="ea413-165">b.</span><span class="sxs-lookup"><span data-stu-id="ea413-165">b.</span></span> <span data-ttu-id="ea413-166">В hello **на URL-адрес входа** текстовом поле введите URL-адрес как:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="ea413-166">In hello **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea413-167">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ea413-167">These values are not real.</span></span> <span data-ttu-id="ea413-168">Вам потребуется tooupdate эти значения из фактический URL-адреса и идентификатор, который описывается далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="ea413-168">You'll need tooupdate these value from actual URLs and Identifier which is explained later in hello tutorial.</span></span>
    
5. <span data-ttu-id="ea413-169">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ea413-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="ea413-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ea413-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ea413-173">tooconfigure единого входа на **123ContactForm** стороны, слишком перейдите[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ea413-173">tooconfigure single sign-on on **123ContactForm** side, go too[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="ea413-175">а.</span><span class="sxs-lookup"><span data-stu-id="ea413-175">a.</span></span> <span data-ttu-id="ea413-176">В hello **электронной почты** в текстовое поле адрес электронной почты пользователя hello т. е. для hello типа</span><span class="sxs-lookup"><span data-stu-id="ea413-176">In hello **Email** textbox, type hello email of hello user i.e</span></span> <span data-ttu-id="ea413-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="ea413-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="ea413-178">b.</span><span class="sxs-lookup"><span data-stu-id="ea413-178">b.</span></span> <span data-ttu-id="ea413-179">Нажмите кнопку **отправить** и обзор hello метаданных XML-файл, который вы скачали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ea413-179">Click **Upload** and browse hello Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="ea413-180">c.</span><span class="sxs-lookup"><span data-stu-id="ea413-180">c.</span></span> <span data-ttu-id="ea413-181">Щелкните **SUBMIT FORM** (Отправить форму).</span><span class="sxs-lookup"><span data-stu-id="ea413-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="ea413-182">На hello **Настройка параметров приложения Microsoft Azure AD единого входа -** выполнения hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ea413-182">On hello **Microsoft Azure AD - Single sign-on - Configure App Settings** perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="ea413-184">а.</span><span class="sxs-lookup"><span data-stu-id="ea413-184">a.</span></span> <span data-ttu-id="ea413-185">При необходимости приложение hello tooconfigure в **режим, инициированный IDP**, hello копирования **идентификатор** значение для экземпляра и вставьте его в **идентификатор** текстовое поле в **123ContactForm URL-адреса и домена** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ea413-185">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="ea413-186">b.</span><span class="sxs-lookup"><span data-stu-id="ea413-186">b.</span></span> <span data-ttu-id="ea413-187">При необходимости приложение hello tooconfigure в **режим, инициированный IDP**, hello копирования **URL-адрес ОТВЕТА** значение для экземпляра и вставьте его в **URL-адрес ответа** текстовое поле в **123ContactForm URL-адреса и домена** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ea413-187">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="ea413-188">c.</span><span class="sxs-lookup"><span data-stu-id="ea413-188">c.</span></span> <span data-ttu-id="ea413-189">При необходимости приложение hello tooconfigure в **режим, инициируемая SP**, hello копирования **URL-адрес входа ON** значение для экземпляра и вставьте его в **на URL-адрес входа** текстовое поле в **123ContactForm URL-адреса и домена** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ea413-189">If you wish tooconfigure hello application in **SP initiated mode**, copy hello **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="ea413-190">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ea413-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ea413-191">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ea413-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ea413-192">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea413-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea413-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea413-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea413-194">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ea413-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ea413-196">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea413-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea413-197">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ea413-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea413-199">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ea413-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea413-201">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ea413-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea413-203">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea413-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea413-205">а.</span><span class="sxs-lookup"><span data-stu-id="ea413-205">a.</span></span> <span data-ttu-id="ea413-206">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea413-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea413-207">b.</span><span class="sxs-lookup"><span data-stu-id="ea413-207">b.</span></span> <span data-ttu-id="ea413-208">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ea413-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea413-209">c.</span><span class="sxs-lookup"><span data-stu-id="ea413-209">c.</span></span> <span data-ttu-id="ea413-210">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ea413-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ea413-211">d.</span><span class="sxs-lookup"><span data-stu-id="ea413-211">d.</span></span> <span data-ttu-id="ea413-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ea413-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="ea413-213">Создание тестового пользователя 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="ea413-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="ea413-214">В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение.</span><span class="sxs-lookup"><span data-stu-id="ea413-214">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ea413-215">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ea413-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ea413-216">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления too123ContactForm доступа.</span><span class="sxs-lookup"><span data-stu-id="ea413-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too123ContactForm.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ea413-218">**tooassign too123ContactForm Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea413-218">**tooassign Britta Simon too123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea413-219">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea413-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ea413-221">В списке приложений hello выберите **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="ea413-221">In hello applications list, select **123ContactForm**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="ea413-223">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ea413-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ea413-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ea413-225">Click **Add** button.</span></span> <span data-ttu-id="ea413-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ea413-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ea413-228">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ea413-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ea413-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ea413-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea413-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ea413-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea413-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ea413-231">Testing single sign-on</span></span>

<span data-ttu-id="ea413-232">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ea413-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ea413-233">При нажатии кнопки hello 123ContactForm плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour 123ContactForm приложения.</span><span class="sxs-lookup"><span data-stu-id="ea413-233">When you click hello 123ContactForm tile in hello Access Panel, you should get automatically signed-on tooyour 123ContactForm application.</span></span>
<span data-ttu-id="ea413-234">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ea413-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea413-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ea413-235">Additional resources</span></span>

* [<span data-ttu-id="ea413-236">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea413-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea413-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ea413-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

