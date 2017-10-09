---
title: "Руководство по интеграции Azure Active Directory с ITRP | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="73733-103">Руководство по интеграции Azure Active Directory с ITRP</span><span class="sxs-lookup"><span data-stu-id="73733-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="73733-104">В этом учебнике вы узнаете, как toointegrate ITRP с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73733-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73733-105">Интеграция ITRP с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="73733-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73733-106">Можно управлять в Azure AD, имеющего доступ tooITRP</span><span class="sxs-lookup"><span data-stu-id="73733-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="73733-107">Можно включить на пользователей tooautomatically get вошедшего tooITRP (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="73733-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73733-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="73733-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73733-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73733-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73733-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="73733-110">Prerequisites</span></span>

<span data-ttu-id="73733-111">tooconfigure интеграция Azure AD с ITRP требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="73733-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="73733-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="73733-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73733-113">подписка ITRP с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="73733-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73733-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="73733-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73733-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="73733-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73733-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="73733-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73733-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73733-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73733-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="73733-118">Scenario description</span></span>
<span data-ttu-id="73733-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="73733-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73733-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="73733-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73733-121">Добавление ITRP из галереи hello</span><span class="sxs-lookup"><span data-stu-id="73733-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="73733-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73733-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="73733-123">Добавление ITRP из галереи hello</span><span class="sxs-lookup"><span data-stu-id="73733-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="73733-124">tooconfigure hello интеграции ITRP в tooAzure AD, вы должны tooadd ITRP из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="73733-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73733-125">**tooadd ITRP из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73733-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73733-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="73733-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73733-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="73733-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73733-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="73733-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="73733-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="73733-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="73733-133">Введите в поле поиска hello **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="73733-133">In hello search box, type **ITRP**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="73733-135">В панели результатов hello выберите **ITRP**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="73733-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73733-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73733-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="73733-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение ITRP с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73733-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="73733-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ITRP является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73733-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="73733-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в ITRP требуется toobe установлено.</span><span class="sxs-lookup"><span data-stu-id="73733-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="73733-141">В ITRP, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="73733-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73733-142">tooconfigure и теста Azure AD единого входа с ITRP, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="73733-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73733-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="73733-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73733-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="73733-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73733-145">**[Создание ITRP тестовый пользователь](#creating-an-itrp-test-user)**  -toohave аналог Саймон Britta в ITRP, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="73733-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73733-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="73733-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73733-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="73733-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73733-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73733-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73733-149">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настройки единого входа в ITRP приложения.</span><span class="sxs-lookup"><span data-stu-id="73733-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="73733-150">**tooconfigure Azure AD единого входа с ITRP, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73733-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="73733-151">В hello в hello портала Azure **ITRP** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="73733-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="73733-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="73733-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="73733-155">На hello **URL-адреса и домена ITRP** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="73733-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="73733-157">а.</span><span class="sxs-lookup"><span data-stu-id="73733-157">a.</span></span> <span data-ttu-id="73733-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="73733-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="73733-159">b.</span><span class="sxs-lookup"><span data-stu-id="73733-159">b.</span></span> <span data-ttu-id="73733-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="73733-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73733-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="73733-161">These values are not real.</span></span> <span data-ttu-id="73733-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="73733-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="73733-163">Обратитесь к [группа поддержки клиент ITRP](https://www.itrp.com/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="73733-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="73733-164">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="73733-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="73733-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="73733-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73733-168">На hello **конфигурации ITRP** щелкните **Настройка ITRP** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="73733-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="73733-169">Копировать hello **SAML единого входа URL-адрес службы и URL-адрес выхода** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="73733-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="73733-171">В другом окне браузера войти в корпоративный сайт ITRP tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="73733-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="73733-172">Щелкните hello панели инструментов в верхней части hello **параметры**.</span><span class="sxs-lookup"><span data-stu-id="73733-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="73733-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="73733-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="73733-174">В области навигации слева hello выберите **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="73733-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="73733-175">![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775571.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="73733-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="73733-176">В hello единым входом раздел конфигурации выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="73733-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="73733-177">![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775572.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="73733-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="73733-178">![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775573.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="73733-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="73733-179">а.</span><span class="sxs-lookup"><span data-stu-id="73733-179">a.</span></span> <span data-ttu-id="73733-180">Нажмите **Включить**.</span><span class="sxs-lookup"><span data-stu-id="73733-180">Click **Enable**.</span></span>

    <span data-ttu-id="73733-181">b.</span><span class="sxs-lookup"><span data-stu-id="73733-181">b.</span></span> <span data-ttu-id="73733-182">В **журнала ожидания URL-адрес удаленного** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="73733-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="73733-183">c.</span><span class="sxs-lookup"><span data-stu-id="73733-183">c.</span></span> <span data-ttu-id="73733-184">В **URL-адрес единого входа SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="73733-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="73733-185">d.In **отпечаток сертификата** текстовое поле, вставить hello **отпечаток** значение сертификат, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="73733-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="73733-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="73733-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="73733-187">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="73733-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73733-188">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="73733-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73733-189">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73733-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73733-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="73733-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="73733-191">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="73733-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="73733-193">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73733-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73733-194">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="73733-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73733-196">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="73733-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73733-198">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="73733-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73733-200">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="73733-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73733-202">а.</span><span class="sxs-lookup"><span data-stu-id="73733-202">a.</span></span> <span data-ttu-id="73733-203">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73733-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73733-204">b.</span><span class="sxs-lookup"><span data-stu-id="73733-204">b.</span></span> <span data-ttu-id="73733-205">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="73733-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73733-206">c.</span><span class="sxs-lookup"><span data-stu-id="73733-206">c.</span></span> <span data-ttu-id="73733-207">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="73733-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73733-208">d.</span><span class="sxs-lookup"><span data-stu-id="73733-208">d.</span></span> <span data-ttu-id="73733-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="73733-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="73733-210">Создание тестового пользователя ITRP</span><span class="sxs-lookup"><span data-stu-id="73733-210">Creating an ITRP test user</span></span>

<span data-ttu-id="73733-211">Пользователи toolog tooenable Azure AD в tooITRP, их необходимо подготовить в tooITRP.</span><span class="sxs-lookup"><span data-stu-id="73733-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="73733-212">В случае hello объекта ITRP Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="73733-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="73733-213">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73733-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="73733-214">Войдите в tooyour **ITRP** клиента.</span><span class="sxs-lookup"><span data-stu-id="73733-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="73733-215">Щелкните hello панели инструментов в верхней части hello **записи**.</span><span class="sxs-lookup"><span data-stu-id="73733-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="73733-216">![Администратор](./media/active-directory-saas-itrp-tutorial/ic775575.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="73733-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="73733-217">Hello всплывающего меню, выберите **людей**.</span><span class="sxs-lookup"><span data-stu-id="73733-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="73733-218">![Люди](./media/active-directory-saas-itrp-tutorial/ic775587.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="73733-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="73733-219">Нажмите **Добавить пользователя** ("+").</span><span class="sxs-lookup"><span data-stu-id="73733-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="73733-220">![Администратор](./media/active-directory-saas-itrp-tutorial/ic775576.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="73733-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="73733-221">В диалоговом окне добавления человека hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="73733-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="73733-222">![Пользователь](./media/active-directory-saas-itrp-tutorial/ic775577.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="73733-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="73733-223">а.</span><span class="sxs-lookup"><span data-stu-id="73733-223">a.</span></span> <span data-ttu-id="73733-224">Тип hello **имя**, **электронной почты** действительной учетной записи AAD, вы хотите tooprovision.</span><span class="sxs-lookup"><span data-stu-id="73733-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="73733-225">b.</span><span class="sxs-lookup"><span data-stu-id="73733-225">b.</span></span> <span data-ttu-id="73733-226">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="73733-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="73733-227">Можно использовать любые другие ITRP пользователя средства создания учетных записей или интерфейсы API, предоставляемые ITRP tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="73733-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="73733-228">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="73733-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="73733-229">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooITRP доступа.</span><span class="sxs-lookup"><span data-stu-id="73733-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="73733-231">**tooassign tooITRP Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73733-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="73733-232">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="73733-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="73733-234">В списке приложений hello выберите **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="73733-234">In hello applications list, select **ITRP**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="73733-236">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="73733-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="73733-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="73733-238">Click **Add** button.</span></span> <span data-ttu-id="73733-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="73733-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="73733-241">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="73733-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73733-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="73733-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73733-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="73733-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73733-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="73733-244">Testing single sign-on</span></span>

<span data-ttu-id="73733-245">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="73733-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73733-246">При нажатии кнопки ITRP плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour ITRP приложения.</span><span class="sxs-lookup"><span data-stu-id="73733-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="73733-247">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73733-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73733-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="73733-248">Additional resources</span></span>

* [<span data-ttu-id="73733-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73733-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73733-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73733-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

