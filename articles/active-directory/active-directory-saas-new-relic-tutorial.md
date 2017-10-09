---
title: "Руководство по интеграции Azure Active Directory с New Relic | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="6addc-103">Учебник. Интеграция Azure Active Directory с New Relic</span><span class="sxs-lookup"><span data-stu-id="6addc-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="6addc-104">В этом учебнике вы узнаете, как toointegrate New Relic с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6addc-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6addc-105">Интеграция New Relic с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="6addc-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6addc-106">Можно управлять в Azure AD, имеющего доступ tooNew Relic</span><span class="sxs-lookup"><span data-stu-id="6addc-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="6addc-107">Можно включить на пользователей tooautomatically get вошедшего tooNew Relic (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="6addc-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6addc-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="6addc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6addc-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6addc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6addc-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6addc-110">Prerequisites</span></span>

<span data-ttu-id="6addc-111">tooconfigure интеграция Azure AD с New Relic, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="6addc-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="6addc-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6addc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6addc-113">Подписка с поддержкой единого входа New Relic.</span><span class="sxs-lookup"><span data-stu-id="6addc-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6addc-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6addc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6addc-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="6addc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6addc-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6addc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6addc-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6addc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6addc-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6addc-118">Scenario description</span></span>
<span data-ttu-id="6addc-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6addc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6addc-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="6addc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6addc-121">Добавление New Relic из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6addc-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="6addc-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6addc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="6addc-123">Добавление New Relic из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6addc-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="6addc-124">tooconfigure hello интеграции New Relic в Azure AD, вы должны tooadd New Relic из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6addc-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6addc-125">**tooadd New Relic из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6addc-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6addc-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="6addc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6addc-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="6addc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6addc-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6addc-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="6addc-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6addc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="6addc-133">Введите в поле поиска hello **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="6addc-133">In hello search box, type **New Relic**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="6addc-135">В панели результатов hello выберите **New Relic**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6addc-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6addc-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6addc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6addc-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение New Relic с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6addc-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6addc-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в New Relic является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6addc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="6addc-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в New Relic должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="6addc-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="6addc-141">В New Relic, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="6addc-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6addc-142">tooconfigure и теста Azure AD единого входа с New Relic, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6addc-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6addc-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="6addc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6addc-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="6addc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6addc-145">**[Создание тестового пользователя New Relic](#creating-a-new-relic-test-user)**  -toohave аналог Саймон Britta в New Relic, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="6addc-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6addc-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="6addc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6addc-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6addc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6addc-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6addc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6addc-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение New Relic.</span><span class="sxs-lookup"><span data-stu-id="6addc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="6addc-150">**tooconfigure Azure AD единого входа с New Relic, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6addc-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="6addc-151">В hello в hello портала Azure **New Relic** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="6addc-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="6addc-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="6addc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="6addc-155">На hello **URL-адреса и нового домена Relic** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6addc-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="6addc-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="6addc-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6addc-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="6addc-158">hello value is not real.</span></span> <span data-ttu-id="6addc-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="6addc-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6addc-160">Обратитесь к [группа поддержки нового клиента Relic](https://support.newrelic.com/) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="6addc-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="6addc-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="6addc-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="6addc-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6addc-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6addc-165">На hello **новую конфигурацию Relic** щелкните **Настройка New Relic** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="6addc-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6addc-166">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="6addc-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="6addc-168">В другом окне браузера, войдите на tooyour **New Relic** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="6addc-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="6addc-169">В меню в верхней части hello hello выберите **параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="6addc-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="6addc-170">![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797036.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="6addc-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="6addc-171">Нажмите кнопку hello **безопасности и проверки подлинности** , а затем щелкните hello **единого входа** вкладки.</span><span class="sxs-lookup"><span data-stu-id="6addc-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="6addc-172">![Единый вход](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="6addc-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="6addc-173">На странице диалогового окна SAML hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="6addc-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="6addc-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="6addc-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="6addc-175">а.</span><span class="sxs-lookup"><span data-stu-id="6addc-175">a.</span></span> <span data-ttu-id="6addc-176">Нажмите кнопку **выбрать файл** tooupload Скачанный сертификат Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6addc-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="6addc-177">b.</span><span class="sxs-lookup"><span data-stu-id="6addc-177">b.</span></span> <span data-ttu-id="6addc-178">В hello **URL-адрес удаленного входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="6addc-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="6addc-179">c.</span><span class="sxs-lookup"><span data-stu-id="6addc-179">c.</span></span> <span data-ttu-id="6addc-180">В hello **целевой URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="6addc-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="6addc-181">d.</span><span class="sxs-lookup"><span data-stu-id="6addc-181">d.</span></span> <span data-ttu-id="6addc-182">Щелкните **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="6addc-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6addc-183">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="6addc-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6addc-184">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="6addc-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6addc-185">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6addc-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6addc-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6addc-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="6addc-187">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6addc-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="6addc-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6addc-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6addc-190">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="6addc-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6addc-192">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6addc-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6addc-194">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="6addc-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6addc-196">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6addc-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6addc-198">а.</span><span class="sxs-lookup"><span data-stu-id="6addc-198">a.</span></span> <span data-ttu-id="6addc-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6addc-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6addc-200">b.</span><span class="sxs-lookup"><span data-stu-id="6addc-200">b.</span></span> <span data-ttu-id="6addc-201">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6addc-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6addc-202">c.</span><span class="sxs-lookup"><span data-stu-id="6addc-202">c.</span></span> <span data-ttu-id="6addc-203">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="6addc-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6addc-204">d.</span><span class="sxs-lookup"><span data-stu-id="6addc-204">d.</span></span> <span data-ttu-id="6addc-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6addc-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="6addc-206">Создание тестового пользователя New Relic</span><span class="sxs-lookup"><span data-stu-id="6addc-206">Creating a New Relic test user</span></span>

<span data-ttu-id="6addc-207">В порядке tooenable toolog пользователей Azure Active Directory в tooNew Relic их необходимо подготовить в New Relic.</span><span class="sxs-lookup"><span data-stu-id="6addc-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="6addc-208">В случае hello объекта New Relic Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="6addc-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="6addc-209">**tooprovision tooNew учетной записи пользователя Relic, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6addc-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="6addc-210">Войдите в tooyour **New Relic** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="6addc-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="6addc-211">В меню в верхней части hello hello выберите **параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="6addc-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="6addc-212">![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797040.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="6addc-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="6addc-213">В hello **учетной записи** на hello панели слева, нажмите кнопку **Сводка**, а затем нажмите кнопку **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="6addc-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="6addc-214">![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797041.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="6addc-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="6addc-215">На hello **активных пользователей** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6addc-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="6addc-216">![Активные пользователи](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Активные пользователи")</span><span class="sxs-lookup"><span data-stu-id="6addc-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="6addc-217">а.</span><span class="sxs-lookup"><span data-stu-id="6addc-217">a.</span></span> <span data-ttu-id="6addc-218">В hello **электронной почты** текстового поля, типа hello адрес электронной почты действительного пользователя Azure Active Directory требуется tooprovision.</span><span class="sxs-lookup"><span data-stu-id="6addc-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="6addc-219">b.</span><span class="sxs-lookup"><span data-stu-id="6addc-219">b.</span></span> <span data-ttu-id="6addc-220">Для параметра **Role** (Роль) выберите значение **User** (Пользователь).</span><span class="sxs-lookup"><span data-stu-id="6addc-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="6addc-221">c.</span><span class="sxs-lookup"><span data-stu-id="6addc-221">c.</span></span> <span data-ttu-id="6addc-222">Щелкните **Добавить этого пользователя**.</span><span class="sxs-lookup"><span data-stu-id="6addc-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="6addc-223">Можно использовать любые другие New Relic пользователя средства создания учетных записей или интерфейсы API, предоставляемые New Relic tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="6addc-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6addc-224">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="6addc-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6addc-225">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooNew Relic.</span><span class="sxs-lookup"><span data-stu-id="6addc-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="6addc-227">**tooassign Britta Simon tooNew Relic, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6addc-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="6addc-228">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6addc-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="6addc-230">В списке приложений hello выберите **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="6addc-230">In hello applications list, select **New Relic**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="6addc-232">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="6addc-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="6addc-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6addc-234">Click **Add** button.</span></span> <span data-ttu-id="6addc-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6addc-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="6addc-237">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="6addc-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6addc-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6addc-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6addc-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="6addc-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6addc-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6addc-240">Testing single sign-on</span></span>

<span data-ttu-id="6addc-241">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="6addc-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6addc-242">При нажатии кнопки hello New Relic плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour New Relic.</span><span class="sxs-lookup"><span data-stu-id="6addc-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6addc-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6addc-243">Additional resources</span></span>

* [<span data-ttu-id="6addc-244">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6addc-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6addc-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6addc-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

