---
title: "Руководство по интеграции Azure Active Directory с Samanage | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="82a3e-103">Руководство. Интеграция Azure Active Directory с Samanage</span><span class="sxs-lookup"><span data-stu-id="82a3e-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="82a3e-104">В этом учебнике вы узнаете, как toointegrate Samanage с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82a3e-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82a3e-105">Интеграция Samanage с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="82a3e-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="82a3e-106">Можно управлять в Azure AD, имеющего доступ tooSamanage</span><span class="sxs-lookup"><span data-stu-id="82a3e-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="82a3e-107">Можно включить на пользователей tooautomatically get вошедшего tooSamanage (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a3e-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82a3e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="82a3e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="82a3e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82a3e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82a3e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82a3e-110">Prerequisites</span></span>

<span data-ttu-id="82a3e-111">tooconfigure интеграция Azure AD с Samanage требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="82a3e-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="82a3e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="82a3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82a3e-113">подписка Samanage с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="82a3e-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82a3e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="82a3e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82a3e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="82a3e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82a3e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="82a3e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82a3e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82a3e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82a3e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="82a3e-118">Scenario description</span></span>
<span data-ttu-id="82a3e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="82a3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82a3e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="82a3e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82a3e-121">Добавление Samanage из галереи hello</span><span class="sxs-lookup"><span data-stu-id="82a3e-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="82a3e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a3e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="82a3e-123">Добавление Samanage из галереи hello</span><span class="sxs-lookup"><span data-stu-id="82a3e-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="82a3e-124">tooconfigure hello интеграции Samanage в Azure AD, вы должны tooadd Samanage из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="82a3e-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="82a3e-125">**tooadd Samanage из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="82a3e-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a3e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="82a3e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82a3e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="82a3e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="82a3e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="82a3e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="82a3e-133">Введите в поле поиска hello **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-133">In hello search box, type **Samanage**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="82a3e-135">В панели результатов hello выберите **Samanage**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="82a3e-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82a3e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a3e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82a3e-138">В этом разделе описана настройка и проверка единого входа Azure AD в Samanage с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82a3e-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="82a3e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Samanage является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82a3e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="82a3e-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Samanage должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="82a3e-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="82a3e-141">В Samanage, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="82a3e-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="82a3e-142">tooconfigure и теста Azure AD единого входа с Samanage, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="82a3e-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="82a3e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="82a3e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="82a3e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="82a3e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82a3e-145">**[Создание тестового пользователя Samanage](#creating-a-samanage-test-user)**  -toohave аналог Саймон Britta в Samanage, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="82a3e-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="82a3e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="82a3e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82a3e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="82a3e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82a3e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a3e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82a3e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Samanage приложения.</span><span class="sxs-lookup"><span data-stu-id="82a3e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="82a3e-150">**tooconfigure Azure AD единого входа с помощью Samanage, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="82a3e-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a3e-151">В hello в hello портала Azure **Samanage** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="82a3e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="82a3e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="82a3e-155">На hello **URL-адреса и домена Samanage** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="82a3e-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="82a3e-157">а.</span><span class="sxs-lookup"><span data-stu-id="82a3e-157">a.</span></span> <span data-ttu-id="82a3e-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="82a3e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="82a3e-159">b.</span><span class="sxs-lookup"><span data-stu-id="82a3e-159">b.</span></span> <span data-ttu-id="82a3e-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="82a3e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82a3e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="82a3e-161">These values are not real.</span></span> <span data-ttu-id="82a3e-162">Обновите эти значения с hello фактический URL-адрес входа и идентификатор, который описан далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="82a3e-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="82a3e-163">Для получения дополнительных сведений обратитесь к [группе поддержки клиентов Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="82a3e-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="82a3e-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="82a3e-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="82a3e-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="82a3e-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="82a3e-168">На hello **конфигурации Samanage** щелкните **Настройка Samanage** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="82a3e-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="82a3e-169">Копировать hello **URL-адрес выхода и идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="82a3e-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="82a3e-171">В другом окне веб-браузера войдите на сайт Samanage компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="82a3e-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="82a3e-172">Щелкните **Панель мониторинга** и выберите **Настройка** в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="82a3e-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="82a3e-173">![Панель мониторинга](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Панель мониторинга")</span><span class="sxs-lookup"><span data-stu-id="82a3e-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="82a3e-174">Щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="82a3e-175">![Единый вход](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="82a3e-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="82a3e-176">Перейдите в слишком**вход с помощью SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="82a3e-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="82a3e-177">![Вход с помощью SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Вход с помощью SAML")</span><span class="sxs-lookup"><span data-stu-id="82a3e-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="82a3e-178">а.</span><span class="sxs-lookup"><span data-stu-id="82a3e-178">a.</span></span> <span data-ttu-id="82a3e-179">Установите флажок **Enable Single Sign-On with SAML**(Включить единый вход с помощью SAML).</span><span class="sxs-lookup"><span data-stu-id="82a3e-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="82a3e-180">b.</span><span class="sxs-lookup"><span data-stu-id="82a3e-180">b.</span></span> <span data-ttu-id="82a3e-181">В hello **URL-адрес поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="82a3e-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="82a3e-182">c.</span><span class="sxs-lookup"><span data-stu-id="82a3e-182">c.</span></span> <span data-ttu-id="82a3e-183">Подтвердите hello **URL-адрес входа** hello совпадений **на URL-адрес входа** из **URL-адреса и домена Samanage** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="82a3e-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="82a3e-184">d.</span><span class="sxs-lookup"><span data-stu-id="82a3e-184">d.</span></span> <span data-ttu-id="82a3e-185">В hello **URL-адрес выхода** текстовом поле введите значение hello **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="82a3e-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="82a3e-186">д.</span><span class="sxs-lookup"><span data-stu-id="82a3e-186">e.</span></span> <span data-ttu-id="82a3e-187">В hello **издатель SAML** текстовое поле, URI идентификатора приложения hello тип установить в поставщик удостоверений.</span><span class="sxs-lookup"><span data-stu-id="82a3e-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="82a3e-188">f.</span><span class="sxs-lookup"><span data-stu-id="82a3e-188">f.</span></span> <span data-ttu-id="82a3e-189">Откройте сертификат кодировке base-64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **вставьте вашего поставщика удостоверений x.509 ниже сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="82a3e-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="82a3e-190">ж.</span><span class="sxs-lookup"><span data-stu-id="82a3e-190">g.</span></span> <span data-ttu-id="82a3e-191">Установите флажок **Create users if they do not exist in Samanage**(Создавать пользователей, если они не существуют в Samanage).</span><span class="sxs-lookup"><span data-stu-id="82a3e-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="82a3e-192">h.</span><span class="sxs-lookup"><span data-stu-id="82a3e-192">h.</span></span> <span data-ttu-id="82a3e-193">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="82a3e-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="82a3e-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="82a3e-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="82a3e-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="82a3e-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82a3e-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82a3e-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a3e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="82a3e-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="82a3e-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="82a3e-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="82a3e-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a3e-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="82a3e-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82a3e-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82a3e-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="82a3e-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82a3e-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="82a3e-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82a3e-209">а.</span><span class="sxs-lookup"><span data-stu-id="82a3e-209">a.</span></span> <span data-ttu-id="82a3e-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82a3e-211">b.</span><span class="sxs-lookup"><span data-stu-id="82a3e-211">b.</span></span> <span data-ttu-id="82a3e-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="82a3e-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82a3e-213">c.</span><span class="sxs-lookup"><span data-stu-id="82a3e-213">c.</span></span> <span data-ttu-id="82a3e-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="82a3e-215">d.</span><span class="sxs-lookup"><span data-stu-id="82a3e-215">d.</span></span> <span data-ttu-id="82a3e-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="82a3e-217">Создание тестового пользователя в приложении Samanage</span><span class="sxs-lookup"><span data-stu-id="82a3e-217">Creating a Samanage test user</span></span>

<span data-ttu-id="82a3e-218">Пользователи toolog tooenable Azure AD в tooSamanage, их необходимо подготовить в Samanage.</span><span class="sxs-lookup"><span data-stu-id="82a3e-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="82a3e-219">В случае hello объекта Samanage Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="82a3e-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="82a3e-220">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="82a3e-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a3e-221">Войдите на корпоративный сайт Samanage в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="82a3e-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="82a3e-222">Щелкните **Dashboard** (Панель мониторинга) и выберите **Setup** (Настройка) в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="82a3e-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="82a3e-223">![Настройка](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="82a3e-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="82a3e-224">Нажмите кнопку hello **пользователей** вкладка</span><span class="sxs-lookup"><span data-stu-id="82a3e-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="82a3e-225">![Пользователи](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="82a3e-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="82a3e-226">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-226">Click **New User**.</span></span>
   
    <span data-ttu-id="82a3e-227">![Новый пользователь](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="82a3e-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="82a3e-228">Тип hello **имя** и hello **адрес электронной почты** учетной записи Azure Active Directory tooprovision и щелкните **создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="82a3e-229">![Создание пользователя](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="82a3e-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="82a3e-230">Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="82a3e-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="82a3e-231">Можно использовать любые другие Samanage пользователя средства создания учетных записей или API, предоставленные Samanage tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="82a3e-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="82a3e-232">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="82a3e-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="82a3e-233">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSamanage доступа.</span><span class="sxs-lookup"><span data-stu-id="82a3e-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="82a3e-235">**tooassign tooSamanage Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="82a3e-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a3e-236">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="82a3e-238">В списке приложений hello выберите **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-238">In hello applications list, select **Samanage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="82a3e-240">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="82a3e-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-242">Click **Add** button.</span></span> <span data-ttu-id="82a3e-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="82a3e-245">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="82a3e-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="82a3e-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82a3e-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="82a3e-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82a3e-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="82a3e-248">Testing single sign-on</span></span>

<span data-ttu-id="82a3e-249">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="82a3e-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="82a3e-250">При нажатии кнопки hello Samanage плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Samanage приложения.</span><span class="sxs-lookup"><span data-stu-id="82a3e-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="82a3e-251">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82a3e-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82a3e-252">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="82a3e-252">Additional resources</span></span>

* [<span data-ttu-id="82a3e-253">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82a3e-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82a3e-254">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82a3e-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

