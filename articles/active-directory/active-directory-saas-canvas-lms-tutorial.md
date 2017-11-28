---
title: "Руководство по интеграции Azure Active Directory с Canvas LMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Canvas LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="ea5af-103">Руководство по интеграции Azure Active Directory с Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="ea5af-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="ea5af-104">В этом учебнике вы узнаете, как toointegrate холст с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea5af-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea5af-105">Интеграция с Azure AD Canvas предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ea5af-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ea5af-106">Можно управлять в Azure AD, имеющего доступ tooCanvas</span><span class="sxs-lookup"><span data-stu-id="ea5af-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="ea5af-107">Можно включить на пользователей tooautomatically get вошедшего tooCanvas (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea5af-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea5af-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ea5af-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ea5af-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea5af-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea5af-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea5af-110">Prerequisites</span></span>

<span data-ttu-id="ea5af-111">tooconfigure интеграция Azure AD с Canvas, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ea5af-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="ea5af-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ea5af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea5af-113">подписка Canvas с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ea5af-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea5af-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ea5af-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea5af-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ea5af-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea5af-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ea5af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea5af-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea5af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea5af-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ea5af-118">Scenario description</span></span>
<span data-ttu-id="ea5af-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ea5af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea5af-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ea5af-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea5af-121">Добавление холст из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ea5af-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="ea5af-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea5af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="ea5af-123">Добавление холст из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ea5af-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="ea5af-124">tooconfigure hello интеграции холста в Azure AD, вы должны tooadd холст из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ea5af-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ea5af-125">**tooadd холст из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="ea5af-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea5af-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ea5af-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea5af-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ea5af-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ea5af-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ea5af-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ea5af-133">Введите в поле поиска hello **холст**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-133">In hello search box, type **Canvas**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="ea5af-135">В панели результатов hello выберите **холст**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ea5af-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea5af-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea5af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea5af-138">В этом разделе описана настройка и проверка единого входа Azure AD в Canvas с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea5af-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ea5af-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello на холсте является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea5af-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="ea5af-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей на холсте должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ea5af-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="ea5af-141">На холсте, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ea5af-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ea5af-142">tooconfigure и теста Azure AD единого входа с Canvas, необходимо hello toocomplete следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="ea5af-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ea5af-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ea5af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ea5af-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ea5af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea5af-145">**[Создание тестового пользователя холст](#creating-a-canvas-test-user)**  -toohave аналог Саймон Britta визуальный элемент, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ea5af-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea5af-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ea5af-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea5af-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ea5af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea5af-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea5af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea5af-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении холста.</span><span class="sxs-lookup"><span data-stu-id="ea5af-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="ea5af-150">**tooconfigure Azure AD единого входа с Canvas, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea5af-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea5af-151">В hello в hello портала Azure **холст** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ea5af-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ea5af-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="ea5af-155">На hello **URL-адреса и домена холст** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea5af-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="ea5af-157">а.</span><span class="sxs-lookup"><span data-stu-id="ea5af-157">a.</span></span> <span data-ttu-id="ea5af-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="ea5af-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="ea5af-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea5af-159">b.</span></span> <span data-ttu-id="ea5af-160">В hello **идентификатор** текстовое значение hello типа, используя следующий шаблон hello:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="ea5af-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea5af-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ea5af-161">These values are not real.</span></span> <span data-ttu-id="ea5af-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ea5af-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ea5af-163">Обратитесь к [группа поддержки клиент Canvas](https://community.canvaslms.com/community/help) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ea5af-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="ea5af-164">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="ea5af-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="ea5af-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ea5af-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea5af-168">На hello **холст конфигурации** щелкните **Настройка холст** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ea5af-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ea5af-169">Копировать hello **URL-адрес изменения пароля, URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ea5af-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="ea5af-171">В другом окне браузера войдите в tooyour сайте компании с Canvas в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ea5af-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="ea5af-172">Go слишком**курсы \> управляемых учетных записей \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="ea5af-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="ea5af-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="ea5af-174">Hello hello левой панели навигации выберите **проверки подлинности**, а затем нажмите кнопку **аутентификация**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="ea5af-175">![Аутентификация](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="ea5af-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="ea5af-176">На странице текущая интеграция hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ea5af-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ea5af-177">![Текущая интеграция](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Текущая интеграция")</span><span class="sxs-lookup"><span data-stu-id="ea5af-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="ea5af-178">а.</span><span class="sxs-lookup"><span data-stu-id="ea5af-178">a.</span></span> <span data-ttu-id="ea5af-179">В **идентификатор сущности поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5af-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ea5af-180">b.</span><span class="sxs-lookup"><span data-stu-id="ea5af-180">b.</span></span> <span data-ttu-id="ea5af-181">В **на URL-адрес** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5af-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="ea5af-182">c.</span><span class="sxs-lookup"><span data-stu-id="ea5af-182">c.</span></span> <span data-ttu-id="ea5af-183">В **журнала URL-адреса выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5af-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ea5af-184">d.</span><span class="sxs-lookup"><span data-stu-id="ea5af-184">d.</span></span> <span data-ttu-id="ea5af-185">В **ссылка для изменения пароля** текстовое значение hello вставить **URL-адрес изменения пароля** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5af-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ea5af-186">д.</span><span class="sxs-lookup"><span data-stu-id="ea5af-186">e.</span></span> <span data-ttu-id="ea5af-187">В **отпечаток сертификата** текстовое поле, вставить hello **отпечаток** значение сертификата, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5af-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="ea5af-188">f.</span><span class="sxs-lookup"><span data-stu-id="ea5af-188">f.</span></span> <span data-ttu-id="ea5af-189">Из hello **входа атрибут** выберите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="ea5af-190">ж.</span><span class="sxs-lookup"><span data-stu-id="ea5af-190">g.</span></span> <span data-ttu-id="ea5af-191">Из hello **формат идентификатора** выберите **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="ea5af-192">h.</span><span class="sxs-lookup"><span data-stu-id="ea5af-192">h.</span></span> <span data-ttu-id="ea5af-193">Нажмите кнопку **Сохранить параметры проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="ea5af-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ea5af-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ea5af-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ea5af-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ea5af-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea5af-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea5af-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea5af-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea5af-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5af-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ea5af-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea5af-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea5af-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ea5af-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea5af-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea5af-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ea5af-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea5af-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea5af-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea5af-209">а.</span><span class="sxs-lookup"><span data-stu-id="ea5af-209">a.</span></span> <span data-ttu-id="ea5af-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea5af-211">b.</span><span class="sxs-lookup"><span data-stu-id="ea5af-211">b.</span></span> <span data-ttu-id="ea5af-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ea5af-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea5af-213">c.</span><span class="sxs-lookup"><span data-stu-id="ea5af-213">c.</span></span> <span data-ttu-id="ea5af-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ea5af-215">d.</span><span class="sxs-lookup"><span data-stu-id="ea5af-215">d.</span></span> <span data-ttu-id="ea5af-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="ea5af-217">Создание тестового пользователя Canvas</span><span class="sxs-lookup"><span data-stu-id="ea5af-217">Creating a Canvas test user</span></span>

<span data-ttu-id="ea5af-218">Пользователи toolog tooenable Azure AD в tooCanvas, их необходимо подготовить в Canvas.</span><span class="sxs-lookup"><span data-stu-id="ea5af-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="ea5af-219">В случае Canvas подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="ea5af-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="ea5af-220">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea5af-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea5af-221">Войдите в tooyour **холст** клиента.</span><span class="sxs-lookup"><span data-stu-id="ea5af-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="ea5af-222">Go слишком**курсы \> управляемых учетных записей \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="ea5af-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="ea5af-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="ea5af-224">Выберите раздел **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-224">Click **Users**.</span></span>
   
   <span data-ttu-id="ea5af-225">![Пользователи](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="ea5af-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="ea5af-226">Нажмите кнопку **Add New User**(Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="ea5af-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="ea5af-227">![Пользователи](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="ea5af-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="ea5af-228">На hello добавить диалоговое окно нового пользователя выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ea5af-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="ea5af-229">![Добавление пользователя](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="ea5af-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="ea5af-230">а.</span><span class="sxs-lookup"><span data-stu-id="ea5af-230">a.</span></span> <span data-ttu-id="ea5af-231">В hello **полное имя** текстовом поле введите имя пользователя, такие как hello **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="ea5af-232">b.</span><span class="sxs-lookup"><span data-stu-id="ea5af-232">b.</span></span> <span data-ttu-id="ea5af-233">В hello **электронной почты** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ea5af-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="ea5af-234">c.</span><span class="sxs-lookup"><span data-stu-id="ea5af-234">c.</span></span> <span data-ttu-id="ea5af-235">В hello **входа** текстовом поле введите адрес электронной почты пользователя hello Azure AD как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ea5af-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="ea5af-236">d.</span><span class="sxs-lookup"><span data-stu-id="ea5af-236">d.</span></span> <span data-ttu-id="ea5af-237">Выберите **пользователя hello по электронной почте о создании этой учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="ea5af-238">д.</span><span class="sxs-lookup"><span data-stu-id="ea5af-238">e.</span></span> <span data-ttu-id="ea5af-239">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="ea5af-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="ea5af-240">Можно использовать любые другие холст пользователя средства создания учетных записей или интерфейсы API, предоставляемые холст tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="ea5af-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ea5af-241">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ea5af-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ea5af-242">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooCanvas доступа.</span><span class="sxs-lookup"><span data-stu-id="ea5af-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ea5af-244">**tooassign tooCanvas Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea5af-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea5af-245">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ea5af-247">В списке приложений hello выберите **холст**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-247">In hello applications list, select **Canvas**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="ea5af-249">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ea5af-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-251">Click **Add** button.</span></span> <span data-ttu-id="ea5af-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ea5af-254">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ea5af-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ea5af-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea5af-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ea5af-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea5af-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ea5af-257">Testing single sign-on</span></span>

<span data-ttu-id="ea5af-258">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ea5af-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ea5af-259">При выборе плитки холст hello в hello панели доступа, вы должны получить приложения tooyour автоматически подписан на холсте.</span><span class="sxs-lookup"><span data-stu-id="ea5af-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="ea5af-260">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ea5af-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea5af-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ea5af-261">Additional resources</span></span>

* [<span data-ttu-id="ea5af-262">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea5af-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea5af-263">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ea5af-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

