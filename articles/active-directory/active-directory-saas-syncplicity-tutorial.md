---
title: "Руководство. Интеграция Azure Active Directory с Syncplicity | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="9391b-103">Учебник. Интеграция Azure Active Directory с Syncplicity</span><span class="sxs-lookup"><span data-stu-id="9391b-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="9391b-104">В этом учебнике вы узнаете, как toointegrate Syncplicity с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9391b-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9391b-105">Интеграция Syncplicity с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9391b-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9391b-106">Можно управлять в Azure AD, имеющего доступ tooSyncplicity</span><span class="sxs-lookup"><span data-stu-id="9391b-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="9391b-107">Можно включить на пользователей tooautomatically get вошедшего tooSyncplicity (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="9391b-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9391b-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9391b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9391b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9391b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9391b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9391b-110">Prerequisites</span></span>

<span data-ttu-id="9391b-111">tooconfigure интеграция Azure AD с Syncplicity требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9391b-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="9391b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9391b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9391b-113">подписка Syncplicity с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9391b-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9391b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9391b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9391b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="9391b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9391b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9391b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9391b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9391b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9391b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9391b-118">Scenario description</span></span>
<span data-ttu-id="9391b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9391b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9391b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="9391b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9391b-121">Добавление Syncplicity из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9391b-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="9391b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9391b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="9391b-123">Добавление Syncplicity из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9391b-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="9391b-124">tooconfigure hello интеграции Syncplicity в Azure AD, вы должны tooadd Syncplicity из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9391b-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9391b-125">**tooadd Syncplicity из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9391b-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9391b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9391b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9391b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="9391b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9391b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9391b-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9391b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9391b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9391b-133">Введите в поле поиска hello **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="9391b-133">In hello search box, type **Syncplicity**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="9391b-135">В панели результатов hello выберите **Syncplicity**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9391b-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9391b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9391b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9391b-138">В этом разделе описана настройка и проверка единого входа Azure AD в Syncplicity с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9391b-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9391b-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Syncplicity является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9391b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="9391b-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Syncplicity должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="9391b-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="9391b-141">В Syncplicity, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="9391b-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9391b-142">tooconfigure и теста Azure AD единого входа с Syncplicity, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9391b-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9391b-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="9391b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9391b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9391b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9391b-145">**[Создание тестового пользователя Syncplicity](#creating-a-syncplicity-test-user)**  -toohave аналог Саймон Britta в Syncplicity, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="9391b-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9391b-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="9391b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9391b-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9391b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9391b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9391b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9391b-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="9391b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="9391b-150">**Azure AD tooconfigure единого входа с Syncplicity, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9391b-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="9391b-151">В hello в hello портала Azure **Syncplicity** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9391b-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9391b-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="9391b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="9391b-155">На hello **URL-адреса и домена Syncplicity** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9391b-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="9391b-157">а.</span><span class="sxs-lookup"><span data-stu-id="9391b-157">a.</span></span> <span data-ttu-id="9391b-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="9391b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="9391b-159">b.</span><span class="sxs-lookup"><span data-stu-id="9391b-159">b.</span></span> <span data-ttu-id="9391b-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="9391b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9391b-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9391b-161">These values are not real.</span></span> <span data-ttu-id="9391b-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9391b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9391b-163">Обратитесь к [группа поддержки клиента Syncplicity](https://www.syncplicity.com/contact-us) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="9391b-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="9391b-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="9391b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="9391b-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9391b-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9391b-168">На hello **конфигурации Syncplicity** щелкните **Настройка Syncplicity** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="9391b-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9391b-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="9391b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="9391b-171">Войдите в tooyour **Syncplicity** клиента.</span><span class="sxs-lookup"><span data-stu-id="9391b-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="9391b-172">В меню в верхней части hello hello выберите **администратора**выберите **параметры**и нажмите кнопку **пользовательский домен и единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9391b-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="9391b-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="9391b-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="9391b-174">На hello **единый вход (SSO)** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9391b-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="9391b-175">![Единый вход\(Единый вход\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="9391b-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="9391b-176">а.</span><span class="sxs-lookup"><span data-stu-id="9391b-176">a.</span></span> <span data-ttu-id="9391b-177">В hello **пользовательский домен** текстового поля, типа hello имя вашего домена.</span><span class="sxs-lookup"><span data-stu-id="9391b-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="9391b-178">b.</span><span class="sxs-lookup"><span data-stu-id="9391b-178">b.</span></span> <span data-ttu-id="9391b-179">В поле **Состояния единого входа** задайте значение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="9391b-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="9391b-180">c.</span><span class="sxs-lookup"><span data-stu-id="9391b-180">c.</span></span> <span data-ttu-id="9391b-181">В hello **идентификатор сущности** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="9391b-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9391b-182">d.</span><span class="sxs-lookup"><span data-stu-id="9391b-182">d.</span></span> <span data-ttu-id="9391b-183">В hello **входа в URL-адрес страницы** текстовое поле, вставить hello **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="9391b-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9391b-184">д.</span><span class="sxs-lookup"><span data-stu-id="9391b-184">e.</span></span> <span data-ttu-id="9391b-185">В hello **URL-адрес страницы выхода** текстовое поле, вставить hello **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="9391b-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9391b-186">f.</span><span class="sxs-lookup"><span data-stu-id="9391b-186">f.</span></span> <span data-ttu-id="9391b-187">В **сертификат поставщика удостоверений**, нажмите кнопку **выбрать файл**, а затем отправьте hello сертификат, который вы скачали из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9391b-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="9391b-188">ж.</span><span class="sxs-lookup"><span data-stu-id="9391b-188">g.</span></span> <span data-ttu-id="9391b-189">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="9391b-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="9391b-190">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="9391b-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9391b-191">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="9391b-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9391b-192">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9391b-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9391b-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9391b-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="9391b-194">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9391b-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9391b-196">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9391b-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9391b-197">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9391b-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9391b-199">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9391b-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9391b-201">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="9391b-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9391b-203">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9391b-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9391b-205">а.</span><span class="sxs-lookup"><span data-stu-id="9391b-205">a.</span></span> <span data-ttu-id="9391b-206">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9391b-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9391b-207">b.</span><span class="sxs-lookup"><span data-stu-id="9391b-207">b.</span></span> <span data-ttu-id="9391b-208">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9391b-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9391b-209">c.</span><span class="sxs-lookup"><span data-stu-id="9391b-209">c.</span></span> <span data-ttu-id="9391b-210">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="9391b-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9391b-211">d.</span><span class="sxs-lookup"><span data-stu-id="9391b-211">d.</span></span> <span data-ttu-id="9391b-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9391b-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="9391b-213">Создание тестового пользователя Syncplicity</span><span class="sxs-lookup"><span data-stu-id="9391b-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="9391b-214">Для AAD пользователей toobe может toosign в они должны быть tooSyncplicity подготовленные приложения.</span><span class="sxs-lookup"><span data-stu-id="9391b-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="9391b-215">В этом разделе описывается, как учетные записи пользователей toocreate AAD в Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="9391b-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="9391b-216">**tooprovision tooSyncplicity учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9391b-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="9391b-217">Войдите в tooyour **Syncplicity** клиента (например: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="9391b-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="9391b-218">Щелкните **Администрирование** и выберите **Учетные записи пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9391b-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="9391b-219">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="9391b-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="9391b-220">![Управление пользователями](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="9391b-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="9391b-221">Тип hello **адресов электронной почты** учетной записи AAD, вы хотите tooprovision, выберите **пользователя** как **роли**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9391b-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="9391b-222">![Сведения об учетной записи](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Сведения об учетной записи")</span><span class="sxs-lookup"><span data-stu-id="9391b-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="9391b-223">Держатель учетной записи AAD Hello получает сообщение электронной почты, tooconfirm ссылку и активации учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="9391b-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="9391b-224">Выберите группу в организации, в которую будет входить новый пользователь, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9391b-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="9391b-225">![Участие в группах](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Участие в группах")</span><span class="sxs-lookup"><span data-stu-id="9391b-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="9391b-226">Если список групп пуст, просто нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9391b-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="9391b-227">Выберите папки hello бы как tooplace под управлением Syncplicity на компьютере пользователя hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9391b-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="9391b-228">![Папки Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Папки Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="9391b-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="9391b-229">Можно использовать любые другие Syncplicity пользователя средства создания учетных записей или интерфейсы API, предоставляемые Syncplicity tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="9391b-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9391b-230">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="9391b-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9391b-231">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSyncplicity доступа.</span><span class="sxs-lookup"><span data-stu-id="9391b-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9391b-233">**tooassign tooSyncplicity Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9391b-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="9391b-234">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9391b-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9391b-236">В списке приложений hello выберите **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="9391b-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="9391b-238">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="9391b-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9391b-240">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9391b-240">Click **Add** button.</span></span> <span data-ttu-id="9391b-241">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9391b-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9391b-243">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="9391b-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9391b-244">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9391b-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9391b-245">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9391b-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9391b-246">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9391b-246">Testing single sign-on</span></span>

<span data-ttu-id="9391b-247">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="9391b-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9391b-248">При нажатии кнопки hello Syncplicity плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Syncplicity приложения.</span><span class="sxs-lookup"><span data-stu-id="9391b-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="9391b-249">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9391b-249">Additional resources</span></span>

* [<span data-ttu-id="9391b-250">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9391b-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9391b-251">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9391b-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

