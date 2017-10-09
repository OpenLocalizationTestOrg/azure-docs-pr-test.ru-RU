---
title: "Руководство по интеграции Azure Active Directory с Nexonia | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 3778804084a7989414260bae5654cf76e9ccca6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="f878c-103">Руководство по интеграции Azure Active Directory с Nexonia</span><span class="sxs-lookup"><span data-stu-id="f878c-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="f878c-104">В этом учебнике вы узнаете, как toointegrate Nexonia с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f878c-104">In this tutorial, you learn how toointegrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f878c-105">Интеграция с Azure AD Nexonia предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f878c-105">Integrating Nexonia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f878c-106">Можно управлять в Azure AD, имеющего доступ tooNexonia</span><span class="sxs-lookup"><span data-stu-id="f878c-106">You can control in Azure AD who has access tooNexonia</span></span>
- <span data-ttu-id="f878c-107">Можно включить на пользователей tooautomatically get вошедшего tooNexonia (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f878c-107">You can enable your users tooautomatically get signed-on tooNexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f878c-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f878c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f878c-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f878c-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="f878c-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f878c-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f878c-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f878c-111">Prerequisites</span></span>

<span data-ttu-id="f878c-112">tooconfigure интеграция Azure AD с Nexonia требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f878c-112">tooconfigure Azure AD integration with Nexonia, you need hello following items:</span></span>

- <span data-ttu-id="f878c-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f878c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="f878c-114">подписка на Nexonia с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f878c-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f878c-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f878c-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f878c-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f878c-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f878c-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f878c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f878c-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f878c-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f878c-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f878c-119">Scenario description</span></span>
<span data-ttu-id="f878c-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f878c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f878c-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f878c-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f878c-122">Добавление Nexonia из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f878c-122">Adding Nexonia from hello gallery</span></span>
2. <span data-ttu-id="f878c-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f878c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-hello-gallery"></a><span data-ttu-id="f878c-124">Добавление Nexonia из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f878c-124">Adding Nexonia from hello gallery</span></span>
<span data-ttu-id="f878c-125">tooconfigure hello интеграции Nexonia в Azure AD, вы должны tooadd Nexonia из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f878c-125">tooconfigure hello integration of Nexonia into Azure AD, you need tooadd Nexonia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f878c-126">**tooadd Nexonia из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f878c-126">**tooadd Nexonia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f878c-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f878c-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f878c-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f878c-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f878c-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f878c-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f878c-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f878c-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f878c-134">Введите в поле поиска hello **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="f878c-134">In hello search box, type **Nexonia**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="f878c-136">В панели результатов hello выберите **Nexonia**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f878c-136">In hello results panel, select **Nexonia**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f878c-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f878c-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f878c-139">В этом разделе описана настройка и проверка единого входа Azure AD в Nexonia с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f878c-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f878c-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Nexonia является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f878c-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nexonia is tooa user in Azure AD.</span></span> <span data-ttu-id="f878c-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Nexonia должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f878c-141">In other words, a link relationship between an Azure AD user and hello related user in Nexonia needs toobe established.</span></span>

<span data-ttu-id="f878c-142">В Nexonia, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f878c-142">In Nexonia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f878c-143">tooconfigure и теста Azure AD единого входа с Nexonia, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f878c-143">tooconfigure and test Azure AD single sign-on with Nexonia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f878c-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f878c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f878c-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f878c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f878c-146">**[Создание тестового пользователя Nexonia](#creating-a-nexonia-test-user)**  -toohave аналог Саймон Britta в Nexonia, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f878c-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - toohave a counterpart of Britta Simon in Nexonia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f878c-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f878c-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f878c-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f878c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f878c-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f878c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f878c-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Nexonia.</span><span class="sxs-lookup"><span data-stu-id="f878c-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="f878c-151">Если возникают проблемы при интеграции hello, то это ссылаться [ссылку](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) для руководство по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="f878c-151">If you have issues in hello integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="f878c-152">Если по-прежнему отсутствуют решения hello, затем создается запрос на получение поддержки hello из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="f878c-152">If you still have not found hello solution, then raise hello support request from Azure portal.</span></span>

<span data-ttu-id="f878c-153">**tooconfigure Azure AD единого входа с Nexonia, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f878c-153">**tooconfigure Azure AD single sign-on with Nexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="f878c-154">В hello в hello портала Azure **Nexonia** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f878c-154">In hello Azure portal, on hello **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f878c-156">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f878c-156">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="f878c-158">На hello **URL-адреса и домена Nexonia** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f878c-158">On hello **Nexonia Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="f878c-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="f878c-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f878c-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="f878c-161">This value is not real.</span></span> <span data-ttu-id="f878c-162">Измените значение этого параметра hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="f878c-162">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="f878c-163">Обратитесь к [Nexonia поддержки](https://nexonia.zendesk.com/hc/requests/new) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="f878c-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooget this value.</span></span> 


4. <span data-ttu-id="f878c-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f878c-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="f878c-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f878c-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f878c-168">На hello **конфигурации Nexonia** щелкните **Настройка Nexonia** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="f878c-168">On hello **Nexonia Configuration** section, click **Configure Nexonia** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f878c-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="f878c-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="f878c-171">tooget SSO настроен для вашего приложения, обратитесь в службу [Nexonia поддержки](https://nexonia.zendesk.com/hc/requests/new) и предоставить им hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f878c-171">tooget SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with hello following:</span></span>

    <span data-ttu-id="f878c-172">• hello загружены **сертификата**</span><span class="sxs-lookup"><span data-stu-id="f878c-172">• hello downloaded **certificate**</span></span>

    <span data-ttu-id="f878c-173">• hello **SAML идентификатор сущности**</span><span class="sxs-lookup"><span data-stu-id="f878c-173">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="f878c-174">• hello **SAML единого входа URL-адрес службы**</span><span class="sxs-lookup"><span data-stu-id="f878c-174">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="f878c-175">• hello **URL-адрес выхода**</span><span class="sxs-lookup"><span data-stu-id="f878c-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="f878c-176">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f878c-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f878c-177">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f878c-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f878c-178">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f878c-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f878c-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f878c-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="f878c-180">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f878c-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f878c-182">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f878c-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f878c-183">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f878c-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f878c-185">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f878c-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f878c-187">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f878c-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f878c-189">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f878c-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f878c-191">а.</span><span class="sxs-lookup"><span data-stu-id="f878c-191">a.</span></span> <span data-ttu-id="f878c-192">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f878c-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f878c-193">b.</span><span class="sxs-lookup"><span data-stu-id="f878c-193">b.</span></span> <span data-ttu-id="f878c-194">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f878c-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f878c-195">c.</span><span class="sxs-lookup"><span data-stu-id="f878c-195">c.</span></span> <span data-ttu-id="f878c-196">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f878c-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f878c-197">d.</span><span class="sxs-lookup"><span data-stu-id="f878c-197">d.</span></span> <span data-ttu-id="f878c-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f878c-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="f878c-199">Создание тестового пользователя Nexonia</span><span class="sxs-lookup"><span data-stu-id="f878c-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="f878c-200">В этом разделе описано, как создать пользователя Britta Simon в приложении Nexonia.</span><span class="sxs-lookup"><span data-stu-id="f878c-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="f878c-201">Работать с [Nexonia поддержки](https://nexonia.zendesk.com/hc/requests/new) tooadd hello пользователей на платформе Nexonia hello.</span><span class="sxs-lookup"><span data-stu-id="f878c-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooadd hello users in hello Nexonia platform.</span></span> <span data-ttu-id="f878c-202">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="f878c-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f878c-203">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f878c-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f878c-204">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNexonia доступа.</span><span class="sxs-lookup"><span data-stu-id="f878c-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNexonia.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f878c-206">**tooassign tooNexonia Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f878c-206">**tooassign Britta Simon tooNexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="f878c-207">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f878c-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f878c-209">В списке приложений hello выберите **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="f878c-209">In hello applications list, select **Nexonia**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="f878c-211">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f878c-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f878c-213">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f878c-213">Click **Add** button.</span></span> <span data-ttu-id="f878c-214">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f878c-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f878c-216">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f878c-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f878c-217">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f878c-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f878c-218">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f878c-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f878c-219">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f878c-219">Testing single sign-on</span></span>

<span data-ttu-id="f878c-220">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f878c-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f878c-221">При нажатии кнопки hello Nexonia плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Nexonia приложения.</span><span class="sxs-lookup"><span data-stu-id="f878c-221">When you click hello Nexonia tile in hello Access Panel, you should get automatically signed-on tooyour Nexonia application.</span></span>
<span data-ttu-id="f878c-222">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f878c-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f878c-223">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f878c-223">Additional resources</span></span>

* [<span data-ttu-id="f878c-224">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f878c-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f878c-225">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f878c-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

