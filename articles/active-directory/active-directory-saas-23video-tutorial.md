---
title: "Руководство по интеграции Azure Active Directory с платформой 23 Video | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и 23 видео."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 3430e4db3cd1114db62233e6699618071a3646ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="d9db0-103">Руководство по интеграции Azure Active Directory с платформой 23 Video</span><span class="sxs-lookup"><span data-stu-id="d9db0-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="d9db0-104">В этом учебнике вы узнаете, как toointegrate 23 видео с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9db0-104">In this tutorial, you learn how toointegrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9db0-105">Интеграция 23 видео с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d9db0-105">Integrating 23 Video with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9db0-106">Можно управлять в Azure AD, который имеет доступ too23 видео</span><span class="sxs-lookup"><span data-stu-id="d9db0-106">You can control in Azure AD who has access too23 Video</span></span>
- <span data-ttu-id="d9db0-107">Позволяет пользователям получить tooautomatically вошедшего too23 видео (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9db0-107">You can enable your users tooautomatically get signed-on too23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9db0-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d9db0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9db0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9db0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9db0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d9db0-110">Prerequisites</span></span>

<span data-ttu-id="d9db0-111">tooconfigure интеграция Azure AD с 23 видео необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d9db0-111">tooconfigure Azure AD integration with 23 Video, you need hello following items:</span></span>

- <span data-ttu-id="d9db0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d9db0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9db0-113">подписка на 23 Video с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d9db0-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9db0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d9db0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9db0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d9db0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9db0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d9db0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9db0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9db0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9db0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d9db0-118">Scenario description</span></span>
<span data-ttu-id="d9db0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d9db0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9db0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d9db0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9db0-121">Добавление 23 видео из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d9db0-121">Adding 23 Video from hello gallery</span></span>
2. <span data-ttu-id="d9db0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9db0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-hello-gallery"></a><span data-ttu-id="d9db0-123">Добавление 23 видео из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d9db0-123">Adding 23 Video from hello gallery</span></span>
<span data-ttu-id="d9db0-124">tooconfigure hello интеграции 23 видео в Azure AD, необходимо tooadd 23 видео с hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d9db0-124">tooconfigure hello integration of 23 Video into Azure AD, you need tooadd 23 Video from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9db0-125">**выполнить видео из галереи hello tooadd 23 hello следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d9db0-125">**tooadd 23 Video from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9db0-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d9db0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9db0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9db0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d9db0-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d9db0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d9db0-133">Введите в поле поиска hello **23 видео**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-133">In hello search box, type **23 Video**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="d9db0-135">В панели результатов hello выберите **23 видео**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d9db0-135">In hello results panel, select **23 Video**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9db0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9db0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9db0-138">В этом разделе мы настроим и проверим единый вход Azure AD в приложении 23 Video с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9db0-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9db0-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в 23 видео является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9db0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 23 Video is tooa user in Azure AD.</span></span> <span data-ttu-id="d9db0-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в 23 видео должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d9db0-140">In other words, a link relationship between an Azure AD user and hello related user in 23 Video needs toobe established.</span></span>

<span data-ttu-id="d9db0-141">В видео, 23, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="d9db0-141">In 23 Video, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d9db0-142">tooconfigure и теста Azure AD единого входа с 23 видео, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d9db0-142">tooconfigure and test Azure AD single sign-on with 23 Video, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9db0-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d9db0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9db0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d9db0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9db0-145">**[Создание тестового пользователя 23 видео](#creating-a-23-video-test-user)**  -toohave аналог Саймон Britta в 23 видео, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="d9db0-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - toohave a counterpart of Britta Simon in 23 Video that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9db0-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d9db0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9db0-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d9db0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9db0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9db0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9db0-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении 23 видео.</span><span class="sxs-lookup"><span data-stu-id="d9db0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="d9db0-150">**tooconfigure Azure AD единого входа с видео, 23, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d9db0-150">**tooconfigure Azure AD single sign-on with 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9db0-151">В hello в hello портала Azure **23 видео** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-151">In hello Azure portal, on hello **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d9db0-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d9db0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="d9db0-155">На hello **23 URL-адреса и домена видео** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d9db0-155">On hello **23 Video Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="d9db0-157">а.</span><span class="sxs-lookup"><span data-stu-id="d9db0-157">a.</span></span> <span data-ttu-id="d9db0-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="d9db0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="d9db0-159">b.</span><span class="sxs-lookup"><span data-stu-id="d9db0-159">b.</span></span> <span data-ttu-id="d9db0-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="d9db0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9db0-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d9db0-161">These values are not real.</span></span> <span data-ttu-id="d9db0-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d9db0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d9db0-163">Обратитесь к [23 группа поддержки клиента видео](mailto:support@23company.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="d9db0-163">Contact [23 Video Client support team](mailto:support@23company.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="d9db0-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="d9db0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="d9db0-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d9db0-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9db0-168">На hello **23 конфигурации видео** щелкните **Настройка видео 23** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="d9db0-168">On hello **23 Video Configuration** section, click **Configure 23 Video** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d9db0-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="d9db0-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="d9db0-171">tooconfigure единого входа на **23 видео** стороны, необходимо загрузить hello toosend **сертификата (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы**слишком[23 группа поддержки видео](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="d9db0-171">tooconfigure single sign-on on **23 Video** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="d9db0-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="d9db0-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9db0-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="d9db0-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9db0-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9db0-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9db0-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9db0-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9db0-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d9db0-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d9db0-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d9db0-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9db0-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d9db0-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9db0-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9db0-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="d9db0-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9db0-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d9db0-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9db0-187">а.</span><span class="sxs-lookup"><span data-stu-id="d9db0-187">a.</span></span> <span data-ttu-id="d9db0-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9db0-189">b.</span><span class="sxs-lookup"><span data-stu-id="d9db0-189">b.</span></span> <span data-ttu-id="d9db0-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d9db0-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9db0-191">c.</span><span class="sxs-lookup"><span data-stu-id="d9db0-191">c.</span></span> <span data-ttu-id="d9db0-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9db0-193">d.</span><span class="sxs-lookup"><span data-stu-id="d9db0-193">d.</span></span> <span data-ttu-id="d9db0-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="d9db0-195">Создание тестового пользователя 23 Video</span><span class="sxs-lookup"><span data-stu-id="d9db0-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="d9db0-196">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в 23 видео.</span><span class="sxs-lookup"><span data-stu-id="d9db0-196">hello objective of this section is toocreate a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="d9db0-197">**toocreate пользователя с именем Britta Simon в видео, 23, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d9db0-197">**toocreate a user called Britta Simon in 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9db0-198">Войдите на tooyour 23 корпоративный сайт видео от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d9db0-198">Sign on tooyour 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="d9db0-199">Go слишком**параметры**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-199">Go too**Settings**.</span></span>
 
3. <span data-ttu-id="d9db0-200">В разделе **Users** (Пользователи) щелкните **Configure** (Настройка).</span><span class="sxs-lookup"><span data-stu-id="d9db0-200">In **Users** section, click **Configure**.</span></span>
   
    ![Назначение пользователя][400]

4. <span data-ttu-id="d9db0-202">Щелкните **Add a new user**(Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="d9db0-202">Click **Add a new user**.</span></span> 
   
    ![Назначение пользователя][401]

5. <span data-ttu-id="d9db0-204">В hello **пригласить пользователя toojoin этот сайт** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d9db0-204">In hello **Invite someone toojoin this site** section, perform hello following steps:</span></span>
   
    ![Назначение пользователя][402]

    <span data-ttu-id="d9db0-206">а.</span><span class="sxs-lookup"><span data-stu-id="d9db0-206">a.</span></span> <span data-ttu-id="d9db0-207">В hello **адреса электронной почты** текстовом поле введите адрес электронной почты Britta Simon в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9db0-207">In hello **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="d9db0-208">b.</span><span class="sxs-lookup"><span data-stu-id="d9db0-208">b.</span></span> <span data-ttu-id="d9db0-209">Нажмите кнопку **hello добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-209">Click **Add hello user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9db0-210">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d9db0-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9db0-211">В этом разделе включите Саймон Britta toouse Azure единого входа путем предоставления доступа к too23 видео.</span><span class="sxs-lookup"><span data-stu-id="d9db0-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too23 Video.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d9db0-213">**tooassign Britta Simon too23 видео, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d9db0-213">**tooassign Britta Simon too23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9db0-214">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d9db0-216">В списке приложений hello выберите **23 видео**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-216">In hello applications list, select **23 Video**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="d9db0-218">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d9db0-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-220">Click **Add** button.</span></span> <span data-ttu-id="d9db0-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d9db0-223">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d9db0-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9db0-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9db0-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d9db0-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9db0-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d9db0-226">Testing single sign-on</span></span>

<span data-ttu-id="d9db0-227">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="d9db0-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d9db0-228">При выборе плитки видео hello 23 hello панели доступа, вы должны получить приложение автоматически вошедшего tooyour 23 видео.</span><span class="sxs-lookup"><span data-stu-id="d9db0-228">When you click hello 23 Video tile in hello Access Panel, you should get automatically signed-on tooyour 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d9db0-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d9db0-229">Additional resources</span></span>

* [<span data-ttu-id="d9db0-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9db0-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9db0-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9db0-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
