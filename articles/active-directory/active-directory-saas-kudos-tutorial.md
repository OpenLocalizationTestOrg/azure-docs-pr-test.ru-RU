---
title: "Учебник. Интеграция Azure Active Directory с Kudos | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="4f079-103">Руководство. Интеграция Azure Active Directory с Kudos</span><span class="sxs-lookup"><span data-stu-id="4f079-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="4f079-104">В этом учебнике вы узнаете, как toointegrate Kudos с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4f079-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f079-105">Интеграция Kudos с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4f079-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4f079-106">Можно управлять в Azure AD, имеющего доступ tooKudos</span><span class="sxs-lookup"><span data-stu-id="4f079-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="4f079-107">Можно включить на пользователей tooautomatically get вошедшего tooKudos (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f079-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f079-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4f079-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4f079-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f079-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f079-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4f079-110">Prerequisites</span></span>

<span data-ttu-id="4f079-111">tooconfigure интеграция Azure AD с Kudos требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4f079-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="4f079-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4f079-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f079-113">подписка Kudos с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4f079-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f079-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4f079-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f079-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="4f079-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f079-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4f079-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f079-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f079-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f079-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4f079-118">Scenario description</span></span>
<span data-ttu-id="4f079-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4f079-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f079-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="4f079-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f079-121">Добавление Kudos из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4f079-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="4f079-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f079-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="4f079-123">Добавление Kudos из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4f079-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="4f079-124">tooconfigure hello интеграции Kudos в Azure AD, вы должны tooadd Kudos из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4f079-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4f079-125">**tooadd Kudos из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4f079-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f079-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4f079-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f079-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="4f079-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4f079-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4f079-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4f079-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4f079-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4f079-133">Введите в поле поиска hello **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="4f079-133">In hello search box, type **Kudos**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="4f079-135">В панели результатов hello выберите **Kudos**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4f079-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f079-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f079-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f079-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kudos для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f079-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4f079-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Kudos является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f079-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="4f079-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Kudos должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="4f079-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="4f079-141">В Kudos, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="4f079-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4f079-142">tooconfigure и теста Azure AD единого входа с Kudos, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4f079-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4f079-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="4f079-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4f079-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="4f079-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f079-145">**[Создание тестового пользователя Kudos](#creating-a-kudos-test-user)**  -toohave аналог Саймон Britta в Kudos, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f079-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f079-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="4f079-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f079-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4f079-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f079-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f079-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f079-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Kudos.</span><span class="sxs-lookup"><span data-stu-id="4f079-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="4f079-150">**Azure AD tooconfigure единого входа с Kudos, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4f079-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f079-151">В hello в hello портала Azure **Kudos** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4f079-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4f079-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="4f079-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="4f079-155">На hello **URL-адреса и домена Kudos** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4f079-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="4f079-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="4f079-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4f079-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="4f079-158">This value is not real.</span></span> <span data-ttu-id="4f079-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="4f079-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4f079-160">Обратитесь к [группа поддержки клиента Kudos](http://success.kudosnow.com/home) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="4f079-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="4f079-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4f079-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="4f079-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4f079-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4f079-165">На hello **конфигурации Kudos** щелкните **Настройка Kudos** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="4f079-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4f079-166">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="4f079-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="4f079-168">В другом окне веб-браузера войдите на ваш корпоративный веб-сайт Kudos в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="4f079-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="4f079-169">В меню в верхней части hello hello выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="4f079-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="4f079-170">![Параметры](./media/active-directory-saas-kudos-tutorial/ic787806.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="4f079-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="4f079-171">Выберите пункты **Integrations \> SSO** (Интеграции > Единый вход).</span><span class="sxs-lookup"><span data-stu-id="4f079-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="4f079-172">В hello **SSO** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4f079-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4f079-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="4f079-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="4f079-174">а.</span><span class="sxs-lookup"><span data-stu-id="4f079-174">a.</span></span> <span data-ttu-id="4f079-175">В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4f079-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4f079-176">b.</span><span class="sxs-lookup"><span data-stu-id="4f079-176">b.</span></span> <span data-ttu-id="4f079-177">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля</span><span class="sxs-lookup"><span data-stu-id="4f079-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="4f079-178">c.</span><span class="sxs-lookup"><span data-stu-id="4f079-178">c.</span></span> <span data-ttu-id="4f079-179">В **tooURL выхода**, вставьте значение hello **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4f079-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="4f079-180">d.</span><span class="sxs-lookup"><span data-stu-id="4f079-180">d.</span></span> <span data-ttu-id="4f079-181">В hello **URL-адрес Kudos** текстовом поле введите название вашей компании.</span><span class="sxs-lookup"><span data-stu-id="4f079-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="4f079-182">д.</span><span class="sxs-lookup"><span data-stu-id="4f079-182">e.</span></span> <span data-ttu-id="4f079-183">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4f079-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4f079-184">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="4f079-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4f079-185">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="4f079-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4f079-186">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f079-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f079-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f079-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f079-188">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4f079-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4f079-190">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4f079-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f079-191">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4f079-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f079-193">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4f079-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f079-195">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="4f079-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f079-197">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4f079-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f079-199">а.</span><span class="sxs-lookup"><span data-stu-id="4f079-199">a.</span></span> <span data-ttu-id="4f079-200">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f079-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f079-201">b.</span><span class="sxs-lookup"><span data-stu-id="4f079-201">b.</span></span> <span data-ttu-id="4f079-202">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4f079-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f079-203">c.</span><span class="sxs-lookup"><span data-stu-id="4f079-203">c.</span></span> <span data-ttu-id="4f079-204">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="4f079-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4f079-205">d.</span><span class="sxs-lookup"><span data-stu-id="4f079-205">d.</span></span> <span data-ttu-id="4f079-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4f079-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="4f079-207">Создание тестового пользователя Kudos</span><span class="sxs-lookup"><span data-stu-id="4f079-207">Creating a Kudos test user</span></span>

<span data-ttu-id="4f079-208">В порядке tooenable toolog пользователей Azure AD в Kudos их необходимо подготовить в Kudos.</span><span class="sxs-lookup"><span data-stu-id="4f079-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="4f079-209">В случае hello объекта Kudos Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="4f079-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="4f079-210">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4f079-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f079-211">Войдите в tooyour **Kudos** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="4f079-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="4f079-212">В меню в верхней части hello hello выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="4f079-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="4f079-213">![Параметры](./media/active-directory-saas-kudos-tutorial/ic787806.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="4f079-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="4f079-214">Выберите **Администратор пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4f079-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="4f079-215">Нажмите кнопку hello **пользователей** , а затем щелкните **Добавление пользователя**.</span><span class="sxs-lookup"><span data-stu-id="4f079-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="4f079-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin") (Администратор пользователей)</span><span class="sxs-lookup"><span data-stu-id="4f079-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="4f079-217">В hello **Добавление пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4f079-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4f079-218">![Добавление пользователя](./media/active-directory-saas-kudos-tutorial/ic787810.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="4f079-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="4f079-219">а.</span><span class="sxs-lookup"><span data-stu-id="4f079-219">a.</span></span> <span data-ttu-id="4f079-220">Тип hello **имя**, **Фамилия**, **электронной почты** и другие сведения о действительной учетной записи Azure Active Directory, которые должны tooprovision hello связаны текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="4f079-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="4f079-221">b.</span><span class="sxs-lookup"><span data-stu-id="4f079-221">b.</span></span> <span data-ttu-id="4f079-222">Нажмите кнопку **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="4f079-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="4f079-223">Можно использовать любые другие Kudos пользователя средства создания учетных записей или интерфейсы API, предоставляемые Kudos tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="4f079-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4f079-224">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="4f079-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4f079-225">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooKudos доступа.</span><span class="sxs-lookup"><span data-stu-id="4f079-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4f079-227">**tooassign tooKudos Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4f079-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f079-228">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4f079-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4f079-230">В списке приложений hello выберите **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="4f079-230">In hello applications list, select **Kudos**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="4f079-232">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="4f079-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4f079-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4f079-234">Click **Add** button.</span></span> <span data-ttu-id="4f079-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4f079-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4f079-237">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="4f079-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4f079-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4f079-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f079-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4f079-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f079-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4f079-240">Testing single sign-on</span></span>

<span data-ttu-id="4f079-241">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="4f079-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4f079-242">При нажатии кнопки hello Kudos плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Kudos приложения.</span><span class="sxs-lookup"><span data-stu-id="4f079-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="4f079-243">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f079-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f079-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4f079-244">Additional resources</span></span>

* [<span data-ttu-id="4f079-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f079-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f079-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4f079-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

