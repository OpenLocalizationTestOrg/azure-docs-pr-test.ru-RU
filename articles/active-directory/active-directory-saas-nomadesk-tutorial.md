---
title: "Руководство по интеграции Azure Active Directory с Nomadesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Nomadesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d261b776-b48e-45f0-9722-0297adefabb8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 9aa55ba6106ea24f556217cfe84d21d7415d9c78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadesk"></a><span data-ttu-id="1e7ac-103">Руководство. Интеграция Azure Active Directory с Nomadesk</span><span class="sxs-lookup"><span data-stu-id="1e7ac-103">Tutorial: Azure Active Directory integration with Nomadesk</span></span>

<span data-ttu-id="1e7ac-104">В этом учебнике вы узнаете, как toointegrate Nomadesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e7ac-104">In this tutorial, you learn how toointegrate Nomadesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e7ac-105">Интеграция с Azure AD Nomadesk предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1e7ac-105">Integrating Nomadesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e7ac-106">Можно управлять в Azure AD, имеющего доступ tooNomadesk</span><span class="sxs-lookup"><span data-stu-id="1e7ac-106">You can control in Azure AD who has access tooNomadesk</span></span>
- <span data-ttu-id="1e7ac-107">Можно включить на пользователей tooautomatically get вошедшего tooNomadesk (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7ac-107">You can enable your users tooautomatically get signed-on tooNomadesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e7ac-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1e7ac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1e7ac-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e7ac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e7ac-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1e7ac-110">Prerequisites</span></span>

<span data-ttu-id="1e7ac-111">tooconfigure интеграция Azure AD с Nomadesk требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1e7ac-111">tooconfigure Azure AD integration with Nomadesk, you need hello following items:</span></span>

- <span data-ttu-id="1e7ac-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1e7ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e7ac-113">подписка Nomadesk с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-113">A Nomadesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e7ac-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e7ac-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1e7ac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e7ac-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e7ac-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e7ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e7ac-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1e7ac-118">Scenario description</span></span>
<span data-ttu-id="1e7ac-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e7ac-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1e7ac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e7ac-121">Добавление Nomadesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1e7ac-121">Adding Nomadesk from hello gallery</span></span>
2. <span data-ttu-id="1e7ac-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nomadesk-from-hello-gallery"></a><span data-ttu-id="1e7ac-123">Добавление Nomadesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1e7ac-123">Adding Nomadesk from hello gallery</span></span>
<span data-ttu-id="1e7ac-124">tooconfigure hello интеграции Nomadesk в Azure AD, вы должны tooadd Nomadesk из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-124">tooconfigure hello integration of Nomadesk into Azure AD, you need tooadd Nomadesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e7ac-125">**tooadd Nomadesk из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e7ac-125">**tooadd Nomadesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e7ac-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e7ac-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1e7ac-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1e7ac-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1e7ac-133">Введите в поле поиска hello **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-133">In hello search box, type **Nomadesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_search.png)

5. <span data-ttu-id="1e7ac-135">В панели результатов hello выберите **Nomadesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-135">In hello results panel, select **Nomadesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e7ac-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e7ac-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложении Nomadesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-138">In this section, you configure and test Azure AD single sign-on with Nomadesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e7ac-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Nomadesk является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nomadesk is tooa user in Azure AD.</span></span> <span data-ttu-id="1e7ac-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Nomadesk должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-140">In other words, a link relationship between an Azure AD user and hello related user in Nomadesk needs toobe established.</span></span>

<span data-ttu-id="1e7ac-141">В Nomadesk, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-141">In Nomadesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1e7ac-142">tooconfigure и теста Azure AD единого входа с Nomadesk, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1e7ac-142">tooconfigure and test Azure AD single sign-on with Nomadesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e7ac-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e7ac-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e7ac-145">**[Создание тестового пользователя Nomadesk](#creating-a-nomadesk-test-user)**  -toohave аналог Саймон Britta в Nomadesk, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-145">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - toohave a counterpart of Britta Simon in Nomadesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e7ac-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e7ac-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e7ac-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e7ac-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nomadesk application.</span></span>

<span data-ttu-id="1e7ac-150">**tooconfigure Azure AD единого входа с Nomadesk, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e7ac-150">**tooconfigure Azure AD single sign-on with Nomadesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e7ac-151">В hello в hello портала Azure **Nomadesk** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-151">In hello Azure portal, on hello **Nomadesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1e7ac-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_samlbase.png)

3. <span data-ttu-id="1e7ac-155">На hello **URL-адреса и домена Nomadesk** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e7ac-155">On hello **Nomadesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_url.png)

    <span data-ttu-id="1e7ac-157">а.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-157">a.</span></span> <span data-ttu-id="1e7ac-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://mynomadesk.com/logon/saml/<TENANTID>`</span><span class="sxs-lookup"><span data-stu-id="1e7ac-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mynomadesk.com/logon/saml/<TENANTID>`</span></span>

    <span data-ttu-id="1e7ac-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-159">b.</span></span> <span data-ttu-id="1e7ac-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://secure.nomadesk.com/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1e7ac-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://secure.nomadesk.com/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e7ac-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-161">These values are not real.</span></span> <span data-ttu-id="1e7ac-162">Обновите эти значения с hello фактический URL-адрес входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="1e7ac-163">Обратитесь к [группа поддержки клиента Nomadesk](mailto:support@nomadesk.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-163">Contact [Nomadesk Client support team](mailto:support@nomadesk.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="1e7ac-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_certificate.png) 

5. <span data-ttu-id="1e7ac-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1e7ac-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nomadesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e7ac-168">На hello **конфигурации Nomadesk** щелкните **Настройка Nomadesk** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-168">On hello **Nomadesk Configuration** section, click **Configure Nomadesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1e7ac-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="1e7ac-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_configure.png) 

7. <span data-ttu-id="1e7ac-171">tooconfigure единого входа на **Nomadesk** стороны, необходимо загрузить hello toosend **сертификат**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Nomadesk поддержки](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="1e7ac-171">tooconfigure single sign-on on **Nomadesk** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Nomadesk support team](mailto:support@nomadesk.com).</span></span> <span data-ttu-id="1e7ac-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1e7ac-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1e7ac-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1e7ac-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1e7ac-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e7ac-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e7ac-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7ac-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e7ac-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1e7ac-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e7ac-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e7ac-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e7ac-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e7ac-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="1e7ac-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e7ac-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e7ac-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e7ac-188">а.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-188">a.</span></span> <span data-ttu-id="1e7ac-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e7ac-190">b.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-190">b.</span></span> <span data-ttu-id="1e7ac-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e7ac-192">c.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-192">c.</span></span> <span data-ttu-id="1e7ac-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1e7ac-194">d.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-194">d.</span></span> <span data-ttu-id="1e7ac-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-195">Click **Create**.</span></span>
 
