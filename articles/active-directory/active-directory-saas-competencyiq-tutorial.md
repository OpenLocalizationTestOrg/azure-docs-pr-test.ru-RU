---
title: "Руководство по интеграции Azure Active Directory с CompetencyIQ | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и CompetencyIQ."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: c032884b092da85684e24e98f75371475e09322d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="45be8-103">Руководство по интеграции Azure Active Directory с CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="45be8-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="45be8-104">В этом учебнике вы узнаете, как toointegrate CompetencyIQ с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="45be8-104">In this tutorial, you learn how toointegrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45be8-105">Интеграция с Azure AD CompetencyIQ предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="45be8-105">Integrating CompetencyIQ with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="45be8-106">Можно управлять в Azure AD, имеющего доступ tooCompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="45be8-106">You can control in Azure AD who has access tooCompetencyIQ</span></span>
- <span data-ttu-id="45be8-107">Можно включить на пользователей tooautomatically get вошедшего tooCompetencyIQ (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="45be8-107">You can enable your users tooautomatically get signed-on tooCompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="45be8-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="45be8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="45be8-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45be8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45be8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="45be8-110">Prerequisites</span></span>

<span data-ttu-id="45be8-111">tooconfigure интеграция Azure AD с CompetencyIQ требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="45be8-111">tooconfigure Azure AD integration with CompetencyIQ, you need hello following items:</span></span>

- <span data-ttu-id="45be8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="45be8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="45be8-113">подписка CompetencyIQ с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="45be8-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="45be8-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="45be8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="45be8-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="45be8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45be8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="45be8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="45be8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45be8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45be8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="45be8-118">Scenario description</span></span>
<span data-ttu-id="45be8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="45be8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45be8-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="45be8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45be8-121">Добавление CompetencyIQ из галереи hello</span><span class="sxs-lookup"><span data-stu-id="45be8-121">Adding CompetencyIQ from hello gallery</span></span>
2. <span data-ttu-id="45be8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="45be8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-hello-gallery"></a><span data-ttu-id="45be8-123">Добавление CompetencyIQ из галереи hello</span><span class="sxs-lookup"><span data-stu-id="45be8-123">Adding CompetencyIQ from hello gallery</span></span>
<span data-ttu-id="45be8-124">tooconfigure hello интеграции CompetencyIQ в Azure AD, вы должны tooadd CompetencyIQ из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="45be8-124">tooconfigure hello integration of CompetencyIQ into Azure AD, you need tooadd CompetencyIQ from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="45be8-125">**tooadd CompetencyIQ из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="45be8-125">**tooadd CompetencyIQ from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="45be8-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="45be8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="45be8-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="45be8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="45be8-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="45be8-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="45be8-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="45be8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="45be8-133">Введите в поле поиска hello **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="45be8-133">In hello search box, type **CompetencyIQ**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_search.png)

5. <span data-ttu-id="45be8-135">В панели результатов hello выберите **CompetencyIQ**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="45be8-135">In hello results panel, select **CompetencyIQ**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45be8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="45be8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45be8-138">В этом разделе описана настройка и проверка единого входа Azure AD в CompetencyIQ с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="45be8-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="45be8-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в CompetencyIQ является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45be8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CompetencyIQ is tooa user in Azure AD.</span></span> <span data-ttu-id="45be8-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в CompetencyIQ должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="45be8-140">In other words, a link relationship between an Azure AD user and hello related user in CompetencyIQ needs toobe established.</span></span>

