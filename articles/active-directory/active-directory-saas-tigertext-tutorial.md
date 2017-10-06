---
title: "Руководство по интеграции Azure Active Directory с TigerText Secure Messenger | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и TigerText защиты сообщений."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="a8edf-103">Руководство по интеграции Azure Active Directory с TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="a8edf-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="a8edf-104">В этом учебнике вы узнаете, как toointegrate TigerText безопасность сообщений с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8edf-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8edf-105">Интеграция TigerText защита сообщений с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a8edf-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a8edf-106">Можно управлять в Azure AD, имеющего доступ tooTigerText безопасных сообщений</span><span class="sxs-lookup"><span data-stu-id="a8edf-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="a8edf-107">Можно включить на пользователей tooautomatically get вошедшего tooTigerText защиты сообщений (Single Sign-On), с их учетными записями Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8edf-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8edf-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a8edf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a8edf-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8edf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8edf-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8edf-110">Prerequisites</span></span>

<span data-ttu-id="a8edf-111">tooconfigure интеграция Azure AD с TigerText защиты сообщений требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a8edf-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="a8edf-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a8edf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8edf-113">подписка TigerText Secure Messenger с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a8edf-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8edf-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a8edf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8edf-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a8edf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8edf-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a8edf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8edf-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8edf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8edf-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a8edf-118">Scenario description</span></span>
<span data-ttu-id="a8edf-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a8edf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8edf-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a8edf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8edf-121">Добавление защиты Messenger TigerText из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a8edf-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="a8edf-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8edf-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="a8edf-123">Добавление защиты Messenger TigerText из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a8edf-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="a8edf-124">tooconfigure hello интеграции TigerText Secure Messenger в Azure AD, вы должны tooadd TigerText Secure Messenger из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a8edf-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a8edf-125">**tooadd TigerText Secure Messenger из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a8edf-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8edf-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a8edf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8edf-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a8edf-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a8edf-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a8edf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a8edf-133">Введите в поле поиска hello **TigerText Secure Messenger**выберите **TigerText Secure Messenger** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a8edf-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Добавление из коллекции](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a8edf-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8edf-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a8edf-136">В этом разделе описана настройка и проверка единого входа Azure AD в TigerText Secure Messenger с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8edf-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a8edf-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в TigerText Secure Messenger является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8edf-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="a8edf-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в TigerText Secure Messenger должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a8edf-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="a8edf-139">В программе Messenger Secure TigerText, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a8edf-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a8edf-140">tooconfigure и теста Azure AD единого входа с TigerText защиты сообщений, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a8edf-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a8edf-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a8edf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a8edf-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a8edf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8edf-143">**[Создание тестового пользователя TigerText Secure Messenger](#create-a-tigertext-secure-messenger-test-user)**  -toohave аналог Саймон Britta в TigerText Secure Messenger, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8edf-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8edf-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a8edf-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8edf-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a8edf-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a8edf-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8edf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a8edf-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении TigerText защиты сообщений.</span><span class="sxs-lookup"><span data-stu-id="a8edf-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="a8edf-148">**tooconfigure Azure AD единый вход в TigerText Secure Messenger выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a8edf-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8edf-149">В hello в hello портала Azure **TigerText Secure Messenger** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a8edf-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a8edf-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="a8edf-153">На hello **URL-адреса и домена Messenger Secure TigerText** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a8edf-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![Раздел "Домены и URL-адреса приложения TigerText Secure Messenger"](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="a8edf-155">а.</span><span class="sxs-lookup"><span data-stu-id="a8edf-155">a.</span></span> <span data-ttu-id="a8edf-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="a8edf-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="a8edf-157">b.</span><span class="sxs-lookup"><span data-stu-id="a8edf-157">b.</span></span> <span data-ttu-id="a8edf-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="a8edf-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a8edf-159">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a8edf-159">This value is not real.</span></span> <span data-ttu-id="a8edf-160">Измените значение этого параметра hello фактический идентификатор.</span><span class="sxs-lookup"><span data-stu-id="a8edf-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="a8edf-161">Обратитесь к [группы поддержки безопасного клиента TigerText](mailTo:prosupport@tigertext.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="a8edf-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="a8edf-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8edf-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="a8edf-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a8edf-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a8edf-166">tooget единый вход настроен для вашего приложения, обратитесь к [группы поддержки безопасного Messenger TigerText](mailTo:prosupport@tigertext.com) и сообщите hello **загрузки метаданных**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="a8edf-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a8edf-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a8edf-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a8edf-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a8edf-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a8edf-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a8edf-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8edf-170">Create an Azure AD test user</span></span>
<span data-ttu-id="a8edf-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a8edf-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a8edf-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a8edf-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8edf-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a8edf-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8edf-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Пользователи и группы" -> "Все пользователи"](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8edf-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a8edf-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8edf-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a8edf-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Диалоговое окно пользователя](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8edf-182">а.</span><span class="sxs-lookup"><span data-stu-id="a8edf-182">a.</span></span> <span data-ttu-id="a8edf-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8edf-184">b.</span><span class="sxs-lookup"><span data-stu-id="a8edf-184">b.</span></span> <span data-ttu-id="a8edf-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a8edf-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8edf-186">c.</span><span class="sxs-lookup"><span data-stu-id="a8edf-186">c.</span></span> <span data-ttu-id="a8edf-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a8edf-188">d.</span><span class="sxs-lookup"><span data-stu-id="a8edf-188">d.</span></span> <span data-ttu-id="a8edf-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="a8edf-190">Создание тестового пользователя TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="a8edf-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="a8edf-191">В этом разделе описано, как создать пользователя Britta Simon в приложении TigerText.</span><span class="sxs-lookup"><span data-stu-id="a8edf-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="a8edf-192">Проверьте направляться слишком[группы поддержки безопасного клиента TigerText](mailTo:prosupport@tigertext.com) tooadd hello пользователей на платформе TigerText hello.</span><span class="sxs-lookup"><span data-stu-id="a8edf-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a8edf-193">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a8edf-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a8edf-194">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooTigerText защиты сообщений.</span><span class="sxs-lookup"><span data-stu-id="a8edf-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a8edf-196">**tooassign tooTigerText Britta Simon Secure Messenger, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="a8edf-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8edf-197">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a8edf-199">В списке приложений hello выберите **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger в списке приложений](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="a8edf-201">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a8edf-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-203">Click **Add** button.</span></span> <span data-ttu-id="a8edf-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a8edf-206">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a8edf-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a8edf-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8edf-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a8edf-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a8edf-209">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a8edf-209">Test single sign-on</span></span>

<span data-ttu-id="a8edf-210">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a8edf-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a8edf-211">При нажатии кнопки hello TigerText плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour TigerText приложения.</span><span class="sxs-lookup"><span data-stu-id="a8edf-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="a8edf-212">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a8edf-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8edf-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a8edf-213">Additional resources</span></span>

* [<span data-ttu-id="a8edf-214">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8edf-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8edf-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a8edf-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