### <a name="creating-a-nomadesk-test-user"></a><span data-ttu-id="1e7ac-196">Создание тестового пользователя Nomadesk</span><span class="sxs-lookup"><span data-stu-id="1e7ac-196">Creating a Nomadesk test user</span></span>

<span data-ttu-id="1e7ac-197">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-197">hello objective of this section is toocreate a user called Britta Simon in Nomadesk.</span></span> <span data-ttu-id="1e7ac-198">Приложение Nomadesk поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-198">Nomadesk supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1e7ac-199">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-199">There is no action item for you in this section.</span></span> <span data-ttu-id="1e7ac-200">Новый пользователь создается во время попытки tooaccess Nomadesk, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-200">A new user is created during an attempt tooaccess Nomadesk if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1e7ac-201">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Nomadesk поддержки](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="1e7ac-201">If you need toocreate a user manually, you need toocontact hello [Nomadesk support team](mailto:support@nomadesk.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1e7ac-202">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1e7ac-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1e7ac-203">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNomadesk доступа.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNomadesk.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1e7ac-205">**tooassign tooNomadesk Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e7ac-205">**tooassign Britta Simon tooNomadesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e7ac-206">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1e7ac-208">В списке приложений hello выберите **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-208">In hello applications list, select **Nomadesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_app.png) 

3. <span data-ttu-id="1e7ac-210">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1e7ac-212">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-212">Click **Add** button.</span></span> <span data-ttu-id="1e7ac-213">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1e7ac-215">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1e7ac-216">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e7ac-217">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e7ac-218">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1e7ac-218">Testing single sign-on</span></span>

<span data-ttu-id="1e7ac-219">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1e7ac-220">При нажатии кнопки hello Nomadesk плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Nomadesk приложения.</span><span class="sxs-lookup"><span data-stu-id="1e7ac-220">When you click hello Nomadesk tile in hello Access Panel,  you should get automatically signed-on tooyour Nomadesk application.</span></span>
<span data-ttu-id="1e7ac-221">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e7ac-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e7ac-222">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1e7ac-222">Additional resources</span></span>

* [<span data-ttu-id="1e7ac-223">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e7ac-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e7ac-224">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e7ac-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_203.png

