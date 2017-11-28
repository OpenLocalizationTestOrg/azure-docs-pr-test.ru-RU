---
title: "Руководство по интеграции Azure Active Directory с ThousandEyes | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="0e2fe-103">Учебник. Интеграция Azure Active Directory с ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="0e2fe-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="0e2fe-104">В этом учебнике вы узнаете, как toointegrate ThousandEyes с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e2fe-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e2fe-105">Интеграция ThousandEyes с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e2fe-106">Можно управлять в Azure AD, имеющего доступ tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="0e2fe-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="0e2fe-107">Можно включить на пользователей tooautomatically get вошедшего tooThousandEyes (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e2fe-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e2fe-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0e2fe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e2fe-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e2fe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e2fe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0e2fe-110">Prerequisites</span></span>

<span data-ttu-id="0e2fe-111">tooconfigure интеграция Azure AD с ThousandEyes требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="0e2fe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0e2fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e2fe-113">подписка ThousandEyes с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e2fe-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e2fe-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e2fe-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e2fe-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e2fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e2fe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0e2fe-118">Scenario description</span></span>
<span data-ttu-id="0e2fe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e2fe-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e2fe-121">Добавление ThousandEyes из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0e2fe-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="0e2fe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e2fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="0e2fe-123">Добавление ThousandEyes из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0e2fe-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="0e2fe-124">tooconfigure hello интеграции ThousandEyes в Azure AD, вы должны tooadd ThousandEyes из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e2fe-125">**tooadd ThousandEyes из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0e2fe-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2fe-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e2fe-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e2fe-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0e2fe-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0e2fe-133">Введите в поле поиска hello **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="0e2fe-135">В панели результатов hello выберите **ThousandEyes**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e2fe-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e2fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e2fe-138">В этом разделе описана настройка и проверка единого входа Azure AD в ThousandEyes с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e2fe-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ThousandEyes является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="0e2fe-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ThousandEyes должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="0e2fe-141">В ThousandEyes, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e2fe-142">tooconfigure и теста Azure AD единого входа с ThousandEyes, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e2fe-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e2fe-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e2fe-145">**[Создание тестового пользователя ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave аналог Саймон Britta в ThousandEyes, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e2fe-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e2fe-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e2fe-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e2fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e2fe-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="0e2fe-150">**Azure AD tooconfigure единого входа с ThousandEyes, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0e2fe-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2fe-151">В hello в hello портала Azure **ThousandEyes** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0e2fe-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="0e2fe-155">На hello **URL-адреса и домена ThousandEyes** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="0e2fe-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="0e2fe-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="0e2fe-158">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="0e2fe-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0e2fe-160">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e2fe-162">На hello **конфигурации ThousandEyes** щелкните **Настройка ThousandEyes** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e2fe-163">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="0e2fe-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="0e2fe-165">В другом окне браузера, войдите на tooyour **ThousandEyes** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="0e2fe-166">В меню в верхней части hello hello выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="0e2fe-167">![Параметры](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="0e2fe-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="0e2fe-168">В нижней части страницы нажмите кнопку **Учетная запись**</span><span class="sxs-lookup"><span data-stu-id="0e2fe-168">Click **Account**</span></span>
   
    <span data-ttu-id="0e2fe-169">![Учетная запись](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Учетная запись")</span><span class="sxs-lookup"><span data-stu-id="0e2fe-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="0e2fe-170">Нажмите кнопку hello **безопасность и аутентификация** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="0e2fe-171">![Безопасность и проверка подлинности](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Безопасность и проверка подлинности")</span><span class="sxs-lookup"><span data-stu-id="0e2fe-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="0e2fe-172">В hello **настройки единого входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0e2fe-173">![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="0e2fe-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="0e2fe-174">а.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-174">a.</span></span> <span data-ttu-id="0e2fe-175">Выберите пункт **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="0e2fe-176">b.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-176">b.</span></span> <span data-ttu-id="0e2fe-177">В текстовое поле **Login Page URL** (URL-адрес страницы входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="0e2fe-178">c.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-178">c.</span></span> <span data-ttu-id="0e2fe-179">В текстовое поле **Logout Page URL** (URL-адрес выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="0e2fe-180">г)</span><span class="sxs-lookup"><span data-stu-id="0e2fe-180">d.</span></span> <span data-ttu-id="0e2fe-181">В текстовое поле **Identity Provider Issuer** (Издатель поставщика удостоверений) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="0e2fe-182">д.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-182">e.</span></span> <span data-ttu-id="0e2fe-183">В **сертификат проверки**, нажмите кнопку **выбрать файл**, а затем отправьте hello сертификат, загруженный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="0e2fe-184">f.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-184">f.</span></span> <span data-ttu-id="0e2fe-185">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="0e2fe-186">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="0e2fe-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e2fe-187">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e2fe-188">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e2fe-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e2fe-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e2fe-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e2fe-190">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0e2fe-192">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0e2fe-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2fe-193">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e2fe-195">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e2fe-197">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="0e2fe-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e2fe-199">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e2fe-201">а.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-201">a.</span></span> <span data-ttu-id="0e2fe-202">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e2fe-203">b.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-203">b.</span></span> <span data-ttu-id="0e2fe-204">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e2fe-205">c.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-205">c.</span></span> <span data-ttu-id="0e2fe-206">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e2fe-207">d.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-207">d.</span></span> <span data-ttu-id="0e2fe-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="0e2fe-209">Создание тестового пользователя ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="0e2fe-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="0e2fe-210">В порядке tooenable toolog пользователей Azure AD в ThousandEyes их необходимо подготовить в ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="0e2fe-211">В случае hello объекта ThousandEyes Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="0e2fe-212">Можно использовать любые другие ThousandEyes пользователя средства создания учетных записей или интерфейсы API, предоставляемые ThousandEyes tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="0e2fe-213">**tooprovision tooThousandEyes учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0e2fe-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2fe-214">Войдите на свой корпоративный веб-сайт ThousandEyes в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="0e2fe-215">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="0e2fe-216">![Параметры](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="0e2fe-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="0e2fe-217">Выберите раздел **Учетная запись**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-217">Click **Account**.</span></span>
   
    <span data-ttu-id="0e2fe-218">![Учетная запись](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Учетная запись")</span><span class="sxs-lookup"><span data-stu-id="0e2fe-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="0e2fe-219">Нажмите кнопку hello **учетные записи и пользователи** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="0e2fe-220">![Учетные записи и пользователи](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Учетные записи и пользователи")</span><span class="sxs-lookup"><span data-stu-id="0e2fe-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="0e2fe-221">В hello **Добавление пользователей и учетных записей** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0e2fe-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0e2fe-222">![Добавление учетных записей пользователей](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Добавление учетных записей пользователей")</span><span class="sxs-lookup"><span data-stu-id="0e2fe-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="0e2fe-223">а.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-223">a.</span></span> <span data-ttu-id="0e2fe-224">В **имя** в текстовое поле имя пользователя как типа hello **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="0e2fe-225">b.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-225">b.</span></span> <span data-ttu-id="0e2fe-226">В **электронной почты** электронной почты hello тип пользователя в текстовое поле, например  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="0e2fe-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="0e2fe-227">b.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-227">b.</span></span> <span data-ttu-id="0e2fe-228">Нажмите кнопку **tooAccount добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="0e2fe-229">Владелец учетной записи Azure Active Directory Hello будет отправлено электронное tooconfirm ссылку и активации учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0e2fe-230">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0e2fe-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0e2fe-231">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooThousandEyes доступа.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0e2fe-233">**tooassign tooThousandEyes Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0e2fe-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2fe-234">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0e2fe-236">В списке приложений hello выберите **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="0e2fe-238">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0e2fe-240">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-240">Click **Add** button.</span></span> <span data-ttu-id="0e2fe-241">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0e2fe-243">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e2fe-244">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e2fe-245">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e2fe-246">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0e2fe-246">Testing single sign-on</span></span>

<span data-ttu-id="0e2fe-247">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e2fe-248">При нажатии кнопки ThousandEyes плитки в панели доступа hello приветствия, вы должны получить tooyour автоматически подписан в приложение ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="0e2fe-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="0e2fe-249">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0e2fe-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e2fe-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0e2fe-250">Additional resources</span></span>

* [<span data-ttu-id="0e2fe-251">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e2fe-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e2fe-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e2fe-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

