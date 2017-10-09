---
title: "Руководство. Интеграция Azure Active Directory с Convercent | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: e6d09d7de52779dcf05e80215df9369ebc2ed06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="3d0ea-103">Руководство. Интеграция Azure Active Directory с Convercent</span><span class="sxs-lookup"><span data-stu-id="3d0ea-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="3d0ea-104">В этом учебнике вы узнаете, как toointegrate Convercent с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d0ea-104">In this tutorial, you learn how toointegrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d0ea-105">Интеграция с Azure AD Convercent предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3d0ea-105">Integrating Convercent with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3d0ea-106">Можно управлять в Azure AD, имеющего доступ tooConvercent</span><span class="sxs-lookup"><span data-stu-id="3d0ea-106">You can control in Azure AD who has access tooConvercent</span></span>
- <span data-ttu-id="3d0ea-107">Можно включить на пользователей tooautomatically get вошедшего tooConvercent (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0ea-107">You can enable your users tooautomatically get signed-on tooConvercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d0ea-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3d0ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3d0ea-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d0ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d0ea-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3d0ea-110">Prerequisites</span></span>

<span data-ttu-id="3d0ea-111">tooconfigure интеграция Azure AD с Convercent требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3d0ea-111">tooconfigure Azure AD integration with Convercent, you need hello following items:</span></span>

- <span data-ttu-id="3d0ea-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3d0ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d0ea-113">подписка Convercent с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d0ea-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d0ea-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3d0ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d0ea-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d0ea-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d0ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d0ea-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3d0ea-118">Scenario description</span></span>
<span data-ttu-id="3d0ea-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d0ea-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3d0ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d0ea-121">Добавление Convercent из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3d0ea-121">Adding Convercent from hello gallery</span></span>
2. <span data-ttu-id="3d0ea-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-hello-gallery"></a><span data-ttu-id="3d0ea-123">Добавление Convercent из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3d0ea-123">Adding Convercent from hello gallery</span></span>
<span data-ttu-id="3d0ea-124">tooconfigure hello интеграции Convercent в Azure AD, вы должны tooadd Convercent из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-124">tooconfigure hello integration of Convercent into Azure AD, you need tooadd Convercent from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3d0ea-125">**tooadd Convercent из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3d0ea-125">**tooadd Convercent from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d0ea-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d0ea-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3d0ea-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3d0ea-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3d0ea-133">Введите в поле поиска hello **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-133">In hello search box, type **Convercent**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="3d0ea-135">В панели результатов hello выберите **Convercent**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-135">In hello results panel, select **Convercent**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d0ea-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d0ea-138">В этом разделе описана настройка и проверка единого входа Azure AD в Convercent с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3d0ea-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Convercent является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Convercent is tooa user in Azure AD.</span></span> <span data-ttu-id="3d0ea-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Convercent должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-140">In other words, a link relationship between an Azure AD user and hello related user in Convercent needs toobe established.</span></span>

<span data-ttu-id="3d0ea-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Convercent.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Convercent.</span></span>

<span data-ttu-id="3d0ea-142">tooconfigure и теста Azure AD единого входа с Convercent, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3d0ea-142">tooconfigure and test Azure AD single sign-on with Convercent, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3d0ea-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3d0ea-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d0ea-145">**[Создание тестового пользователя Convercent](#creating-a-convercent-test-user)**  -toohave аналог Саймон Britta в Convercent, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - toohave a counterpart of Britta Simon in Convercent that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d0ea-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d0ea-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d0ea-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d0ea-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Convercent.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="3d0ea-150">**tooconfigure Azure AD единого входа с Convercent, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3d0ea-150">**tooconfigure Azure AD single sign-on with Convercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d0ea-151">В hello в hello портала Azure **Convercent** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-151">In hello Azure portal, on hello **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3d0ea-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="3d0ea-155">На hello **URL-адреса и домена Convercent** статьи, при желании tooconfigure приложения hello в **режим, инициированный IDP**, выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="3d0ea-155">On hello **Convercent Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="3d0ea-157">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="3d0ea-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="3d0ea-158">При желании tooconfigure приложения hello в **режиме, инициируемая SP**, на hello **URL-адреса и домена Convercent** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3d0ea-158">If you wish tooconfigure hello application in **SP initiated mode**, on hello **Convercent Domain and URLs** section perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="3d0ea-160">а.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-160">a.</span></span> <span data-ttu-id="3d0ea-161">Щелкните **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="3d0ea-162">b.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-162">b.</span></span> <span data-ttu-id="3d0ea-163">В hello **на URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="3d0ea-163">In hello **Sign On URL** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="3d0ea-164">c.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-164">c.</span></span> <span data-ttu-id="3d0ea-165">В hello **состояние ретрансляции** текстовое значение hello типа, используя следующий шаблон hello:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="3d0ea-165">In hello **Relay State** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d0ea-166">Эти значения не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-166">These values are not hello real values.</span></span> <span data-ttu-id="3d0ea-167">Обновить значения hello фактический идентификатор, на URL-адрес входа и состояние ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-167">Update these values with hello actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="3d0ea-168">Обратитесь к [группа поддержки клиента Convercent](http://support.convercent.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-168">Contact [Convercent Client support team](http://support.convercent.com) tooget these values.</span></span>

5. <span data-ttu-id="3d0ea-169">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="3d0ea-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3d0ea-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3d0ea-173">tooget SSO настроен для вашего приложения, обратитесь в службу [Convercent поддержки](mailto:support@convercent.com) и предоставить им загружаются hello **метаданные в формате XML**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-173">tooget SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with hello downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="3d0ea-174">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3d0ea-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3d0ea-175">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3d0ea-176">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d0ea-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d0ea-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0ea-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d0ea-178">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3d0ea-180">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3d0ea-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d0ea-181">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d0ea-183">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d0ea-185">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="3d0ea-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d0ea-187">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3d0ea-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d0ea-189">а.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-189">a.</span></span> <span data-ttu-id="3d0ea-190">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d0ea-191">b.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-191">b.</span></span> <span data-ttu-id="3d0ea-192">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d0ea-193">c.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-193">c.</span></span> <span data-ttu-id="3d0ea-194">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3d0ea-195">d.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-195">d.</span></span> <span data-ttu-id="3d0ea-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="3d0ea-197">Создание тестового пользователя Convercent</span><span class="sxs-lookup"><span data-stu-id="3d0ea-197">Creating a Convercent test user</span></span>

<span data-ttu-id="3d0ea-198">Работать с [Convercent поддержки](mailto:support@convercent.com) tooadd hello пользователей на платформе Convercent hello.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-198">Work with [Convercent support team](mailto:support@convercent.com) tooadd hello users in hello Convercent platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3d0ea-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3d0ea-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3d0ea-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooConvercent доступа.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConvercent.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3d0ea-202">**tooassign tooConvercent Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3d0ea-202">**tooassign Britta Simon tooConvercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d0ea-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3d0ea-205">В списке приложений hello выберите **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-205">In hello applications list, select **Convercent**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="3d0ea-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3d0ea-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-209">Click **Add** button.</span></span> <span data-ttu-id="3d0ea-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3d0ea-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3d0ea-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d0ea-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d0ea-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3d0ea-215">Testing single sign-on</span></span>

<span data-ttu-id="3d0ea-216">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3d0ea-217">При нажатии кнопки hello Convercent плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Convercent приложения.</span><span class="sxs-lookup"><span data-stu-id="3d0ea-217">When you click hello Convercent tile in hello Access Panel, you should get automatically signed-on tooyour Convercent application.</span></span>
<span data-ttu-id="3d0ea-218">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d0ea-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3d0ea-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3d0ea-219">Additional resources</span></span>

* [<span data-ttu-id="3d0ea-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d0ea-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d0ea-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d0ea-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

