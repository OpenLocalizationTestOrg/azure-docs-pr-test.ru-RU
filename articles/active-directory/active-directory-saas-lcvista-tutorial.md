---
title: "Руководство. Интеграция Azure Active Directory с LCVista | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="17c83-103">Руководство. Интеграция Azure Active Directory с LCVista</span><span class="sxs-lookup"><span data-stu-id="17c83-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="17c83-104">В этом учебнике вы узнаете, как toointegrate LCVista с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17c83-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17c83-105">Интеграция с Azure AD LCVista предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="17c83-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17c83-106">Можно управлять в Azure AD, имеющего доступ tooLCVista</span><span class="sxs-lookup"><span data-stu-id="17c83-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="17c83-107">Можно включить на пользователей tooautomatically get вошедшего tooLCVista (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c83-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17c83-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="17c83-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17c83-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17c83-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17c83-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="17c83-110">Prerequisites</span></span>

<span data-ttu-id="17c83-111">tooconfigure интеграция Azure AD с LCVista требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="17c83-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="17c83-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="17c83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17c83-113">подписка LCVista с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="17c83-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17c83-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="17c83-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17c83-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="17c83-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17c83-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="17c83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17c83-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17c83-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17c83-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="17c83-118">Scenario description</span></span>
<span data-ttu-id="17c83-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="17c83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17c83-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="17c83-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17c83-121">Добавление LCVista из галереи hello</span><span class="sxs-lookup"><span data-stu-id="17c83-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="17c83-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="17c83-123">Добавление LCVista из галереи hello</span><span class="sxs-lookup"><span data-stu-id="17c83-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="17c83-124">tooconfigure hello интеграции LCVista в Azure AD, вы должны tooadd LCVista из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="17c83-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17c83-125">**tooadd LCVista из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="17c83-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c83-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="17c83-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17c83-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="17c83-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17c83-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="17c83-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="17c83-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="17c83-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="17c83-133">Введите в поле поиска hello **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="17c83-133">In hello search box, type **LCVista**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="17c83-135">В панели результатов hello выберите **LCVista**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="17c83-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17c83-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c83-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17c83-138">В этом разделе описана настройка и проверка единого входа Azure AD в LCVista с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17c83-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17c83-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в LCVista является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17c83-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="17c83-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в LCVista должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="17c83-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="17c83-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в LCVista.</span><span class="sxs-lookup"><span data-stu-id="17c83-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="17c83-142">tooconfigure и теста Azure AD единого входа с LCVista, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="17c83-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17c83-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="17c83-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17c83-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="17c83-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17c83-145">**[Создание тестового пользователя LCVista](#creating-a-lcvista-test-user)**  -toohave аналог Саймон Britta в LCVista, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="17c83-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="17c83-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="17c83-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17c83-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="17c83-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17c83-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c83-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17c83-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LCVista.</span><span class="sxs-lookup"><span data-stu-id="17c83-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="17c83-150">**tooconfigure Azure AD единого входа с LCVista, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="17c83-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c83-151">В hello в hello портала Azure **LCVista** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="17c83-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="17c83-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="17c83-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="17c83-155">На hello **URL-адреса и домена LCVista** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="17c83-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="17c83-157">а.</span><span class="sxs-lookup"><span data-stu-id="17c83-157">a.</span></span> <span data-ttu-id="17c83-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="17c83-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="17c83-159">b.</span><span class="sxs-lookup"><span data-stu-id="17c83-159">b.</span></span> <span data-ttu-id="17c83-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="17c83-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="17c83-161">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="17c83-161">These values are not hello real.</span></span> <span data-ttu-id="17c83-162">Обновить значения hello фактический идентификатор и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="17c83-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="17c83-163">Обратитесь к [группа поддержки клиента LCVista](https://lcvista.com/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="17c83-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="17c83-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="17c83-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="17c83-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="17c83-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="17c83-168">На hello **конфигурации LCVista** щелкните **Настройка LCVista** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="17c83-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="17c83-169">Копировать hello **идентификатор сущности SAML** и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="17c83-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="17c83-171">Войдите на tooyour LCVista приложения от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="17c83-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="17c83-172">В hello **конфигурации SAML** статьи, проверьте hello **входа включить SAML** и введите сведения о hello, как упоминалось в под изображением.</span><span class="sxs-lookup"><span data-stu-id="17c83-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="17c83-174">а.</span><span class="sxs-lookup"><span data-stu-id="17c83-174">a.</span></span> <span data-ttu-id="17c83-175">Вставить hello **URL-адрес издателя** скопирован из Azure AD в hello **идентификатор сущности** раздела.</span><span class="sxs-lookup"><span data-stu-id="17c83-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="17c83-176">b.</span><span class="sxs-lookup"><span data-stu-id="17c83-176">b.</span></span> <span data-ttu-id="17c83-177">Вставить hello **единого входа URL-адрес службы** скопирован из Azure AD в hello **URL-адрес** раздела.</span><span class="sxs-lookup"><span data-stu-id="17c83-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="17c83-178">c.</span><span class="sxs-lookup"><span data-stu-id="17c83-178">c.</span></span> <span data-ttu-id="17c83-179">Из метаданных (XML) которого загруженный с портала Azure скопируйте значение hello **X509Certificate** и вставьте его в hello **x509 сертификатов** раздела.</span><span class="sxs-lookup"><span data-stu-id="17c83-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="17c83-180">d.</span><span class="sxs-lookup"><span data-stu-id="17c83-180">d.</span></span> <span data-ttu-id="17c83-181">В hello **атрибут имени** текстовое значение hello вставить `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="17c83-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="17c83-182">д.</span><span class="sxs-lookup"><span data-stu-id="17c83-182">e.</span></span> <span data-ttu-id="17c83-183">В hello **атрибут фамилии** текстовое значение hello вставить `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="17c83-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="17c83-184">f.</span><span class="sxs-lookup"><span data-stu-id="17c83-184">f.</span></span> <span data-ttu-id="17c83-185">В hello **атрибут адреса электронной почты** текстовое значение hello вставить `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="17c83-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="17c83-186">ж.</span><span class="sxs-lookup"><span data-stu-id="17c83-186">g.</span></span> <span data-ttu-id="17c83-187">В hello **атрибута Username** текстовое значение hello вставить `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="17c83-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="17c83-188">д.</span><span class="sxs-lookup"><span data-stu-id="17c83-188">e.</span></span> <span data-ttu-id="17c83-189">Нажмите кнопку **Сохранить** toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="17c83-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="17c83-190">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="17c83-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17c83-191">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="17c83-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17c83-192">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17c83-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17c83-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c83-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="17c83-194">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="17c83-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="17c83-196">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="17c83-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c83-197">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="17c83-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17c83-199">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="17c83-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17c83-201">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="17c83-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17c83-203">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="17c83-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17c83-205">а.</span><span class="sxs-lookup"><span data-stu-id="17c83-205">a.</span></span> <span data-ttu-id="17c83-206">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17c83-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17c83-207">b.</span><span class="sxs-lookup"><span data-stu-id="17c83-207">b.</span></span> <span data-ttu-id="17c83-208">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17c83-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17c83-209">c.</span><span class="sxs-lookup"><span data-stu-id="17c83-209">c.</span></span> <span data-ttu-id="17c83-210">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="17c83-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17c83-211">d.</span><span class="sxs-lookup"><span data-stu-id="17c83-211">d.</span></span> <span data-ttu-id="17c83-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="17c83-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="17c83-213">Создание тестового пользователя LCVista</span><span class="sxs-lookup"><span data-stu-id="17c83-213">Creating a LCVista test user</span></span>

<span data-ttu-id="17c83-214">В этом разделе описано, как создать пользователя Britta Simon в LCVista.</span><span class="sxs-lookup"><span data-stu-id="17c83-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="17c83-215">Требуется toocontact [группа поддержки клиента LCVista](https://lcvista.com/contact) tooadd пользователей hello в hello LCVista приложения.</span><span class="sxs-lookup"><span data-stu-id="17c83-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17c83-216">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="17c83-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17c83-217">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLCVista доступа.</span><span class="sxs-lookup"><span data-stu-id="17c83-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="17c83-219">**tooassign tooLCVista Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="17c83-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c83-220">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="17c83-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="17c83-222">В списке приложений hello выберите **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="17c83-222">In hello applications list, select **LCVista**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="17c83-224">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="17c83-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="17c83-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="17c83-226">Click **Add** button.</span></span> <span data-ttu-id="17c83-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="17c83-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="17c83-229">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="17c83-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17c83-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="17c83-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17c83-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="17c83-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17c83-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="17c83-232">Testing single sign-on</span></span>

<span data-ttu-id="17c83-233">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="17c83-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="17c83-234">Щелкните плитку LCVista hello в hello панели доступа, могут быть перенаправлены на страницу входа tooOrganization.</span><span class="sxs-lookup"><span data-stu-id="17c83-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="17c83-235">После успешного входа будет подписан на tooyour LCVista приложения.</span><span class="sxs-lookup"><span data-stu-id="17c83-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="17c83-236">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="17c83-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17c83-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="17c83-237">Additional resources</span></span>

* [<span data-ttu-id="17c83-238">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17c83-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17c83-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17c83-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

