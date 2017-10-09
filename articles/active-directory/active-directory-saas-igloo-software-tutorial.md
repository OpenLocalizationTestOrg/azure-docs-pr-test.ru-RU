---
title: "Учебник. Интеграция Azure Active Directory с Igloo Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="06516-103">Учебник. Интеграция Azure Active Directory с Igloo Software</span><span class="sxs-lookup"><span data-stu-id="06516-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="06516-104">В этом учебнике вы узнаете, как toointegrate Igloo Software с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06516-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06516-105">Интеграция Igloo Software с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="06516-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="06516-106">Можно управлять в Azure AD, имеющего доступ tooIgloo программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="06516-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="06516-107">Можно включить на пользователей tooautomatically get вошедшего tooIgloo программного обеспечения (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="06516-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06516-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="06516-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="06516-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="06516-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06516-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="06516-110">Prerequisites</span></span>

<span data-ttu-id="06516-111">tooconfigure интеграция Azure AD с Igloo Software необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="06516-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="06516-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="06516-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06516-113">подписка Igloo Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="06516-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06516-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="06516-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06516-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="06516-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06516-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="06516-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06516-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06516-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06516-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="06516-118">Scenario description</span></span>
<span data-ttu-id="06516-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="06516-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06516-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="06516-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06516-121">Добавление Igloo Software из галереи hello</span><span class="sxs-lookup"><span data-stu-id="06516-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="06516-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="06516-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="06516-123">Добавление Igloo Software из галереи hello</span><span class="sxs-lookup"><span data-stu-id="06516-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="06516-124">tooconfigure hello интеграции Igloo Software в Azure AD, вы должны tooadd Igloo Software из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="06516-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="06516-125">**tooadd Igloo Software из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="06516-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="06516-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="06516-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06516-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="06516-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="06516-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="06516-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="06516-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="06516-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="06516-133">Введите в поле поиска hello **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="06516-133">In hello search box, type **Igloo Software**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="06516-135">В панели результатов hello выберите **Igloo Software**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="06516-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06516-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="06516-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06516-138">В этом разделе описана настройка и проверка единого входа Azure AD в Igloo Software для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06516-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="06516-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Igloo Software является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06516-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="06516-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Igloo Software должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="06516-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="06516-141">В Igloo Software, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="06516-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="06516-142">tooconfigure и теста Azure AD единого входа с Igloo Software, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="06516-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="06516-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="06516-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="06516-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="06516-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06516-145">**[Создание тестового пользователя, прошедшего Igloo Software](#creating-an-igloo-software-test-user)**  -toohave аналог Саймон Britta в Igloo Software, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="06516-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="06516-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="06516-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06516-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="06516-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06516-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="06516-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06516-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="06516-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="06516-150">**tooconfigure Azure AD единого входа с Igloo Software, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="06516-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="06516-151">В hello в hello портала Azure **Igloo Software** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="06516-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="06516-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="06516-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="06516-155">На hello **URL-адреса и домена программного обеспечения Igloo** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="06516-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="06516-157">а.</span><span class="sxs-lookup"><span data-stu-id="06516-157">a.</span></span> <span data-ttu-id="06516-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="06516-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="06516-159">b.</span><span class="sxs-lookup"><span data-stu-id="06516-159">b.</span></span> <span data-ttu-id="06516-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="06516-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="06516-161">c.</span><span class="sxs-lookup"><span data-stu-id="06516-161">c.</span></span> <span data-ttu-id="06516-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="06516-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06516-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="06516-163">These values are not real.</span></span> <span data-ttu-id="06516-164">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="06516-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="06516-165">Обратитесь к [Igloo клиентское программное обеспечение поддержки](https://www.igloosoftware.com/services/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="06516-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="06516-166">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="06516-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="06516-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="06516-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="06516-170">На hello **конфигурации программного обеспечения Igloo** щелкните **Настройка Igloo Software** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="06516-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="06516-171">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="06516-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="06516-173">В другом окне браузера Войдите на сайте компании Igloo Software tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="06516-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="06516-174">Go toohello **панели управления**.</span><span class="sxs-lookup"><span data-stu-id="06516-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="06516-175">![Панель управления](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Панель управления")</span><span class="sxs-lookup"><span data-stu-id="06516-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="06516-176">В hello **членства** щелкните **параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="06516-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="06516-177">![Параметры входа](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Параметры входа")</span><span class="sxs-lookup"><span data-stu-id="06516-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="06516-178">В hello раздел конфигурации SAML, нажмите кнопку **Настройка проверки подлинности SAML**.</span><span class="sxs-lookup"><span data-stu-id="06516-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="06516-179">![Настройка SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="06516-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="06516-180">В hello **Общая конфигурация** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="06516-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="06516-181">![Общая конфигурация](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "Общая конфигурация")</span><span class="sxs-lookup"><span data-stu-id="06516-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="06516-182">а.</span><span class="sxs-lookup"><span data-stu-id="06516-182">a.</span></span> <span data-ttu-id="06516-183">В hello **имя подключения** текстовом поле введите имя файла для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="06516-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="06516-184">b.</span><span class="sxs-lookup"><span data-stu-id="06516-184">b.</span></span> <span data-ttu-id="06516-185">В hello **URL-адрес входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="06516-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="06516-186">c.</span><span class="sxs-lookup"><span data-stu-id="06516-186">c.</span></span> <span data-ttu-id="06516-187">В hello **URL-адрес выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="06516-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="06516-188">d.</span><span class="sxs-lookup"><span data-stu-id="06516-188">d.</span></span> <span data-ttu-id="06516-189">Для параметра **Тип HTTP запроса и ответа о выходе** укажите значение **POST**.</span><span class="sxs-lookup"><span data-stu-id="06516-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="06516-190">д.</span><span class="sxs-lookup"><span data-stu-id="06516-190">e.</span></span> <span data-ttu-id="06516-191">Откройте ваш **base-64** закодированный сертификат в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **открытый сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="06516-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="06516-192">В hello **Настройка ответа и аутентификации**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="06516-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="06516-193">![Конфигурация ответа и проверки подлинности](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Конфигурация ответа и проверки подлинности")</span><span class="sxs-lookup"><span data-stu-id="06516-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="06516-194">а.</span><span class="sxs-lookup"><span data-stu-id="06516-194">a.</span></span> <span data-ttu-id="06516-195">Выберите для параметра **Поставщик удостоверений** значение **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="06516-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="06516-196">b.</span><span class="sxs-lookup"><span data-stu-id="06516-196">b.</span></span> <span data-ttu-id="06516-197">Выберите для параметра **Тип идентификатора** значение **Адрес электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="06516-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="06516-198">c.</span><span class="sxs-lookup"><span data-stu-id="06516-198">c.</span></span> <span data-ttu-id="06516-199">В hello **атрибут адреса электронной почты** введите **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="06516-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="06516-200">d.</span><span class="sxs-lookup"><span data-stu-id="06516-200">d.</span></span> <span data-ttu-id="06516-201">В hello **атрибут имени** введите **givenname**.</span><span class="sxs-lookup"><span data-stu-id="06516-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="06516-202">д.</span><span class="sxs-lookup"><span data-stu-id="06516-202">e.</span></span> <span data-ttu-id="06516-203">В hello **атрибут фамилии** введите **Фамилия**.</span><span class="sxs-lookup"><span data-stu-id="06516-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="06516-204">Выполните hello следующая конфигурация hello toocomplete действия.</span><span class="sxs-lookup"><span data-stu-id="06516-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="06516-205">![Создание пользователя при входе](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Создание пользователя при входе")</span><span class="sxs-lookup"><span data-stu-id="06516-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="06516-206">а.</span><span class="sxs-lookup"><span data-stu-id="06516-206">a.</span></span> <span data-ttu-id="06516-207">Выберите для параметра **Создание пользователя при входе** значение **Создать нового пользователя на веб-сайте при входе**.</span><span class="sxs-lookup"><span data-stu-id="06516-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="06516-208">b.</span><span class="sxs-lookup"><span data-stu-id="06516-208">b.</span></span> <span data-ttu-id="06516-209">Выберите для параметра **Параметры входа** значение **Использовать кнопку SAML на экране входа**.</span><span class="sxs-lookup"><span data-stu-id="06516-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="06516-210">c.</span><span class="sxs-lookup"><span data-stu-id="06516-210">c.</span></span> <span data-ttu-id="06516-211">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="06516-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="06516-212">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="06516-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="06516-213">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="06516-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="06516-214">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06516-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06516-215">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="06516-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="06516-216">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="06516-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="06516-218">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="06516-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="06516-219">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="06516-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06516-221">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="06516-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06516-223">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="06516-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06516-225">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="06516-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06516-227">а.</span><span class="sxs-lookup"><span data-stu-id="06516-227">a.</span></span> <span data-ttu-id="06516-228">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06516-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06516-229">b.</span><span class="sxs-lookup"><span data-stu-id="06516-229">b.</span></span> <span data-ttu-id="06516-230">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="06516-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06516-231">c.</span><span class="sxs-lookup"><span data-stu-id="06516-231">c.</span></span> <span data-ttu-id="06516-232">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="06516-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="06516-233">d.</span><span class="sxs-lookup"><span data-stu-id="06516-233">d.</span></span> <span data-ttu-id="06516-234">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="06516-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="06516-235">Создание тестового пользователя Igloo Software</span><span class="sxs-lookup"><span data-stu-id="06516-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="06516-236">Нет элемента действия для вас tooconfigure подготовки пользователей tooIgloo программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="06516-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="06516-237">Когда назначенный пользователь пытается toolog в tooIgloo программного обеспечения с помощью панели доступа hello, Igloo Software проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="06516-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="06516-238">Если учетная запись пользователя отсутствует, Igloo Software автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="06516-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="06516-239">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="06516-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="06516-240">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooIgloo программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="06516-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="06516-242">**tooassign tooIgloo Britta Simon программное обеспечение, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="06516-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="06516-243">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="06516-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="06516-245">В списке приложений hello выберите **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="06516-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="06516-247">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="06516-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="06516-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="06516-249">Click **Add** button.</span></span> <span data-ttu-id="06516-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="06516-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="06516-252">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="06516-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="06516-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="06516-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06516-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="06516-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06516-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="06516-255">Testing single sign-on</span></span>

<span data-ttu-id="06516-256">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="06516-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="06516-257">При выборе плитки Igloo Software hello в hello панели доступа, вы должны получить приложения автоматически вошедшего tooyour Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="06516-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="06516-258">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06516-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06516-259">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="06516-259">Additional resources</span></span>

* [<span data-ttu-id="06516-260">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06516-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06516-261">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="06516-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

