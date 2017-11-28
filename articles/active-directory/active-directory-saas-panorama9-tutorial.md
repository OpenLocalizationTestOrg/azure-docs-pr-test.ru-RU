---
title: "Руководство по интеграции Azure Active Directory с Panorama9 | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="5a05d-103">Учебник. Интеграция Azure Active Directory с Panorama9</span><span class="sxs-lookup"><span data-stu-id="5a05d-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="5a05d-104">В этом учебнике вы узнаете, как toointegrate Panorama9 с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a05d-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a05d-105">Интеграция Panorama9 с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5a05d-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a05d-106">Можно управлять в Azure AD, имеющего доступ tooPanorama9</span><span class="sxs-lookup"><span data-stu-id="5a05d-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="5a05d-107">Можно включить на пользователей tooautomatically get вошедшего tooPanorama9 (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a05d-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a05d-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5a05d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5a05d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a05d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a05d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5a05d-110">Prerequisites</span></span>

<span data-ttu-id="5a05d-111">tooconfigure интеграция Azure AD с Panorama9 требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5a05d-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="5a05d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5a05d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a05d-113">Подписка с поддержкой единого входа Panorama9.</span><span class="sxs-lookup"><span data-stu-id="5a05d-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a05d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5a05d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a05d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5a05d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a05d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5a05d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a05d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a05d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a05d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5a05d-118">Scenario description</span></span>
<span data-ttu-id="5a05d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5a05d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a05d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5a05d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a05d-121">Добавление Panorama9 из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5a05d-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="5a05d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a05d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="5a05d-123">Добавление Panorama9 из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5a05d-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="5a05d-124">tooconfigure hello интеграции Panorama9 в Azure AD, вы должны tooadd Panorama9 из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5a05d-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a05d-125">**tooadd Panorama9 из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5a05d-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a05d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5a05d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a05d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a05d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5a05d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5a05d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5a05d-133">Введите в поле поиска hello **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-133">In hello search box, type **Panorama9**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="5a05d-135">В панели результатов hello выберите **Panorama9**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5a05d-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a05d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a05d-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="5a05d-138">В этом разделе описана настройка и проверка единого входа Azure AD в Panorama9 с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a05d-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5a05d-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Panorama9 является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a05d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="5a05d-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Panorama9 должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5a05d-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="5a05d-141">В Panorama9, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="5a05d-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a05d-142">tooconfigure и теста Azure AD единого входа с Panorama9, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5a05d-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a05d-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5a05d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a05d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5a05d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a05d-145">**[Создание тестового пользователя Panorama9](#creating-a-panorama9-test-user)**  -toohave аналог Саймон Britta в Panorama9, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5a05d-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a05d-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5a05d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a05d-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5a05d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a05d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a05d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a05d-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Panorama9 приложения.</span><span class="sxs-lookup"><span data-stu-id="5a05d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="5a05d-150">**tooconfigure Azure AD единого входа с Panorama9, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5a05d-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a05d-151">В hello в hello портала Azure **Panorama9** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5a05d-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5a05d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="5a05d-155">На hello **URL-адреса и домена Panorama9** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5a05d-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="5a05d-157">а.</span><span class="sxs-lookup"><span data-stu-id="5a05d-157">a.</span></span> <span data-ttu-id="5a05d-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="5a05d-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="5a05d-159">b.</span><span class="sxs-lookup"><span data-stu-id="5a05d-159">b.</span></span> <span data-ttu-id="5a05d-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="5a05d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a05d-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5a05d-161">These values are not real.</span></span> <span data-ttu-id="5a05d-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="5a05d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5a05d-163">Обратитесь к [группа поддержки клиента Panorama9](https://support.panorama9.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="5a05d-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="5a05d-164">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="5a05d-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="5a05d-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5a05d-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5a05d-168">На hello **конфигурации Panorama9** щелкните **Настройка Panorama9** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="5a05d-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5a05d-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="5a05d-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="5a05d-171">В другом окне веб-браузера войдите на сайт Panorama9 своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5a05d-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="5a05d-172">Щелкните hello панели инструментов в верхней части hello **управление**, а затем нажмите кнопку **расширения**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="5a05d-173">![Расширения](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Расширения")</span><span class="sxs-lookup"><span data-stu-id="5a05d-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="5a05d-174">На hello **расширения** диалоговое окно, нажмите кнопку **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="5a05d-175">![Единый вход](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="5a05d-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="5a05d-176">В hello **параметры** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5a05d-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="5a05d-177">![Параметры](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="5a05d-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="5a05d-178">а.</span><span class="sxs-lookup"><span data-stu-id="5a05d-178">a.</span></span> <span data-ttu-id="5a05d-179">В **URL-адрес поставщика удостоверений** текстовое значение hello вставить **единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5a05d-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="5a05d-180">b.</span><span class="sxs-lookup"><span data-stu-id="5a05d-180">b.</span></span> <span data-ttu-id="5a05d-181">В **отпечаток сертификата** текстовое поле, вставить hello **отпечаток** значение сертификат, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5a05d-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="5a05d-182">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5a05d-183">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5a05d-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a05d-184">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5a05d-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a05d-185">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a05d-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a05d-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a05d-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a05d-187">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5a05d-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5a05d-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5a05d-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a05d-190">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5a05d-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a05d-192">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a05d-194">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="5a05d-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a05d-196">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5a05d-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a05d-198">а.</span><span class="sxs-lookup"><span data-stu-id="5a05d-198">a.</span></span> <span data-ttu-id="5a05d-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a05d-200">b.</span><span class="sxs-lookup"><span data-stu-id="5a05d-200">b.</span></span> <span data-ttu-id="5a05d-201">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5a05d-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a05d-202">c.</span><span class="sxs-lookup"><span data-stu-id="5a05d-202">c.</span></span> <span data-ttu-id="5a05d-203">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5a05d-204">d.</span><span class="sxs-lookup"><span data-stu-id="5a05d-204">d.</span></span> <span data-ttu-id="5a05d-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="5a05d-206">Создание тестового пользователя Panorama9</span><span class="sxs-lookup"><span data-stu-id="5a05d-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="5a05d-207">В порядке tooenable toolog пользователей Azure AD в Panorama9 их необходимо подготовить в Panorama9.</span><span class="sxs-lookup"><span data-stu-id="5a05d-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="5a05d-208">В случае Panorama9 hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="5a05d-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="5a05d-209">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5a05d-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a05d-210">Войдите в tooyour **Panorama9** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="5a05d-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="5a05d-211">В меню в верхней части hello hello выберите **управление**, а затем нажмите кнопку **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="5a05d-212">![Пользователи](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="5a05d-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="5a05d-213">В hello раздел "пользователи", щелкните  **+**  tooadd нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="5a05d-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="5a05d-214">![Пользователи](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="5a05d-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="5a05d-215">Последовательно выберите toohello раздел данных пользователя, типа hello адрес электронной почты действительного пользователя Azure Active Directory требуется tooprovision в hello **электронной почты** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="5a05d-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="5a05d-216">Поступать toohello раздел "пользователи", нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="5a05d-217">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="5a05d-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5a05d-218">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5a05d-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5a05d-219">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPanorama9 доступа.</span><span class="sxs-lookup"><span data-stu-id="5a05d-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5a05d-221">**tooassign tooPanorama9 Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5a05d-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a05d-222">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5a05d-224">В списке приложений hello выберите **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-224">In hello applications list, select **Panorama9**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="5a05d-226">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5a05d-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-228">Click **Add** button.</span></span> <span data-ttu-id="5a05d-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5a05d-231">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5a05d-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a05d-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a05d-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5a05d-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a05d-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5a05d-234">Testing single sign-on</span></span>

<span data-ttu-id="5a05d-235">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5a05d-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a05d-236">При нажатии кнопки hello Panorama9 плитки в панели доступа hello, вы должны получить автоматически вошедшего tooPanorama9 приложения.</span><span class="sxs-lookup"><span data-stu-id="5a05d-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="5a05d-237">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a05d-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a05d-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5a05d-238">Additional resources</span></span>

* [<span data-ttu-id="5a05d-239">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a05d-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a05d-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5a05d-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

