---
title: "Руководство по интеграции Azure Active Directory с Dropbox for Business | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Dropbox для бизнеса."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="67aaf-103">Руководство. Интеграция Azure Active Directory с Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="67aaf-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="67aaf-104">В этом учебнике вы узнаете, как toointegrate Dropbox для бизнеса с помощью Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67aaf-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67aaf-105">Интеграция Dropbox для бизнеса с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="67aaf-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="67aaf-106">Можно управлять в Azure AD, имеющего доступ tooDropbox для бизнеса</span><span class="sxs-lookup"><span data-stu-id="67aaf-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="67aaf-107">Вы можете включить вашей пользователей tooautomatically get вошедшего tooDropbox для бизнеса (Single Sign-On) учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="67aaf-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67aaf-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="67aaf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="67aaf-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67aaf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67aaf-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="67aaf-110">Prerequisites</span></span>

<span data-ttu-id="67aaf-111">tooconfigure интеграция Azure AD с Dropbox для бизнеса требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="67aaf-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="67aaf-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="67aaf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67aaf-113">подписка Dropbox for Business с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="67aaf-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67aaf-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="67aaf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67aaf-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="67aaf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67aaf-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="67aaf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67aaf-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67aaf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67aaf-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="67aaf-118">Scenario description</span></span>
<span data-ttu-id="67aaf-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="67aaf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67aaf-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="67aaf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67aaf-121">Добавление из галереи hello Dropbox для бизнеса</span><span class="sxs-lookup"><span data-stu-id="67aaf-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="67aaf-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="67aaf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="67aaf-123">Добавление из галереи hello Dropbox для бизнеса</span><span class="sxs-lookup"><span data-stu-id="67aaf-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="67aaf-124">интеграции hello tooconfigure Dropbox для бизнеса в Azure AD, необходимо tooadd Dropbox для бизнеса из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="67aaf-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="67aaf-125">**tooadd Dropbox для бизнеса из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="67aaf-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="67aaf-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="67aaf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67aaf-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="67aaf-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="67aaf-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="67aaf-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="67aaf-133">Введите в поле поиска hello **Dropbox для бизнеса**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="67aaf-135">В панели результатов hello выберите **Dropbox для бизнеса**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="67aaf-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67aaf-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="67aaf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67aaf-138">В этом разделе описана настройка и проверка единого входа Azure AD в Dropbox for Business с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67aaf-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67aaf-139">Для единого входа toowork Azure AD необходима tooknow какой пользователь hello аналога в Dropbox для бизнеса — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67aaf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="67aaf-140">Другими словами связи между hello связанных пользователей в Dropbox для бизнеса и пользователя Azure AD должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="67aaf-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="67aaf-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Dropbox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="67aaf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="67aaf-142">tooconfigure и теста Azure AD единого входа с Dropbox для бизнеса, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="67aaf-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="67aaf-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="67aaf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="67aaf-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="67aaf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67aaf-145">**[Создание Dropbox для бизнеса тестового пользователя](#creating-a-dropbox-for-business-test-user)**  -toohave аналог Саймон Britta в Dropbox для бизнеса, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="67aaf-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="67aaf-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="67aaf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67aaf-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="67aaf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67aaf-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="67aaf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67aaf-149">В этом разделе Azure AD единым входом в портал Azure hello включить и настроить единый вход в Dropbox для бизнес-приложений.</span><span class="sxs-lookup"><span data-stu-id="67aaf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="67aaf-150">**Azure AD tooconfigure единого входа с Dropbox для бизнеса, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="67aaf-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="67aaf-151">В hello в hello портала Azure **Dropbox для бизнеса** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="67aaf-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="67aaf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="67aaf-155">На hello **Dropbox для бизнеса домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="67aaf-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="67aaf-156">а.</span><span class="sxs-lookup"><span data-stu-id="67aaf-156">a.</span></span> <span data-ttu-id="67aaf-157">Войдите на tooyour Dropbox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="67aaf-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="67aaf-158">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="67aaf-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="67aaf-159">b.</span><span class="sxs-lookup"><span data-stu-id="67aaf-159">b.</span></span> <span data-ttu-id="67aaf-160">Hello hello левой панели навигации щелкните **консоли администрирования**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="67aaf-161">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="67aaf-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="67aaf-162">c.</span><span class="sxs-lookup"><span data-stu-id="67aaf-162">c.</span></span> <span data-ttu-id="67aaf-163">На hello **консоли администрирования**, нажмите кнопку **проверки подлинности** hello левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="67aaf-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="67aaf-164">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="67aaf-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="67aaf-165">d.</span><span class="sxs-lookup"><span data-stu-id="67aaf-165">d.</span></span> <span data-ttu-id="67aaf-166">В hello **единого входа** выберите **Включить единый вход**, а затем нажмите кнопку **дополнительные** tooexpand в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="67aaf-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="67aaf-167">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="67aaf-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="67aaf-168">д.</span><span class="sxs-lookup"><span data-stu-id="67aaf-168">e.</span></span> <span data-ttu-id="67aaf-169">Скопируйте URL-адрес hello рядом слишком**пользователи могут войти, введя свой адрес электронной почты или переходить непосредственно к**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="67aaf-171">f.</span><span class="sxs-lookup"><span data-stu-id="67aaf-171">f.</span></span> <span data-ttu-id="67aaf-172">На портал Azure, в hello hello **URL-адрес входа** в текстовое поле URL-адрес для вставки hello.</span><span class="sxs-lookup"><span data-stu-id="67aaf-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="67aaf-174">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="67aaf-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67aaf-175">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="67aaf-175">This value is not real value.</span></span> <span data-ttu-id="67aaf-176">Обновите значение hello с hello фактический URL-адрес входа получить из их раздела единого входа.</span><span class="sxs-lookup"><span data-stu-id="67aaf-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="67aaf-177">Обратитесь к [Dropbox для бизнеса клиента поддержки](https://www.dropbox.com/business/contact) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="67aaf-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="67aaf-178">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="67aaf-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="67aaf-180">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="67aaf-180">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67aaf-182">На hello **Dropbox для бизнеса конфигурации** щелкните **настроить Dropbox для бизнеса** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="67aaf-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="67aaf-183">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="67aaf-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="67aaf-185">tooconfigure единого входа на **Dropbox для бизнеса** стороны, перейдите на клиенте Dropbox для бизнеса, в hello **единого входа** раздел hello **проверки подлинности** страницы, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="67aaf-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="67aaf-186">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="67aaf-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="67aaf-187">а.</span><span class="sxs-lookup"><span data-stu-id="67aaf-187">a.</span></span> <span data-ttu-id="67aaf-188">Установите флажок **Обязательно**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-188">Click **Required**.</span></span>
   
    <span data-ttu-id="67aaf-189">b.</span><span class="sxs-lookup"><span data-stu-id="67aaf-189">b.</span></span> <span data-ttu-id="67aaf-190">В hello в hello портала Azure **Настройка входа** окна, hello копирования **SAML единого входа URL-адрес службы** значение, а затем вставьте его в hello **URL-адрес входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="67aaf-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="67aaf-191">c.</span><span class="sxs-lookup"><span data-stu-id="67aaf-191">c.</span></span> <span data-ttu-id="67aaf-192">Нажмите кнопку **изменить сертификат**, а затем найдите tooyour **файл сертификата в кодировке Base64**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="67aaf-193">d.</span><span class="sxs-lookup"><span data-stu-id="67aaf-193">d.</span></span> <span data-ttu-id="67aaf-194">Нажмите кнопку **сохранить изменения** toocomplete hello конфигурации на клиенте DropBox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="67aaf-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="67aaf-195">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="67aaf-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="67aaf-196">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="67aaf-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="67aaf-197">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="67aaf-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67aaf-198">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="67aaf-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="67aaf-199">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="67aaf-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="67aaf-201">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="67aaf-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="67aaf-202">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="67aaf-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="67aaf-204">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67aaf-206">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="67aaf-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67aaf-208">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="67aaf-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67aaf-210">а.</span><span class="sxs-lookup"><span data-stu-id="67aaf-210">a.</span></span> <span data-ttu-id="67aaf-211">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67aaf-212">b.</span><span class="sxs-lookup"><span data-stu-id="67aaf-212">b.</span></span> <span data-ttu-id="67aaf-213">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="67aaf-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67aaf-214">c.</span><span class="sxs-lookup"><span data-stu-id="67aaf-214">c.</span></span> <span data-ttu-id="67aaf-215">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="67aaf-216">d.</span><span class="sxs-lookup"><span data-stu-id="67aaf-216">d.</span></span> <span data-ttu-id="67aaf-217">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="67aaf-218">Создание тестового пользователя Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="67aaf-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="67aaf-219">В этом разделе вы создадите в Dropbox for Business пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67aaf-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="67aaf-220">Приложение Dropbox for Business поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="67aaf-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="67aaf-221">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="67aaf-221">There is no action item for you in this section.</span></span> <span data-ttu-id="67aaf-222">Если пользователь еще не существует в Dropbox для бизнеса, создается новый, при попытке tooaccess Dropbox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="67aaf-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="67aaf-223">При необходимости пользователь вручную, обратитесь к toocreate [Dropbox для бизнеса клиента поддержки](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="67aaf-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="67aaf-224">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="67aaf-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="67aaf-225">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooDropbox для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="67aaf-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="67aaf-227">**tooassign tooDropbox Britta Simon для бизнеса, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="67aaf-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="67aaf-228">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="67aaf-230">В списке приложений hello выберите **Dropbox для бизнеса**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="67aaf-232">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="67aaf-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-234">Click **Add** button.</span></span> <span data-ttu-id="67aaf-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="67aaf-237">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="67aaf-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="67aaf-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67aaf-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="67aaf-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67aaf-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="67aaf-240">Testing single sign-on</span></span>

<span data-ttu-id="67aaf-241">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="67aaf-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="67aaf-242">При нажатии кнопки hello Dropbox для бизнеса плитки в панели доступа hello, вы должны получить страницу входа для Dropbox для бизнес-приложений.</span><span class="sxs-lookup"><span data-stu-id="67aaf-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="67aaf-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="67aaf-243">Additional resources</span></span>

* [<span data-ttu-id="67aaf-244">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67aaf-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67aaf-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="67aaf-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="67aaf-246">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="67aaf-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

