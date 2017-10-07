---
title: "Руководство по интеграции Azure Active Directory с Picturepark | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="f4a2e-103">Руководство по интеграции Azure Active Directory с Picturepark</span><span class="sxs-lookup"><span data-stu-id="f4a2e-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="f4a2e-104">В этом учебнике вы узнаете, как toointegrate Picturepark с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4a2e-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4a2e-105">Интеграция Picturepark с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f4a2e-106">Можно управлять в Azure AD, имеющего доступ tooPicturepark</span><span class="sxs-lookup"><span data-stu-id="f4a2e-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="f4a2e-107">Можно включить на пользователей tooautomatically get вошедшего tooPicturepark (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4a2e-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4a2e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f4a2e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f4a2e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4a2e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4a2e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f4a2e-110">Prerequisites</span></span>

<span data-ttu-id="f4a2e-111">tooconfigure интеграция Azure AD с Picturepark требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="f4a2e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f4a2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4a2e-113">подписка Picturepark с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4a2e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4a2e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4a2e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4a2e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4a2e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4a2e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f4a2e-118">Scenario description</span></span>
<span data-ttu-id="f4a2e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4a2e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4a2e-121">Добавление Picturepark из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f4a2e-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="f4a2e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4a2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="f4a2e-123">Добавление Picturepark из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f4a2e-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="f4a2e-124">tooconfigure hello интеграции Picturepark в Azure AD, вы должны tooadd Picturepark из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f4a2e-125">**tooadd Picturepark из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4a2e-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4a2e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f4a2e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f4a2e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f4a2e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f4a2e-133">Введите в поле поиска hello **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-133">In hello search box, type **Picturepark**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="f4a2e-135">В панели результатов hello выберите **Picturepark**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4a2e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4a2e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4a2e-138">В этом разделе описана настройка и проверка единого входа Azure AD в Picturepark с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f4a2e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Picturepark является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="f4a2e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Picturepark должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="f4a2e-141">В Picturepark, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f4a2e-142">tooconfigure и теста Azure AD единого входа с Picturepark, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f4a2e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f4a2e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4a2e-145">**[Создание тестового пользователя Picturepark](#creating-a-picturepark-test-user)**  -toohave аналог Саймон Britta в Picturepark, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4a2e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4a2e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4a2e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4a2e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4a2e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Picturepark приложения.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="f4a2e-150">**tooconfigure Azure AD единого входа с Picturepark, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4a2e-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4a2e-151">В hello в hello портала Azure **Picturepark** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f4a2e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="f4a2e-155">На hello **URL-адреса и домена Picturepark** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="f4a2e-157">а.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-157">a.</span></span> <span data-ttu-id="f4a2e-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="f4a2e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="f4a2e-159">b.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-159">b.</span></span> <span data-ttu-id="f4a2e-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="f4a2e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-161">These values are not real.</span></span> <span data-ttu-id="f4a2e-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f4a2e-163">Обратитесь к [группа поддержки клиент Picturepark](https://picturepark.com/about/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="f4a2e-164">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="f4a2e-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f4a2e-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f4a2e-168">На hello **конфигурации Picturepark** щелкните **Настройка Picturepark** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f4a2e-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="f4a2e-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="f4a2e-171">В другом окне веб-браузера войдите на сайт Picturepark своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="f4a2e-172">Щелкните hello панели инструментов в верхней части hello **Администрирование**, а затем нажмите кнопку **консоли управления**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="f4a2e-173">![Консоль управления](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Консоль управления")</span><span class="sxs-lookup"><span data-stu-id="f4a2e-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="f4a2e-174">Щелкните **Authentication** (Аутентификация), а затем выберите **Identity providers** (Поставщики удостоверений).</span><span class="sxs-lookup"><span data-stu-id="f4a2e-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="f4a2e-175">![Аутентификация](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="f4a2e-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="f4a2e-176">В hello **конфигурация поставщика удостоверений** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f4a2e-177">![Конфигурация поставщика удостоверений](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Конфигурация поставщика удостоверений")</span><span class="sxs-lookup"><span data-stu-id="f4a2e-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="f4a2e-178">а.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-178">a.</span></span> <span data-ttu-id="f4a2e-179">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-179">Click **Add**.</span></span>
  
    <span data-ttu-id="f4a2e-180">b.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-180">b.</span></span> <span data-ttu-id="f4a2e-181">Введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="f4a2e-182">c.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-182">c.</span></span> <span data-ttu-id="f4a2e-183">Выберите **По умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="f4a2e-184">d.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-184">d.</span></span> <span data-ttu-id="f4a2e-185">В **URI издателя** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f4a2e-186">д.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-186">e.</span></span> <span data-ttu-id="f4a2e-187">В **отпечаток доверенного издателя** текстовое значение hello вставить **отпечаток** скопирован из **сертификат подписи SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="f4a2e-188">Щелкните **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="f4a2e-189">tooset hello **Emailaddress** атрибута в hello **утверждения** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="f4a2e-190">![Конфигурация](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Конфигурация")</span><span class="sxs-lookup"><span data-stu-id="f4a2e-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="f4a2e-191">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f4a2e-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f4a2e-192">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f4a2e-193">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4a2e-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4a2e-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4a2e-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4a2e-195">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f4a2e-197">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4a2e-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4a2e-198">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4a2e-200">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4a2e-202">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f4a2e-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4a2e-204">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4a2e-206">а.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-206">a.</span></span> <span data-ttu-id="f4a2e-207">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4a2e-208">b.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-208">b.</span></span> <span data-ttu-id="f4a2e-209">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4a2e-210">c.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-210">c.</span></span> <span data-ttu-id="f4a2e-211">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f4a2e-212">d.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-212">d.</span></span> <span data-ttu-id="f4a2e-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="f4a2e-214">Создание тестового пользователя Picturepark</span><span class="sxs-lookup"><span data-stu-id="f4a2e-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="f4a2e-215">В порядке tooenable toolog пользователей Azure AD в Picturepark их необходимо подготовить в Picturepark.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="f4a2e-216">В случае hello Picturepark Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="f4a2e-217">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4a2e-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4a2e-218">Войдите в tooyour **Picturepark** клиента.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="f4a2e-219">Щелкните hello панели инструментов в верхней части hello **Администрирование**, а затем нажмите кнопку **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="f4a2e-220">![Пользователи](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="f4a2e-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="f4a2e-221">В hello **Обзор пользователей** щелкните **New**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="f4a2e-222">![Управление пользователями](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="f4a2e-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="f4a2e-223">На hello **Create User** диалогового окна hello выполните следующие действия действительного пользователя Active Directory Azure требуется tooprovision:</span><span class="sxs-lookup"><span data-stu-id="f4a2e-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="f4a2e-224">![Создание пользователя](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="f4a2e-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="f4a2e-225">а.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-225">a.</span></span> <span data-ttu-id="f4a2e-226">В hello **адрес электронной почты** в текстовое поле типа hello **адрес электронной почты** пользователя hello  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f4a2e-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="f4a2e-227">b.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-227">b.</span></span> <span data-ttu-id="f4a2e-228">В hello **пароль** и **подтверждение пароля** текстовые поля, типа hello **пароль** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="f4a2e-229">c.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-229">c.</span></span> <span data-ttu-id="f4a2e-230">В hello **имя** в текстовое поле типа hello **имя** пользователя hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="f4a2e-231">d.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-231">d.</span></span> <span data-ttu-id="f4a2e-232">В hello **Фамилия** в текстовое поле типа hello **Фамилия** пользователя hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="f4a2e-233">д.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-233">e.</span></span> <span data-ttu-id="f4a2e-234">В hello **компании** в текстовое поле типа hello **название компании** hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="f4a2e-235">f.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-235">f.</span></span> <span data-ttu-id="f4a2e-236">В hello **страны** текстового поля, выберите hello **страны** hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="f4a2e-237">ж.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-237">g.</span></span> <span data-ttu-id="f4a2e-238">В hello **ZIP** в текстовое поле типа hello **ПОЧТОВЫЙ индекс** hello города.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="f4a2e-239">h.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-239">h.</span></span> <span data-ttu-id="f4a2e-240">В hello **Город** в текстовое поле типа hello **название города** hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="f4a2e-241">i.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-241">i.</span></span> <span data-ttu-id="f4a2e-242">В поле **Язык**укажите язык.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="f4a2e-243">j.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-243">j.</span></span> <span data-ttu-id="f4a2e-244">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="f4a2e-245">Можно использовать любые другие Picturepark пользователя средства создания учетных записей или интерфейсы API, предоставляемые Picturepark tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f4a2e-246">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f4a2e-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f4a2e-247">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPicturepark доступа.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f4a2e-249">**tooassign tooPicturepark Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4a2e-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4a2e-250">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f4a2e-252">В списке приложений hello выберите **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-252">In hello applications list, select **Picturepark**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="f4a2e-254">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f4a2e-256">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-256">Click **Add** button.</span></span> <span data-ttu-id="f4a2e-257">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f4a2e-259">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f4a2e-260">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4a2e-261">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f4a2e-262">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f4a2e-262">Testing single sign-on</span></span>

<span data-ttu-id="f4a2e-263">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f4a2e-264">При нажатии кнопки hello Picturepark плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на Picturepark приложения.</span><span class="sxs-lookup"><span data-stu-id="f4a2e-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="f4a2e-265">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4a2e-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f4a2e-266">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f4a2e-266">Additional resources</span></span>

* [<span data-ttu-id="f4a2e-267">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4a2e-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4a2e-268">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4a2e-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

