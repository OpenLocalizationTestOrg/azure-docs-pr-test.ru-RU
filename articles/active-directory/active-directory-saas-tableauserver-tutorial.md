---
title: "Руководство по интеграции Azure Active Directory с Tableau Server | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Tableau сервером."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="7f4d2-103">Учебник. Интеграция Azure Active Directory с Tableau Server</span><span class="sxs-lookup"><span data-stu-id="7f4d2-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="7f4d2-104">В этом учебнике вы узнаете, как toointegrate Tableau Server в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f4d2-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f4d2-105">Интеграция сервера Tableau с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7f4d2-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7f4d2-106">Можно управлять в Azure AD, имеющего доступ tooTableau сервера</span><span class="sxs-lookup"><span data-stu-id="7f4d2-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="7f4d2-107">Можно включить на пользователей tooautomatically get вошедшего tooTableau сервера (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f4d2-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f4d2-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7f4d2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7f4d2-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f4d2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f4d2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7f4d2-110">Prerequisites</span></span>

<span data-ttu-id="7f4d2-111">tooconfigure интеграция Azure AD с сервером Tableau, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7f4d2-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="7f4d2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7f4d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f4d2-113">подписка Tableau Server с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f4d2-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f4d2-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7f4d2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f4d2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f4d2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f4d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f4d2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7f4d2-118">Scenario description</span></span>
<span data-ttu-id="7f4d2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f4d2-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7f4d2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f4d2-121">Добавление сервера Tableau из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7f4d2-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="7f4d2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f4d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="7f4d2-123">Добавление сервера Tableau из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7f4d2-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="7f4d2-124">tooconfigure hello интеграции Tableau Server в Azure AD, вы должны tooadd Tableau сервера из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7f4d2-125">**tooadd Tableau сервера из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="7f4d2-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f4d2-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7f4d2-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7f4d2-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7f4d2-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7f4d2-133">Введите в поле поиска hello **Tableau сервера**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-133">In hello search box, type **Tableau Server**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="7f4d2-135">В панели результатов hello, выберите **сервера Tableau**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7f4d2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f4d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7f4d2-138">В этом разделе описана настройка и проверка единого входа Azure AD в Tableau Server для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7f4d2-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Tableau Server является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="7f4d2-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей на сервере Tableau должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="7f4d2-141">В сервере Tableau, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7f4d2-142">tooconfigure и теста Azure AD единого входа с сервера Tableau, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7f4d2-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7f4d2-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7f4d2-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f4d2-145">**[Создание тестового пользователя сервера Tableau](#creating-a-tableau-server-test-user)**  -toohave аналог Саймон Britta Server Tableau, которое представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f4d2-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f4d2-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7f4d2-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f4d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7f4d2-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Tableau серверное приложение.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="7f4d2-150">**tooconfigure Azure AD единого входа с сервером Tableau, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f4d2-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f4d2-151">В hello в hello портала Azure **сервера Tableau** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7f4d2-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="7f4d2-155">На hello **URL-адреса и доменом сервера Tableau** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f4d2-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="7f4d2-157">а.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-157">a.</span></span> <span data-ttu-id="7f4d2-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="7f4d2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="7f4d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-159">b.</span></span> <span data-ttu-id="7f4d2-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="7f4d2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="7f4d2-161">c.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-161">c.</span></span> <span data-ttu-id="7f4d2-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="7f4d2-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7f4d2-163">Hello выше значения не реальные значения.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-163">hello preceding values are not real values.</span></span> <span data-ttu-id="7f4d2-164">Более поздней версии обновляются значениями hello hello фактический URL-адрес и идентификатор, на странице конфигурации сервера Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="7f4d2-165">Tableau серверное приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7f4d2-166">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="7f4d2-167">Вы можете управлять hello значения этих атрибутов из hello **«Атрибуты пользователя»** раздел на странице интеграции приложений.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="7f4d2-168">Hello следующем снимке экрана показан пример для hello же.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="7f4d2-170">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7f4d2-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7f4d2-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="7f4d2-171">Attribute Name</span></span> | <span data-ttu-id="7f4d2-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="7f4d2-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="7f4d2-173">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="7f4d2-173">username</span></span> | <span data-ttu-id="7f4d2-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="7f4d2-174">*user.displayname*</span></span> |

    <span data-ttu-id="7f4d2-175">а.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-175">a.</span></span> <span data-ttu-id="7f4d2-176">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="7f4d2-179">b.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-179">b.</span></span> <span data-ttu-id="7f4d2-180">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7f4d2-181">c.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-181">c.</span></span> <span data-ttu-id="7f4d2-182">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7f4d2-183">d.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-183">d.</span></span> <span data-ttu-id="7f4d2-184">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-184">Click **Ok**</span></span>


6. <span data-ttu-id="7f4d2-185">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="7f4d2-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7f4d2-187">Click **Save** button.</span></span>

    <span data-ttu-id="7f4d2-188">![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="7f4d2-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="7f4d2-189">tooget единого входа, настроенному для вашего приложения, необходимо клиента сервера Tableau tooyour toosign вход в систему с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="7f4d2-190">а.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-190">a.</span></span> <span data-ttu-id="7f4d2-191">В конфигурации сервера Tableau hello, щелкните hello **SAML** вкладки.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="7f4d2-193">b.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-193">b.</span></span> <span data-ttu-id="7f4d2-194">Установка флажка hello **использование SAML для единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="7f4d2-195">c.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-195">c.</span></span> <span data-ttu-id="7f4d2-196">URL-адрес возврата tableau сервера — URL-адрес, Tableau сервер пользователи будут получать доступ к, таких как http://tableau_server hello.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="7f4d2-197">Мы не рекомендуем использовать http://localhost.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="7f4d2-198">URL-адреса с конечной косой чертой (например http://tableau_server/) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="7f4d2-199">Копировать **URL-адрес возврата сервера Tableau** и вставьте его tooAzure AD **на URL-адрес входа** текстовое поле в **Tableau домена сервера и URL-адреса** раздела.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="7f4d2-200">d.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-200">d.</span></span> <span data-ttu-id="7f4d2-201">Идентификатор сущности SAML — идентификатор сущности hello однозначно определяет ваш сервер Tableau установки toohello поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="7f4d2-202">Можно ввести URL-адрес сервера Tableau еще раз, при необходимости, но он не имеет toobe Tableau URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="7f4d2-203">Копировать **идентификатор сущности SAML** и вставьте его tooAzure AD **идентификатор** текстовое поле в **Tableau домена сервера и URL-адреса** раздела.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="7f4d2-204">д.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-204">e.</span></span> <span data-ttu-id="7f4d2-205">Нажмите кнопку hello **экспорт метаданных файла** и откройте его в приложение hello текстового редактора.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="7f4d2-206">Найдите URL-адрес службы утверждения потребителя с Http Post и индексом 0, а также копировать hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="7f4d2-207">Теперь вставьте tooAzure AD **URL-адрес ответа** текстовое поле в **URL-адреса и доменом сервера Tableau** раздела.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="7f4d2-208">f.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-208">f.</span></span> <span data-ttu-id="7f4d2-209">Найдите файл метаданных федерации, Скачанный с портала Azure, а затем передать его в hello **файл метаданных поставщика удостоверений SAML**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="7f4d2-210">ж.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-210">g.</span></span> <span data-ttu-id="7f4d2-211">Нажмите кнопку hello **ОК** кнопки странице конфигурации сервера Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="7f4d2-212">Клиент имеет tooupload сертификаты в конфигурации единого входа SAML Server Tableau hello и может получить пропущена в hello потока единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="7f4d2-213">Если требуется справка настройки SAML на сервере Tableau затем см. в статье toothis [Настройка SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="7f4d2-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="7f4d2-214">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7f4d2-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7f4d2-215">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7f4d2-216">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f4d2-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7f4d2-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f4d2-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="7f4d2-218">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7f4d2-220">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f4d2-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f4d2-221">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f4d2-223">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f4d2-225">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7f4d2-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f4d2-227">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f4d2-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f4d2-229">а.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-229">a.</span></span> <span data-ttu-id="7f4d2-230">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f4d2-231">b.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-231">b.</span></span> <span data-ttu-id="7f4d2-232">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f4d2-233">c.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-233">c.</span></span> <span data-ttu-id="7f4d2-234">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7f4d2-235">d.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-235">d.</span></span> <span data-ttu-id="7f4d2-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="7f4d2-237">Создание тестового пользователя Tableau Server</span><span class="sxs-lookup"><span data-stu-id="7f4d2-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="7f4d2-238">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="7f4d2-239">Необходимо tooprovision всем пользователям hello hello Tableau server.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="7f4d2-240">Username hello пользователя должен соответствовать hello значение, которое вы настроили в Azure AD hello пользовательский атрибут **username**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="7f4d2-241">С hello правильное сопоставление интеграции hello должно работать [Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="7f4d2-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="7f4d2-242">Если вам требуется toocreate пользователя вручную, необходимы toocontact hello Tableau Server администратора в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7f4d2-243">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7f4d2-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7f4d2-244">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooTableau сервера.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7f4d2-246">**tooassign tooTableau Britta Simon сервера, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="7f4d2-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f4d2-247">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7f4d2-249">В списке приложений hello выберите **Tableau сервера**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="7f4d2-251">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7f4d2-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-253">Click **Add** button.</span></span> <span data-ttu-id="7f4d2-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7f4d2-256">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7f4d2-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f4d2-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7f4d2-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7f4d2-259">Testing single sign-on</span></span>

<span data-ttu-id="7f4d2-260">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7f4d2-261">При нажатии кнопки hello Tableau Server плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Tableau серверного приложения.</span><span class="sxs-lookup"><span data-stu-id="7f4d2-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="7f4d2-262">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="7f4d2-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7f4d2-263">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7f4d2-263">Additional resources</span></span>

* [<span data-ttu-id="7f4d2-264">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f4d2-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f4d2-265">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f4d2-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

