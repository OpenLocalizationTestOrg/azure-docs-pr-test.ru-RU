---
title: "Руководство по интеграции Azure Active Directory с Bridge | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и моста."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 85e1917de63356a86aa87a0f82621391733ab2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="5fd3e-103">Руководство. Интеграция Azure Active Directory с Bridge</span><span class="sxs-lookup"><span data-stu-id="5fd3e-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="5fd3e-104">В этом учебнике вы узнаете, как мост toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fd3e-104">In this tutorial, you learn how toointegrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fd3e-105">Интеграция моста с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5fd3e-105">Integrating Bridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5fd3e-106">Можно управлять в Azure AD, имеющего доступ tooBridge</span><span class="sxs-lookup"><span data-stu-id="5fd3e-106">You can control in Azure AD who has access tooBridge</span></span>
- <span data-ttu-id="5fd3e-107">Можно включить на пользователей tooautomatically get вошедшего tooBridge (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fd3e-107">You can enable your users tooautomatically get signed-on tooBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5fd3e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5fd3e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5fd3e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fd3e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fd3e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5fd3e-110">Prerequisites</span></span>

<span data-ttu-id="5fd3e-111">tooconfigure интеграция Azure AD с помощью моста требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5fd3e-111">tooconfigure Azure AD integration with Bridge, you need hello following items:</span></span>

- <span data-ttu-id="5fd3e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5fd3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fd3e-113">подписка Bridge с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fd3e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fd3e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5fd3e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fd3e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fd3e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fd3e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fd3e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5fd3e-118">Scenario description</span></span>
<span data-ttu-id="5fd3e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fd3e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5fd3e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fd3e-121">Добавление моста из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5fd3e-121">Adding Bridge from hello gallery</span></span>
2. <span data-ttu-id="5fd3e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fd3e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-hello-gallery"></a><span data-ttu-id="5fd3e-123">Добавление моста из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5fd3e-123">Adding Bridge from hello gallery</span></span>
<span data-ttu-id="5fd3e-124">tooconfigure hello интеграции моста в Azure AD, вы должны моста tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-124">tooconfigure hello integration of Bridge into Azure AD, you need tooadd Bridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5fd3e-125">**Мост tooadd из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="5fd3e-125">**tooadd Bridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fd3e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5fd3e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5fd3e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5fd3e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5fd3e-133">Введите в поле поиска hello **моста**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-133">In hello search box, type **Bridge**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. <span data-ttu-id="5fd3e-135">В панели результатов hello выберите **моста**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-135">In hello results panel, select **Bridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5fd3e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fd3e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5fd3e-138">В этом разделе описана настройка и проверка единого входа Azure AD в Bridge с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5fd3e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в мост является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bridge is tooa user in Azure AD.</span></span> <span data-ttu-id="5fd3e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в мост должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-140">In other words, a link relationship between an Azure AD user and hello related user in Bridge needs toobe established.</span></span>

<span data-ttu-id="5fd3e-141">В мост, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-141">In Bridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5fd3e-142">tooconfigure и тестирования Azure AD единого входа с помощью моста, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5fd3e-142">tooconfigure and test Azure AD single sign-on with Bridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5fd3e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5fd3e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fd3e-145">**[Создание тестового пользователя моста](#creating-a-bridge-test-user)**  -toohave аналог Саймон Britta в мост, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - toohave a counterpart of Britta Simon in Bridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fd3e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fd3e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5fd3e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fd3e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5fd3e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении моста.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="5fd3e-150">**tooconfigure Azure AD единого входа с помощью моста, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5fd3e-150">**tooconfigure Azure AD single sign-on with Bridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fd3e-151">В hello в hello портала Azure **моста** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-151">In hello Azure portal, on hello **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5fd3e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. <span data-ttu-id="5fd3e-155">На hello **URL-адреса и домена моста** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5fd3e-155">On hello **Bridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="5fd3e-157">а.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-157">a.</span></span> <span data-ttu-id="5fd3e-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="5fd3e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="5fd3e-159">b.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-159">b.</span></span> <span data-ttu-id="5fd3e-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="5fd3e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fd3e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-161">These values are not real.</span></span> <span data-ttu-id="5fd3e-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5fd3e-163">Обратитесь к [группа поддержки клиента моста](https://community.bridgeapp.com/community/help) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="5fd3e-164">На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. <span data-ttu-id="5fd3e-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5fd3e-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fd3e-168">На hello **конфигурации моста** щелкните **настройка моста** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-168">On hello **Bridge Configuration** section, click **Configure Bridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5fd3e-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="5fd3e-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. <span data-ttu-id="5fd3e-171">tooconfigure единого входа на **моста** стороны, необходимо загрузить hello toosend **Certificate(Raw)** и **SAML идентификатор сущности, SAML единого входа URL-адрес службы и URL-адрес выхода**слишком[группа поддержки моста](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="5fd3e-171">tooconfigure single sign-on on **Bridge** side, you need toosend hello downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** too[Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="5fd3e-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5fd3e-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5fd3e-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5fd3e-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fd3e-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5fd3e-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fd3e-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="5fd3e-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5fd3e-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5fd3e-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fd3e-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5fd3e-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5fd3e-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="5fd3e-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5fd3e-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5fd3e-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5fd3e-187">а.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-187">a.</span></span> <span data-ttu-id="5fd3e-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fd3e-189">b.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-189">b.</span></span> <span data-ttu-id="5fd3e-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5fd3e-191">c.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-191">c.</span></span> <span data-ttu-id="5fd3e-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5fd3e-193">d.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-193">d.</span></span> <span data-ttu-id="5fd3e-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="5fd3e-195">Создание тестового пользователя Bridge</span><span class="sxs-lookup"><span data-stu-id="5fd3e-195">Creating a Bridge test user</span></span>

<span data-ttu-id="5fd3e-196">В этом разделе описано, как создать пользователя Britta Simon в Bridge.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="5fd3e-197">Работать с [группа поддержки клиента моста](https://community.bridgeapp.com/community/help) toocreate пользователя на платформе hello.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) toocreate a user in hello platform.</span></span> <span data-ttu-id="5fd3e-198">Можно вызвать hello в службу поддержки с помощью моста из <a href="https://community.bridgeapp.com/community/help">здесь</a> tooadd hello пользователей на платформе моста hello.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-198">You can raise hello support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> tooadd hello users in hello Bridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5fd3e-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5fd3e-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5fd3e-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBridge доступа.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBridge.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5fd3e-202">**tooassign tooBridge Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5fd3e-202">**tooassign Britta Simon tooBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fd3e-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5fd3e-205">В списке приложений hello выберите **моста**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-205">In hello applications list, select **Bridge**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. <span data-ttu-id="5fd3e-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5fd3e-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-209">Click **Add** button.</span></span> <span data-ttu-id="5fd3e-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5fd3e-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5fd3e-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fd3e-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5fd3e-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5fd3e-215">Testing single sign-on</span></span>

<span data-ttu-id="5fd3e-216">В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-216">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5fd3e-217">При выборе плитки моста hello в hello панели доступа, следует получать автоматически вошедшего моста tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="5fd3e-217">When you click hello Bridge tile in hello Access Panel, you should get automatically signed-on tooyour Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5fd3e-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5fd3e-218">Additional resources</span></span>

* [<span data-ttu-id="5fd3e-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fd3e-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fd3e-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fd3e-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png

