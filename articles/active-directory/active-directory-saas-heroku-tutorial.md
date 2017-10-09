---
title: "Учебник. Интеграция Azure Active Directory с Heroku | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="8d0c9-103">Учебник. Интеграция Azure Active Directory с Heroku</span><span class="sxs-lookup"><span data-stu-id="8d0c9-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="8d0c9-104">В этом учебнике вы узнаете, как toointegrate Heroku с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d0c9-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d0c9-105">Интеграция с Azure AD Heroku предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d0c9-106">Можно управлять в Azure AD, имеющего доступ tooHeroku</span><span class="sxs-lookup"><span data-stu-id="8d0c9-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="8d0c9-107">Можно включить на пользователей tooautomatically get вошедшего tooHeroku (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d0c9-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d0c9-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8d0c9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d0c9-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d0c9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d0c9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d0c9-110">Prerequisites</span></span>

<span data-ttu-id="8d0c9-111">tooconfigure интеграция Azure AD с Heroku требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="8d0c9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8d0c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d0c9-113">подписка Heroku с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d0c9-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d0c9-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d0c9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d0c9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d0c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d0c9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8d0c9-118">Scenario description</span></span>
<span data-ttu-id="8d0c9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d0c9-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d0c9-121">Добавление Heroku из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8d0c9-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="8d0c9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d0c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="8d0c9-123">Добавление Heroku из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8d0c9-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="8d0c9-124">tooconfigure hello интеграции Heroku в Azure AD, вы должны tooadd Heroku из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d0c9-125">**tooadd Heroku из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d0c9-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d0c9-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d0c9-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d0c9-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8d0c9-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8d0c9-133">Введите в поле поиска hello **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-133">In hello search box, type **Heroku**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="8d0c9-135">В панели результатов hello выберите **Heroku**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d0c9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d0c9-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="8d0c9-138">В этом разделе описана настройка и проверка единого входа Azure AD в Heroku с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d0c9-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Heroku является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="8d0c9-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Heroku должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="8d0c9-141">В Heroku, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8d0c9-142">tooconfigure и теста Azure AD единого входа с Heroku, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d0c9-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d0c9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d0c9-145">**[Создание тестового пользователя Heroku](#creating-a-heroku-test-user)**  -toohave аналог Саймон Britta в Heroku, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d0c9-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d0c9-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d0c9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d0c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d0c9-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Heroku.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="8d0c9-150">**tooconfigure Azure AD единого входа с Heroku, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d0c9-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d0c9-151">В hello в hello портала Azure **Heroku** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8d0c9-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="8d0c9-155">На hello **URL-адреса и домена Heroku** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="8d0c9-157">а.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-157">a.</span></span> <span data-ttu-id="8d0c9-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="8d0c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-159">b.</span></span> <span data-ttu-id="8d0c9-160">В hello **URL-адрес идентификатора** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="8d0c9-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-161">These values are not real.</span></span> <span data-ttu-id="8d0c9-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8d0c9-163">Вы получаете эти значения от команды Heroku. Как это сделать, описано в последующих разделах этой статьи.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="8d0c9-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="8d0c9-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8d0c9-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d0c9-168">tooenable единого входа в Heroku, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="8d0c9-169">а.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-169">a.</span></span> <span data-ttu-id="8d0c9-170">Войдите в toohello Heroku учетную запись с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="8d0c9-171">b.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-171">b.</span></span> <span data-ttu-id="8d0c9-172">Нажмите кнопку hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="8d0c9-173">c.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-173">c.</span></span> <span data-ttu-id="8d0c9-174">На hello **единого входа на странице**, нажмите кнопку **Отправка метаданных**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="8d0c9-175">d.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-175">d.</span></span> <span data-ttu-id="8d0c9-176">Отправка файла метаданных hello, который вы скачали из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="8d0c9-177">д.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-177">e.</span></span> <span data-ttu-id="8d0c9-178">После успешной установки hello Администраторы видят диалоговое окно подтверждения и отображается URL-адрес hello hello Единого входа для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="8d0c9-179">f.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-179">f.</span></span> <span data-ttu-id="8d0c9-180">Hello копирования **URL-адрес входа Heroku** и **идентификатор сущности Heroku** значения и возвращается обратно слишком**URL-адреса и домена Heroku** статьи на портале Azure и вставьте эти значения в hello **URL-адрес входа** и **идентификатор** текстовые поля соответственно.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="8d0c9-182">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="8d0c9-183">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8d0c9-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8d0c9-184">После добавления этого приложения из hello **корпоративных приложений Active Directory** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8d0c9-185">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d0c9-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d0c9-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d0c9-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="8d0c9-187">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8d0c9-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d0c9-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d0c9-190">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d0c9-192">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d0c9-194">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8d0c9-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d0c9-196">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d0c9-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d0c9-198">а.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-198">a.</span></span> <span data-ttu-id="8d0c9-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d0c9-200">b.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-200">b.</span></span> <span data-ttu-id="8d0c9-201">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d0c9-202">c.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-202">c.</span></span> <span data-ttu-id="8d0c9-203">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d0c9-204">d.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-204">d.</span></span> <span data-ttu-id="8d0c9-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="8d0c9-206">Создание тестового пользователя Heroku</span><span class="sxs-lookup"><span data-stu-id="8d0c9-206">Creating a Heroku test user</span></span>

<span data-ttu-id="8d0c9-207">В этом разделе описано, как создать пользователя Britta Simon в приложении Heroku.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="8d0c9-208">Приложение Heroku поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8d0c9-209">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-209">There is no action item for you in this section.</span></span> <span data-ttu-id="8d0c9-210">При доступе к Heroku, если пользователь hello еще не существует, создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="8d0c9-211">После подготовки учетной записи hello hello конечный пользователь получит письмо с подтверждением, и должен связать tooclick hello подтверждения.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="8d0c9-212">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Heroku клиента поддержки](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="8d0c9-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d0c9-213">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8d0c9-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d0c9-214">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHeroku доступа.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8d0c9-216">**tooassign tooHeroku Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d0c9-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d0c9-217">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8d0c9-219">В списке приложений hello выберите **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-219">In hello applications list, select **Heroku**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="8d0c9-221">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8d0c9-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-223">Click **Add** button.</span></span> <span data-ttu-id="8d0c9-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8d0c9-226">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d0c9-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d0c9-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d0c9-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8d0c9-229">Testing single sign-on</span></span>

<span data-ttu-id="8d0c9-230">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8d0c9-231">При нажатии кнопки hello Heroku плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Heroku приложения.</span><span class="sxs-lookup"><span data-stu-id="8d0c9-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d0c9-232">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8d0c9-232">Additional resources</span></span>

* [<span data-ttu-id="8d0c9-233">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d0c9-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d0c9-234">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d0c9-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
