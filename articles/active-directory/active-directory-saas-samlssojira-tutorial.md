---
title: "Руководство по интеграции Azure Active Directory с SAML SSO for Jira by resolution GmbH | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и единого входа SAML для Jira методом GmbH разрешения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="3a9f3-103">Руководство по интеграции Azure Active Directory с SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="3a9f3-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="3a9f3-104">В этом учебнике вы узнаете, как toointegrate единого входа SAML для Jira постановлением GmbH с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a9f3-105">Интеграция единого входа SAML для Jira постановлением GmbH с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3a9f3-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3a9f3-106">Можно управлять в Azure AD, имеющим доступ tooSAML единого входа с разрешением GmbH Jira</span><span class="sxs-lookup"><span data-stu-id="3a9f3-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="3a9f3-107">Можно включить на пользователей tooautomatically get вошедшего tooSAML единого входа для Jira, разрешение GmbH (Single Sign-On) с использованием их учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a9f3-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a9f3-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3a9f3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3a9f3-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a9f3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3a9f3-110">Prerequisites</span></span>

<span data-ttu-id="3a9f3-111">tooconfigure интеграция Azure AD с помощью единого входа SAML для Jira постановлением GmbH требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3a9f3-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="3a9f3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3a9f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a9f3-113">подписка SAML SSO for Jira by resolution GmbH с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a9f3-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a9f3-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3a9f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a9f3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a9f3-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a9f3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3a9f3-118">Scenario description</span></span>
<span data-ttu-id="3a9f3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a9f3-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3a9f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a9f3-121">Добавление единого входа SAML для Jira путем разрешения GmbH из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3a9f3-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="3a9f3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a9f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="3a9f3-123">Добавление единого входа SAML для Jira путем разрешения GmbH из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3a9f3-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="3a9f3-124">tooconfigure hello интеграции единого входа SAML для Jira постановлением GmbH в Azure AD, необходимо tooadd единого входа SAML для Jira постановлением GmbH из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3a9f3-125">**tooadd единого входа SAML для Jira постановлением GmbH из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3a9f3-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a9f3-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a9f3-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3a9f3-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3a9f3-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3a9f3-133">Введите в поле поиска hello **единого входа SAML для Jira постановлением GmbH**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="3a9f3-135">В панели результатов hello выберите **единого входа SAML для Jira постановлением GmbH**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a9f3-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a9f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a9f3-138">В этом разделе описана настройка и проверка единого входа Azure AD в SAML SSO for Jira by resolution GmbH с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3a9f3-139">Для единого входа toowork Azure AD необходима tooknow пользователя аналог какие hello в единый вход SAML для Jira постановлением GmbH является tooa пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="3a9f3-140">Другими словами связи между пользователя Azure AD и связанных пользователей в единый вход SAML для Jira постановлением hello GmbH должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="3a9f3-141">В единый вход SAML для Jira постановлением GmbH, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3a9f3-142">tooconfigure и выполнить проверку Azure AD единого входа с помощью единого входа SAML Jira методом GmbH разрешения, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3a9f3-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3a9f3-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a9f3-145">**[Создание единого входа SAML для Jira теста пользователем разрешение GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave аналог Саймон Britta в единый вход SAML для Jira постановлением GmbH, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a9f3-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a9f3-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a9f3-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a9f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a9f3-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей единого входа SAML для Jira постановлением GmbH приложения.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="3a9f3-150">**tooconfigure Azure AD единого входа с помощью единого входа SAML для Jira постановлением GmbH, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3a9f3-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a9f3-151">В hello в hello портала Azure **единого входа SAML для Jira постановлением GmbH** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3a9f3-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="3a9f3-155">На hello **единого входа SAML Jira постановлением GmbH доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="3a9f3-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="3a9f3-157">а.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-157">a.</span></span> <span data-ttu-id="3a9f3-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="3a9f3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="3a9f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-159">b.</span></span> <span data-ttu-id="3a9f3-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="3a9f3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="3a9f3-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="3a9f3-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="3a9f3-162">При необходимости приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="3a9f3-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="3a9f3-164">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="3a9f3-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3a9f3-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-165">These values are not real.</span></span> <span data-ttu-id="3a9f3-166">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3a9f3-167">Обратитесь к [поддержки единого входа SAML для Jira постановлением GmbH клиента](https://www.resolution.de/go/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="3a9f3-168">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="3a9f3-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3a9f3-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3a9f3-172">В другом окне браузера, войдите в tooyour **единого входа SAML для Jira с портала администрирования GmbH разрешение** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="3a9f3-173">Наведите указатель мыши на шестеренки и выберите hello **надстройки**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="3a9f3-175">Все страницы перенаправленный tooAdministrator доступа.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="3a9f3-176">Введите hello **пароль** и нажмите кнопку **Подтверждение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="3a9f3-178">На вкладке "Add-ons" (Надстройки) щелкните **Find new add-ons** (Найти новые надстройки).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="3a9f3-179">Поиск **SAML единого входа (SSO) для JIRA** и нажмите кнопку **установить** tooinstall кнопку hello нового подключаемого модуля SAML.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="3a9f3-181">Установка подключаемого модуля Hello начнется.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-181">hello plugin installation will start.</span></span> <span data-ttu-id="3a9f3-182">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="3a9f3-182">Click **Close**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="3a9f3-185">Нажмите кнопку **Управление**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-185">Click **Manage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="3a9f3-187">Нажмите кнопку **Настройка** tooconfigure hello нового подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="3a9f3-189">На **конфигурации подключаемый модуль единого входа SAML** щелкните **Добавление дополнительного поставщика удостоверений** кнопку tooconfigure hello параметры поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="3a9f3-191">На этой странице сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-191">Perform following steps on this page:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="3a9f3-193">а.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-193">a.</span></span> <span data-ttu-id="3a9f3-194">Добавить **имя** из hello поставщика удостоверений (например, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="3a9f3-195">b.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-195">b.</span></span> <span data-ttu-id="3a9f3-196">Добавить **описание** из hello поставщика удостоверений (например, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="3a9f3-197">c.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-197">c.</span></span> <span data-ttu-id="3a9f3-198">Нажмите кнопку **XML** и выберите hello **метаданные** файл, загруженный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="3a9f3-199">d.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-199">d.</span></span> <span data-ttu-id="3a9f3-200">Нажмите кнопку **Load** (Загрузить).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-200">Click **Load** button.</span></span>

    <span data-ttu-id="3a9f3-201">д.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-201">e.</span></span> <span data-ttu-id="3a9f3-202">Считывает метаданные поставщика удостоверений hello и заполняет поля hello, как показано на снимке экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="3a9f3-203">Нажмите кнопку **сохранить параметры** кнопку Параметры toosave hello.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-203">Click **Save settings** button toosave hello settings.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="3a9f3-205">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3a9f3-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3a9f3-206">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3a9f3-207">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a9f3-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a9f3-208">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a9f3-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a9f3-209">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3a9f3-211">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3a9f3-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a9f3-212">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a9f3-214">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a9f3-216">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="3a9f3-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a9f3-218">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3a9f3-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a9f3-220">а.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-220">a.</span></span> <span data-ttu-id="3a9f3-221">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a9f3-222">b.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-222">b.</span></span> <span data-ttu-id="3a9f3-223">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a9f3-224">c.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-224">c.</span></span> <span data-ttu-id="3a9f3-225">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3a9f3-226">d.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-226">d.</span></span> <span data-ttu-id="3a9f3-227">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="3a9f3-228">Создание тестового пользователя SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="3a9f3-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="3a9f3-229">Пользователи toolog tooenable Azure AD в tooSAML единого входа для Jira постановлением GmbH, их необходимо подготовить в единый вход SAML для Jira методом GmbH разрешения.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="3a9f3-230">Подготовка в SAML SSO for Jira by resolution GmbH выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="3a9f3-231">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3a9f3-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a9f3-232">Войдите в tooyour единого входа SAML для Jira путем разрешения GmbH корпоративный сайт с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="3a9f3-233">Наведите указатель мыши на шестеренки и выберите hello **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-233">Hover on cog and click hello **User management**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="3a9f3-235">Являются tooenter страницы доступ перенаправленной tooAdministrator **пароль** и нажмите кнопку **Подтверждение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="3a9f3-237">В разделе **User management** (Управление пользователями) щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-237">Under **User management** tab section, click **create user**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="3a9f3-239">На hello **«Создать пользователя»** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3a9f3-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="3a9f3-241">а.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-241">a.</span></span> <span data-ttu-id="3a9f3-242">В hello **адрес электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3a9f3-243">b.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-243">b.</span></span> <span data-ttu-id="3a9f3-244">В hello **полное имя** текстовое поле, полное имя типа пользователя hello как Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="3a9f3-245">c.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-245">c.</span></span> <span data-ttu-id="3a9f3-246">В hello **Username** электронной почты hello тип пользователя в текстовое поле, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3a9f3-247">d.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-247">d.</span></span> <span data-ttu-id="3a9f3-248">В hello **пароль** текстового поля, типа hello пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="3a9f3-249">д.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-249">e.</span></span> <span data-ttu-id="3a9f3-250">Щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3a9f3-251">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3a9f3-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3a9f3-252">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAML единого входа для Jira методом GmbH разрешения.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3a9f3-254">**tooassign tooSAML Britta Simon единого входа для Jira постановлением GmbH, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="3a9f3-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a9f3-255">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3a9f3-257">В списке приложений hello выберите **единого входа SAML для Jira постановлением GmbH**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="3a9f3-259">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3a9f3-261">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-261">Click **Add** button.</span></span> <span data-ttu-id="3a9f3-262">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3a9f3-264">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3a9f3-265">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a9f3-266">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a9f3-267">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3a9f3-267">Testing single sign-on</span></span>

<span data-ttu-id="3a9f3-268">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3a9f3-269">При нажатии кнопки hello единого входа SAML для Jira путем разрешения GmbH плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour единого входа SAML для Jira постановлением GmbH приложения.</span><span class="sxs-lookup"><span data-stu-id="3a9f3-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="3a9f3-270">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a9f3-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3a9f3-271">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3a9f3-271">Additional resources</span></span>

* [<span data-ttu-id="3a9f3-272">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a9f3-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a9f3-273">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a9f3-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

