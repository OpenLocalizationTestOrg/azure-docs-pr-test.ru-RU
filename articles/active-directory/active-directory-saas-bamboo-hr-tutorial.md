---
title: "Руководство по интеграции Azure Active Directory с BambooHR | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="65ab2-103">Руководство по интеграции Azure Active Directory с BambooHR</span><span class="sxs-lookup"><span data-stu-id="65ab2-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="65ab2-104">В этом учебнике вы узнаете, как toointegrate BambooHR с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65ab2-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65ab2-105">Интеграция BambooHR с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="65ab2-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65ab2-106">Можно управлять в Azure AD, имеющего доступ tooBambooHR</span><span class="sxs-lookup"><span data-stu-id="65ab2-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="65ab2-107">Можно включить на пользователей tooautomatically get вошедшего tooBambooHR (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="65ab2-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65ab2-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="65ab2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="65ab2-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65ab2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65ab2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="65ab2-110">Prerequisites</span></span>

<span data-ttu-id="65ab2-111">tooconfigure интеграция Azure AD с BambooHR требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="65ab2-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="65ab2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="65ab2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65ab2-113">подписка BambooHR с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="65ab2-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65ab2-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="65ab2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65ab2-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="65ab2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65ab2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="65ab2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65ab2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65ab2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65ab2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="65ab2-118">Scenario description</span></span>
<span data-ttu-id="65ab2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="65ab2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65ab2-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="65ab2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65ab2-121">Добавление BambooHR из галереи hello</span><span class="sxs-lookup"><span data-stu-id="65ab2-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="65ab2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="65ab2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="65ab2-123">Добавление BambooHR из галереи hello</span><span class="sxs-lookup"><span data-stu-id="65ab2-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="65ab2-124">tooconfigure hello интеграции BambooHR в Azure AD, вы должны tooadd BambooHR из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="65ab2-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65ab2-125">**tooadd BambooHR из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="65ab2-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ab2-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="65ab2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65ab2-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65ab2-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="65ab2-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="65ab2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="65ab2-133">Введите в поле поиска hello **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-133">In hello search box, type **BambooHR**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="65ab2-135">В панели результатов hello выберите **BambooHR**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="65ab2-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65ab2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="65ab2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65ab2-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение BambooHR с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65ab2-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65ab2-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BambooHR является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65ab2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="65ab2-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в BambooHR должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="65ab2-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="65ab2-141">В BambooHR, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="65ab2-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65ab2-142">tooconfigure и теста Azure AD единого входа с BambooHR, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="65ab2-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65ab2-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="65ab2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65ab2-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="65ab2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65ab2-145">**[Создание тестового пользователя BambooHR](#creating-a-bamboohr-test-user)**  -toohave аналог Саймон Britta в BambooHR, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="65ab2-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65ab2-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="65ab2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65ab2-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="65ab2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65ab2-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="65ab2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65ab2-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в ваше приложение BambooHR.</span><span class="sxs-lookup"><span data-stu-id="65ab2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="65ab2-150">**tooconfigure Azure AD единого входа с BambooHR, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="65ab2-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ab2-151">В hello в hello портала Azure **BambooHR** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="65ab2-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="65ab2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="65ab2-155">На hello **URL-адреса и домена BambooHR** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="65ab2-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="65ab2-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="65ab2-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="65ab2-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="65ab2-158">This value is not real.</span></span> <span data-ttu-id="65ab2-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="65ab2-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="65ab2-160">Обратитесь к [группа поддержки клиента BambooHR](https://www.bamboohr.com/contact.php) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="65ab2-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="65ab2-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="65ab2-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="65ab2-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="65ab2-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65ab2-165">На hello **конфигурации BambooHR** щелкните **Настройка BambooHR** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="65ab2-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="65ab2-166">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="65ab2-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="65ab2-168">В другом окне веб-браузера войдите на свой корпоративный веб-сайт BambooHR в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="65ab2-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="65ab2-169">На домашнюю страницу приветствия выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="65ab2-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="65ab2-170">![Единый вход](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="65ab2-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="65ab2-171">а.</span><span class="sxs-lookup"><span data-stu-id="65ab2-171">a.</span></span> <span data-ttu-id="65ab2-172">Нажмите **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="65ab2-173">b.</span><span class="sxs-lookup"><span data-stu-id="65ab2-173">b.</span></span> <span data-ttu-id="65ab2-174">В меню приложения hello слева hello, щелкните **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="65ab2-175">c.</span><span class="sxs-lookup"><span data-stu-id="65ab2-175">c.</span></span> <span data-ttu-id="65ab2-176">Нажмите **Единый вход SAML**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="65ab2-177">В hello **SAML Single Sign-On** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="65ab2-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="65ab2-178">![Единый вход SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Единый вход SAML")</span><span class="sxs-lookup"><span data-stu-id="65ab2-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="65ab2-179">а.</span><span class="sxs-lookup"><span data-stu-id="65ab2-179">a.</span></span> <span data-ttu-id="65ab2-180">Вставить hello **SAML единого входа URL-адрес службы** значение в hello **URL-адрес входа SSO** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="65ab2-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="65ab2-181">b.</span><span class="sxs-lookup"><span data-stu-id="65ab2-181">b.</span></span> <span data-ttu-id="65ab2-182">Откройте сертификат в кодировке base-64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля</span><span class="sxs-lookup"><span data-stu-id="65ab2-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="65ab2-183">c.</span><span class="sxs-lookup"><span data-stu-id="65ab2-183">c.</span></span> <span data-ttu-id="65ab2-184">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="65ab2-185">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="65ab2-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65ab2-186">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="65ab2-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65ab2-187">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65ab2-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65ab2-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="65ab2-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="65ab2-189">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="65ab2-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="65ab2-191">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="65ab2-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ab2-192">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="65ab2-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65ab2-194">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65ab2-196">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="65ab2-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65ab2-198">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="65ab2-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65ab2-200">а.</span><span class="sxs-lookup"><span data-stu-id="65ab2-200">a.</span></span> <span data-ttu-id="65ab2-201">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65ab2-202">b.</span><span class="sxs-lookup"><span data-stu-id="65ab2-202">b.</span></span> <span data-ttu-id="65ab2-203">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65ab2-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65ab2-204">c.</span><span class="sxs-lookup"><span data-stu-id="65ab2-204">c.</span></span> <span data-ttu-id="65ab2-205">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="65ab2-206">d.</span><span class="sxs-lookup"><span data-stu-id="65ab2-206">d.</span></span> <span data-ttu-id="65ab2-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="65ab2-208">Создание тестового пользователя BambooHR</span><span class="sxs-lookup"><span data-stu-id="65ab2-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="65ab2-209">Пользователи toolog tooenable Azure AD в tooBambooHR, их необходимо подготовить в BambooHR.</span><span class="sxs-lookup"><span data-stu-id="65ab2-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="65ab2-210">В случае hello BambooHR Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="65ab2-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="65ab2-211">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="65ab2-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ab2-212">Войдите в tooyour **BambooHR** сайта от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="65ab2-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="65ab2-213">Щелкните hello панели инструментов в верхней части hello **параметры**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="65ab2-214">![Параметр](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Параметр")</span><span class="sxs-lookup"><span data-stu-id="65ab2-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="65ab2-215">Нажмите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-215">Click **Overview**.</span></span>

4. <span data-ttu-id="65ab2-216">В области навигации слева hello, переходите слишком**безопасности \> пользователей**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="65ab2-217">Введите имя пользователя hello, пароль и адрес электронной почты действительной учетной записи AAD, требуется tooprovision в hello связанные текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="65ab2-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="65ab2-218">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="65ab2-219">Можно использовать любые другие BambooHR пользователя средства создания учетных записей или интерфейсы API, предоставляемые BambooHR tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="65ab2-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="65ab2-220">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="65ab2-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="65ab2-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBambooHR доступа.</span><span class="sxs-lookup"><span data-stu-id="65ab2-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="65ab2-223">**tooassign tooBambooHR Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="65ab2-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ab2-224">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="65ab2-226">В списке приложений hello выберите **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-226">In hello applications list, select **BambooHR**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="65ab2-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="65ab2-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-230">Click **Add** button.</span></span> <span data-ttu-id="65ab2-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="65ab2-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="65ab2-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65ab2-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65ab2-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="65ab2-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65ab2-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="65ab2-236">Testing single sign-on</span></span>

<span data-ttu-id="65ab2-237">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="65ab2-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="65ab2-238">При нажатии кнопки hello BambooHR плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour BambooHR.</span><span class="sxs-lookup"><span data-stu-id="65ab2-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="65ab2-239">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65ab2-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="65ab2-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="65ab2-240">Additional resources</span></span>

* [<span data-ttu-id="65ab2-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65ab2-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65ab2-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65ab2-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

