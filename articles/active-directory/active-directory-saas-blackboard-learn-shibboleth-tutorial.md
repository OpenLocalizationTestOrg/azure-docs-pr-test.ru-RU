---
title: "Руководство по интеграции Azure Active Directory с Blackboard Learn — Shibboleth | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и узнайте, Blackboard - Shibboleth."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 40aa3ec5f42b93157af3c56daaadfa66203b21d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="39c38-103">Руководство. Интеграция Azure Active Directory с Blackboard Learn — Shibboleth</span><span class="sxs-lookup"><span data-stu-id="39c38-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="39c38-104">В этом учебнике вы узнаете, как узнать Blackboard - toointegrate Shibboleth с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39c38-104">In this tutorial, you learn how toointegrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39c38-105">Интеграция подробнее Blackboard - Shibboleth с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="39c38-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="39c38-106">Можно управлять в Azure AD, имеющего доступ tooBlackboard подробнее - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="39c38-106">You can control in Azure AD who has access tooBlackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="39c38-107">Можно включить на пользователей tooautomatically get вошедшего tooBlackboard подробнее - Shibboleth (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="39c38-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39c38-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="39c38-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="39c38-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39c38-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39c38-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="39c38-110">Prerequisites</span></span>

<span data-ttu-id="39c38-111">Интеграция Azure AD с узнать Blackboard - Shibboleth, tooconfigure требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="39c38-111">tooconfigure Azure AD integration with Blackboard Learn - Shibboleth, you need hello following items:</span></span>

- <span data-ttu-id="39c38-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="39c38-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39c38-113">подписка на Blackboard Learn — Shibboleth с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="39c38-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39c38-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="39c38-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39c38-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="39c38-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39c38-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="39c38-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39c38-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39c38-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39c38-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="39c38-118">Scenario description</span></span>
<span data-ttu-id="39c38-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="39c38-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39c38-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="39c38-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39c38-121">Добавление подробнее Blackboard - Shibboleth из галереи hello</span><span class="sxs-lookup"><span data-stu-id="39c38-121">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
2. <span data-ttu-id="39c38-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39c38-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-hello-gallery"></a><span data-ttu-id="39c38-123">Добавление подробнее Blackboard - Shibboleth из галереи hello</span><span class="sxs-lookup"><span data-stu-id="39c38-123">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
<span data-ttu-id="39c38-124">Интеграция hello tooconfigure узнать Blackboard - Shibboleth в Azure AD, необходимо узнать Blackboard - tooadd Shibboleth из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="39c38-124">tooconfigure hello integration of Blackboard Learn - Shibboleth into Azure AD, you need tooadd Blackboard Learn - Shibboleth from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39c38-125">**Узнайте Blackboard - tooadd Shibboleth из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="39c38-125">**tooadd Blackboard Learn - Shibboleth from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39c38-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="39c38-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39c38-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="39c38-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="39c38-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="39c38-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="39c38-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="39c38-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="39c38-133">Введите в поле поиска hello **Blackboard узнать - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="39c38-133">In hello search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="39c38-135">В панели результатов hello выберите **Blackboard узнать - Shibboleth**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="39c38-135">In hello results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39c38-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39c38-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39c38-138">В этом разделе описана настройка и проверка единого входа Azure AD в Blackboard Learn — Shibboleth с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39c38-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="39c38-139">Для единого входа toowork Azure AD необходима tooknow, какой пользователь аналог hello в узнать Blackboard - Shibboleth tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39c38-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn - Shibboleth is tooa user in Azure AD.</span></span> <span data-ttu-id="39c38-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в узнать Blackboard - Shibboleth должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="39c38-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn - Shibboleth needs toobe established.</span></span>

<span data-ttu-id="39c38-141">В сведения Blackboard - Shibboleth, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="39c38-141">In Blackboard Learn - Shibboleth, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="39c38-142">tooconfigure и теста Azure AD единого входа с узнать Blackboard - Shibboleth, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="39c38-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39c38-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="39c38-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39c38-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="39c38-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39c38-145">**[Создание Blackboard узнать - тестового пользователя Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**  - toohave аналог Саймон Britta в узнать Blackboard - Shibboleth, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="39c38-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="39c38-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="39c38-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39c38-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="39c38-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39c38-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39c38-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39c38-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей Blackboard узнать - Shibboleth приложения.</span><span class="sxs-lookup"><span data-stu-id="39c38-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="39c38-150">**tooconfigure Azure AD единого входа с узнать Blackboard - Shibboleth, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="39c38-150">**tooconfigure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="39c38-151">В hello в hello портала Azure **Blackboard узнать - Shibboleth** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="39c38-151">In hello Azure portal, on hello **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="39c38-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="39c38-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="39c38-155">На hello **Blackboard узнать - URL-адреса и домена Shibboleth** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="39c38-155">On hello **Blackboard Learn - Shibboleth Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="39c38-157">а.</span><span class="sxs-lookup"><span data-stu-id="39c38-157">a.</span></span> <span data-ttu-id="39c38-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="39c38-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="39c38-159">b.</span><span class="sxs-lookup"><span data-stu-id="39c38-159">b.</span></span> <span data-ttu-id="39c38-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="39c38-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="39c38-161">c.</span><span class="sxs-lookup"><span data-stu-id="39c38-161">c.</span></span> <span data-ttu-id="39c38-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="39c38-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="39c38-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="39c38-163">These values are not real.</span></span> <span data-ttu-id="39c38-164">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="39c38-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="39c38-165">Обратитесь к [Blackboard узнать - группа поддержки клиента Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="39c38-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="39c38-166">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="39c38-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="39c38-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="39c38-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="39c38-170">На hello **Blackboard узнать - конфигурации Shibboleth** щелкните **Настройка Blackboard узнать - Shibboleth** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="39c38-170">On hello **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="39c38-171">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="39c38-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="39c38-173">tooconfigure единого входа на **Blackboard узнать - Shibboleth** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа службы URL-адрес** слишком[Blackboard узнать - группа поддержки Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="39c38-173">tooconfigure single sign-on on **Blackboard Learn - Shibboleth** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="39c38-174">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="39c38-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="39c38-175">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="39c38-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="39c38-176">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39c38-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39c38-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="39c38-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="39c38-178">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="39c38-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="39c38-180">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="39c38-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39c38-181">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="39c38-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39c38-183">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="39c38-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39c38-185">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="39c38-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39c38-187">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="39c38-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39c38-189">а.</span><span class="sxs-lookup"><span data-stu-id="39c38-189">a.</span></span> <span data-ttu-id="39c38-190">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39c38-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39c38-191">b.</span><span class="sxs-lookup"><span data-stu-id="39c38-191">b.</span></span> <span data-ttu-id="39c38-192">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39c38-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39c38-193">c.</span><span class="sxs-lookup"><span data-stu-id="39c38-193">c.</span></span> <span data-ttu-id="39c38-194">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="39c38-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="39c38-195">d.</span><span class="sxs-lookup"><span data-stu-id="39c38-195">d.</span></span> <span data-ttu-id="39c38-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="39c38-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="39c38-197">Создание тестового пользователя Blackboard Learn — Shibboleth</span><span class="sxs-lookup"><span data-stu-id="39c38-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="39c38-198">В этом разделе описано, как создать пользователя Britta Simon в приложении Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="39c38-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="39c38-199">Работать с вашей [Blackboard узнать - группа поддержки Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd пользователей hello в hello узнать Blackboard - Shibboleth платформы.</span><span class="sxs-lookup"><span data-stu-id="39c38-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd hello users in hello Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="39c38-200">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="39c38-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="39c38-201">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooBlackboard подробнее - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="39c38-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn - Shibboleth.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="39c38-203">**tooassign Britta Simon tooBlackboard подробнее - Shibboleth, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="39c38-203">**tooassign Britta Simon tooBlackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="39c38-204">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="39c38-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="39c38-206">В списке приложений hello выберите **Blackboard узнать - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="39c38-206">In hello applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="39c38-208">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="39c38-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="39c38-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="39c38-210">Click **Add** button.</span></span> <span data-ttu-id="39c38-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="39c38-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="39c38-213">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="39c38-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="39c38-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="39c38-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39c38-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="39c38-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39c38-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="39c38-216">Testing single sign-on</span></span>

<span data-ttu-id="39c38-217">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="39c38-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="39c38-218">При нажатии кнопки hello узнать Blackboard - Shibboleth плитки в панели доступа hello следует получать автоматически вошедшего tooyour узнать Blackboard - Shibboleth приложения.</span><span class="sxs-lookup"><span data-stu-id="39c38-218">When you click hello Blackboard Learn - Shibboleth tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39c38-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="39c38-219">Additional resources</span></span>

* [<span data-ttu-id="39c38-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39c38-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39c38-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39c38-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