<span data-ttu-id="45be8-141">В CompetencyIQ, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="45be8-141">In CompetencyIQ, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="45be8-142">tooconfigure и теста Azure AD единого входа с CompetencyIQ, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="45be8-142">tooconfigure and test Azure AD single sign-on with CompetencyIQ, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="45be8-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="45be8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="45be8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="45be8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="45be8-145">**[Создание тестового пользователя CompetencyIQ](#creating-a-competencyiq-test-user)**  -toohave аналог Саймон Britta в CompetencyIQ, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="45be8-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - toohave a counterpart of Britta Simon in CompetencyIQ that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="45be8-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="45be8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="45be8-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="45be8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="45be8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="45be8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="45be8-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="45be8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="45be8-150">**tooconfigure Azure AD единого входа с CompetencyIQ, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="45be8-150">**tooconfigure Azure AD single sign-on with CompetencyIQ, perform hello following steps:**</span></span>

1. <span data-ttu-id="45be8-151">В hello в hello портала Azure **CompetencyIQ** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="45be8-151">In hello Azure portal, on hello **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="45be8-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="45be8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

3. <span data-ttu-id="45be8-155">На hello **URL-адреса и домена CompetencyIQ** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="45be8-155">On hello **CompetencyIQ Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="45be8-157">а.</span><span class="sxs-lookup"><span data-stu-id="45be8-157">a.</span></span> <span data-ttu-id="45be8-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<customer>.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="45be8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="45be8-159">b.</span><span class="sxs-lookup"><span data-stu-id="45be8-159">b.</span></span> <span data-ttu-id="45be8-160">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="45be8-160">In hello **Identifier** textbox, type hello URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="45be8-161">значение URL-адреса Hello входа real таким образом обновляет это фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="45be8-161">hello Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="45be8-162">Обратитесь к [группа поддержки клиента CompetencyIQ](https://www.competencyiq.com/) tooget это.</span><span class="sxs-lookup"><span data-stu-id="45be8-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) tooget this.</span></span> 
 
4. <span data-ttu-id="45be8-163">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="45be8-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

5. <span data-ttu-id="45be8-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="45be8-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-competencyiq-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="45be8-167">На hello **конфигурации CompetencyIQ** щелкните **Настройка CompetencyIQ** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="45be8-167">On hello **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="45be8-168">Копировать hello **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="45be8-168">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_configure.png) 

7. <span data-ttu-id="45be8-170">tooconfigure единого входа на **CompetencyIQ** стороны, необходимо загрузить hello toosend **метаданные в формате XML**, **идентификатор сущности SAML** и **SAML Single Sign-On URL-адрес службы** слишком[CompetencyIQ поддержки](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="45be8-170">tooconfigure single sign-on on **CompetencyIQ** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="45be8-171">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="45be8-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="45be8-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="45be8-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="45be8-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="45be8-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="45be8-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="45be8-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45be8-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="45be8-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="45be8-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="45be8-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="45be8-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="45be8-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="45be8-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="45be8-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="45be8-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="45be8-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="45be8-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="45be8-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45be8-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="45be8-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="45be8-187">а.</span><span class="sxs-lookup"><span data-stu-id="45be8-187">a.</span></span> <span data-ttu-id="45be8-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="45be8-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="45be8-189">b.</span><span class="sxs-lookup"><span data-stu-id="45be8-189">b.</span></span> <span data-ttu-id="45be8-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="45be8-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="45be8-191">c.</span><span class="sxs-lookup"><span data-stu-id="45be8-191">c.</span></span> <span data-ttu-id="45be8-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="45be8-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="45be8-193">d.</span><span class="sxs-lookup"><span data-stu-id="45be8-193">d.</span></span> <span data-ttu-id="45be8-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="45be8-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="45be8-195">Создание тестового пользователя CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="45be8-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="45be8-196">Пользователи toolog tooenable Azure AD в tooCompetencyIQ, их необходимо подготовить в CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="45be8-196">tooenable Azure AD users toolog in tooCompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="45be8-197">Обратитесь к [CompetencyIQ поддержки](https://www.competencyiq.com/) toocreate пользователей в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="45be8-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) toocreate users in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="45be8-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="45be8-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="45be8-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooCompetencyIQ доступа.</span><span class="sxs-lookup"><span data-stu-id="45be8-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCompetencyIQ.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="45be8-201">**tooassign tooCompetencyIQ Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="45be8-201">**tooassign Britta Simon tooCompetencyIQ, perform hello following steps:**</span></span>

1. <span data-ttu-id="45be8-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="45be8-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="45be8-204">В списке приложений hello выберите **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="45be8-204">In hello applications list, select **CompetencyIQ**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_app.png) 

3. <span data-ttu-id="45be8-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="45be8-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="45be8-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="45be8-208">Click **Add** button.</span></span> <span data-ttu-id="45be8-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="45be8-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="45be8-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="45be8-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="45be8-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="45be8-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45be8-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="45be8-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="45be8-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="45be8-214">Testing single sign-on</span></span>

<span data-ttu-id="45be8-215">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="45be8-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="45be8-216">Если щелкнуть плитку CompetencyIQ hello в hello панели доступа, вы должны получить автоматически входить в приложения hello.</span><span class="sxs-lookup"><span data-stu-id="45be8-216">When you click hello CompetencyIQ tile in hello Access Panel, you should get automatically logged into hello application.</span></span>
<span data-ttu-id="45be8-217">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="45be8-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="45be8-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="45be8-218">Additional resources</span></span>

* [<span data-ttu-id="45be8-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45be8-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45be8-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="45be8-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_203.png

