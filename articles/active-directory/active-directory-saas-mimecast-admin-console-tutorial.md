---
title: "Учебник. Интеграция Azure Active Directory с консолью администрирования Mimecast | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и консоль администрирования Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="d6d9d-103">Учебник. Интеграция Azure Active Directory с консолью администрирования Mimecast</span><span class="sxs-lookup"><span data-stu-id="d6d9d-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="d6d9d-104">В этом учебнике вы узнаете, как toointegrate из консоли администрирования Mimecast с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6d9d-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6d9d-105">Интеграция консоль администрирования Mimecast с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d6d9d-106">Можно управлять в Azure AD, имеющего доступ tooMimecast консоли администрирования.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="d6d9d-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooMimecast консоли администрирования (Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="d6d9d-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d6d9d-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="d6d9d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6d9d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6d9d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d6d9d-110">Prerequisites</span></span>

<span data-ttu-id="d6d9d-111">tooconfigure интеграция Azure AD с помощью консоли администрирования Mimecast требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="d6d9d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d6d9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6d9d-113">Подписка на консоль администрирования Mimecast с поддержкой единого входа</span><span class="sxs-lookup"><span data-stu-id="d6d9d-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6d9d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6d9d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6d9d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6d9d-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6d9d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6d9d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d6d9d-118">Scenario description</span></span>
<span data-ttu-id="d6d9d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6d9d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6d9d-121">Добавление консоли администрирования Mimecast из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d6d9d-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="d6d9d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6d9d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="d6d9d-123">Добавление консоли администрирования Mimecast из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d6d9d-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="d6d9d-124">tooconfigure hello интеграция консоль администрирования Mimecast в Azure AD, вы должны tooadd консоль администрирования Mimecast из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d6d9d-125">**tooadd консоль администрирования Mimecast из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d6d9d-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6d9d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="d6d9d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d6d9d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="d6d9d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="d6d9d-133">Введите в поле поиска hello **консоль администрирования Mimecast**выберите **консоль администрирования Mimecast** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Консоль администрирования Mimecast в списке результатов hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d6d9d-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6d9d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d6d9d-136">В этом разделе описана настройка и проверка единого входа Azure AD в консоли администрирования Mimecast с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d6d9d-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в консоли администрирования Mimecast является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="d6d9d-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в консоли администрирования Mimecast должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="d6d9d-139">В консоли администрирования Mimecast, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d6d9d-140">tooconfigure и теста Azure AD единого входа с консоли администрирования Mimecast, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d6d9d-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d6d9d-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6d9d-143">**[Создание тестового пользователя консоли администрирования Mimecast](#create-a-mimecast-admin-console-test-user)**  -toohave аналог Саймон Britta в консоли администрирования Mimecast, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6d9d-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6d9d-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d6d9d-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6d9d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d6d9d-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="d6d9d-148">**tooconfigure Azure AD единого входа с помощью консоли администрирования Mimecast, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d6d9d-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6d9d-149">В hello в hello портала Azure **консоль администрирования Mimecast** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="d6d9d-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="d6d9d-153">На hello **URL-адреса и домена консоли администрирования Mimecast** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа консоли администрирования Mimecast](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="d6d9d-155">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="d6d9d-156">URL-адрес входа Hello имеет зависимости от региона.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="d6d9d-157">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="d6d9d-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d6d9d-159">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d6d9d-161">На hello **конфигурация консоли администрирования Mimecast** щелкните **настроить консоль администрирования Mimecast** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d6d9d-162">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="d6d9d-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка консоли администрирования Mimecast](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="d6d9d-164">В другом окне веб-браузера войдите в консоль администрирования Mimecast в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="d6d9d-165">Go слишком**службы \> приложения**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="d6d9d-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services") (Службы)</span><span class="sxs-lookup"><span data-stu-id="d6d9d-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="d6d9d-167">Щелкните **Профили проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="d6d9d-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles") (Профили аутентификации)</span><span class="sxs-lookup"><span data-stu-id="d6d9d-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="d6d9d-169">Щелкните **Новый профиль проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="d6d9d-170">![New Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profile") (Создать профиль аутентификации)</span><span class="sxs-lookup"><span data-stu-id="d6d9d-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="d6d9d-171">В hello **профиль проверки подлинности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="d6d9d-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile") (Профиль аутентификации)</span><span class="sxs-lookup"><span data-stu-id="d6d9d-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="d6d9d-173">а.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-173">a.</span></span> <span data-ttu-id="d6d9d-174">В hello **описание** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="d6d9d-175">b.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-175">b.</span></span> <span data-ttu-id="d6d9d-176">Выберите **Обязательное использование проверки подлинности SAML для консоли администрирования Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="d6d9d-177">c.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-177">c.</span></span> <span data-ttu-id="d6d9d-178">В поле **Provider** (Поставщик) выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="d6d9d-179">d.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-179">d.</span></span> <span data-ttu-id="d6d9d-180">Вставить **идентификатор сущности SAML**, которой копируются hello портал Azure в hello **URL-адрес издателя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="d6d9d-181">д.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-181">e.</span></span> <span data-ttu-id="d6d9d-182">Вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure hello в hello **URL-адрес входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="d6d9d-183">f.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-183">f.</span></span> <span data-ttu-id="d6d9d-184">Вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure hello в hello **URL-адрес выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="d6d9d-185">Hello значения URL-адрес входа и URL-адрес выхода hello предназначены для hello консоль администрирования Mimecast hello таким же.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="d6d9d-186">ж.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-186">g.</span></span> <span data-ttu-id="d6d9d-187">Откройте сертификат в base-64, загруженные из портала Azure в блокноте, удалите первую строку hello («*--*») и последнюю строку hello («*--*»), копирования hello, оставшихся в его содержимого в буфер обмена а затем вставьте его toohello **сертификат поставщика удостоверений (метаданные)** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="d6d9d-188">h.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-188">h.</span></span> <span data-ttu-id="d6d9d-189">Установите флажок **Разрешить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="d6d9d-190">i.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-190">i.</span></span> <span data-ttu-id="d6d9d-191">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d6d9d-192">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="d6d9d-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d6d9d-193">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d6d9d-194">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6d9d-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d6d9d-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6d9d-195">Create an Azure AD test user</span></span>

<span data-ttu-id="d6d9d-196">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="d6d9d-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d6d9d-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6d9d-199">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d6d9d-201">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d6d9d-203">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d6d9d-205">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d6d9d-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d6d9d-207">а.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-207">a.</span></span> <span data-ttu-id="d6d9d-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6d9d-209">b.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-209">b.</span></span> <span data-ttu-id="d6d9d-210">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d6d9d-211">c.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-211">c.</span></span> <span data-ttu-id="d6d9d-212">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d6d9d-213">d.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-213">d.</span></span> <span data-ttu-id="d6d9d-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="d6d9d-215">Создание тестового пользователя консоли администрирования Mimecast</span><span class="sxs-lookup"><span data-stu-id="d6d9d-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="d6d9d-216">В порядке tooenable toolog пользователей Azure AD в консоли администрирования Mimecast их необходимо подготовить в консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="d6d9d-217">В случае hello консоль администрирования Mimecast Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="d6d9d-218">Перед созданием пользователей необходимо tooregister домена.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="d6d9d-219">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d6d9d-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6d9d-220">Войдите на tooyour **консоль администрирования Mimecast** от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="d6d9d-221">Go слишком**каталогов \> внутренний**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="d6d9d-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories") (Каталоги)</span><span class="sxs-lookup"><span data-stu-id="d6d9d-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="d6d9d-223">Щелкните **Зарегистрировать новый домен**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="d6d9d-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain") (Зарегистрировать новый домен)</span><span class="sxs-lookup"><span data-stu-id="d6d9d-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="d6d9d-225">После создания нового домена щелкните **Новый адрес**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="d6d9d-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address") (Новый адрес)</span><span class="sxs-lookup"><span data-stu-id="d6d9d-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="d6d9d-227">В hello новый адрес диалогового окна выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="d6d9d-228">![Сохранить](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Сохранить")</span><span class="sxs-lookup"><span data-stu-id="d6d9d-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="d6d9d-229">а.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-229">a.</span></span> <span data-ttu-id="d6d9d-230">Тип hello **адрес электронной почты**, **глобальное имя**, **пароль**, и **подтверждение пароля** атрибуты допустимым Azure AD учетную запись, которую хотите текстовые поля, связанные с tooprovision в hello.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="d6d9d-231">b.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-231">b.</span></span> <span data-ttu-id="d6d9d-232">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="d6d9d-233">Можно использовать другие средства создания учетных записей пользователя консоли администрирования Mimecast или интерфейсы API, предоставляемые учетных записей пользователей Azure AD tooprovision консоль администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d6d9d-234">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d6d9d-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d6d9d-235">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooMimecast доступа к консоли администрирования.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="d6d9d-237">**tooassign tooMimecast Britta Simon консоли администрирования, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="d6d9d-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6d9d-238">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d6d9d-240">В списке приложений hello выберите **консоль администрирования Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![ссылка консоль администрирования Mimecast Hello в списке приложений hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="d6d9d-242">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="d6d9d-244">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-244">Click **Add** button.</span></span> <span data-ttu-id="d6d9d-245">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="d6d9d-247">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d6d9d-248">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6d9d-249">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d6d9d-250">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d6d9d-250">Test single sign-on</span></span>

<span data-ttu-id="d6d9d-251">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d6d9d-252">При нажатии кнопки hello консоль администрирования Mimecast плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на консоли администрирования Mimecast приложения.</span><span class="sxs-lookup"><span data-stu-id="d6d9d-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="d6d9d-253">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d6d9d-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d6d9d-254">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d6d9d-254">Additional resources</span></span>

* [<span data-ttu-id="d6d9d-255">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6d9d-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6d9d-256">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d6d9d-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

