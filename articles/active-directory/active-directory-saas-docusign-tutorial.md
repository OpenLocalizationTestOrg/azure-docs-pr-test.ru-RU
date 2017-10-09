---
title: "Учебник. Интеграция Azure Active Directory с DocuSign | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="bdc8a-103">Учебник. Интеграция Azure Active Directory с DocuSign</span><span class="sxs-lookup"><span data-stu-id="bdc8a-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="bdc8a-104">В этом учебнике вы узнаете, как toointegrate DocuSign с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdc8a-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdc8a-105">Интеграция DocuSign с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bdc8a-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bdc8a-106">Можно управлять в Azure AD, имеющего доступ tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="bdc8a-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="bdc8a-107">Можно включить на пользователей tooautomatically get вошедшего tooDocuSign (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdc8a-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bdc8a-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bdc8a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bdc8a-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdc8a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdc8a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bdc8a-110">Prerequisites</span></span>

<span data-ttu-id="bdc8a-111">tooconfigure интеграция Azure AD с DocuSign требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="bdc8a-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="bdc8a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bdc8a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdc8a-113">подписка DocuSign с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdc8a-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdc8a-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="bdc8a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdc8a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdc8a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdc8a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdc8a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bdc8a-118">Scenario description</span></span>
<span data-ttu-id="bdc8a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdc8a-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="bdc8a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdc8a-121">Добавление DocuSign из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bdc8a-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="bdc8a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdc8a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="bdc8a-123">Добавление DocuSign из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bdc8a-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="bdc8a-124">tooconfigure hello интеграции DocuSign в Azure AD, вы должны tooadd DocuSign из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bdc8a-125">**tooadd DocuSign из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bdc8a-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc8a-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bdc8a-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bdc8a-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bdc8a-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="bdc8a-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bdc8a-133">Введите в поле поиска hello **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-133">In hello search box, type **DocuSign**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="bdc8a-135">В панели результатов hello выберите **DocuSign**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdc8a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdc8a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdc8a-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение DocuSign с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bdc8a-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в DocuSign является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="bdc8a-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в DocuSign должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="bdc8a-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в DocuSign.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="bdc8a-142">tooconfigure и теста Azure AD единого входа с DocuSign, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bdc8a-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bdc8a-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bdc8a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdc8a-145">**[Создание тестового пользователя DocuSign](#creating-a-docusign-test-user)**  -toohave аналог Саймон Britta в DocuSign, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bdc8a-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdc8a-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdc8a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdc8a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bdc8a-149">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настройки единого входа в DocuSign приложения.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="bdc8a-150">**Azure AD tooconfigure единого входа с DocuSign, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bdc8a-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc8a-151">В hello в hello портала Azure **DocuSign** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bdc8a-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="bdc8a-155">На hello **сертификат подписи SAML** щелкните **сертификат (Base 64)** и затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="bdc8a-157">На hello **DocuSign конфигурации** части портала Azure щелкните **Настройка DocuSign** tooopen Настройка входа окна.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="bdc8a-158">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="bdc8a-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="bdc8a-160">В другом окне браузера, tooyour входа **портал администратора DocuSign** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="bdc8a-161">В меню навигации hello слева hello, щелкните **домены**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Настройка единого входа][51]

7. <span data-ttu-id="bdc8a-163">На правой панели hello щелкните **домена утверждения**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Настройка единого входа][52]

8. <span data-ttu-id="bdc8a-165">На hello **утверждения домена** диалогового окна в hello **доменное имя** текстовом поле введите домен компании и нажмите кнопку **утверждения**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="bdc8a-166">Убедитесь, что проверка домена hello и находится в активном состоянии hello.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Настройка единого входа][53]

9. <span data-ttu-id="bdc8a-168">В меню слева hello щелкните **Поставщики удостоверений**</span><span class="sxs-lookup"><span data-stu-id="bdc8a-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Настройка единого входа][54]
10. <span data-ttu-id="bdc8a-170">Hello правой панели щелкните **Добавление поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Настройка единого входа][55]

11. <span data-ttu-id="bdc8a-172">На hello **параметры поставщика удостоверений** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bdc8a-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Настройка единого входа][56]

    <span data-ttu-id="bdc8a-174">а.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-174">a.</span></span> <span data-ttu-id="bdc8a-175">В hello **имя** текстовом поле введите уникальное имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="bdc8a-176">Не используйте пробелы.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-176">Do not use spaces.</span></span>

    <span data-ttu-id="bdc8a-177">b.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-177">b.</span></span> <span data-ttu-id="bdc8a-178">Вставить **идентификатор сущности SAML** в hello **издатель поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="bdc8a-179">c.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-179">c.</span></span> <span data-ttu-id="bdc8a-180">Вставить **SAML единого входа URL-адрес службы** в hello **URL-адрес входа поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="bdc8a-181">d.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-181">d.</span></span> <span data-ttu-id="bdc8a-182">Вставить **URL-адрес выхода** в hello **URL-адрес выхода поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="bdc8a-183">д.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-183">e.</span></span> <span data-ttu-id="bdc8a-184">Выберите **Sign AuthN Request**(Подпись запроса авторизации).</span><span class="sxs-lookup"><span data-stu-id="bdc8a-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="bdc8a-185">Е.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-185">f.</span></span> <span data-ttu-id="bdc8a-186">Для параметра **Send AuthN request by** (Как отправлять запрос авторизации) выберите значение **POST**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="bdc8a-187">g.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-187">g.</span></span> <span data-ttu-id="bdc8a-188">Для параметра **Send logout request by** (Как отправлять запрос на выход) выберите значение **GET**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="bdc8a-189">В hello **сопоставление настраиваемый атрибут** выберите поле hello требуется toomap с утверждением Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="bdc8a-190">В этом примере hello **emailaddress** утверждения сопоставляется со значением hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="bdc8a-191">Это имя утверждения по умолчанию hello из Azure AD для утверждений электронной почты.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="bdc8a-192">Используйте hello соответствующие **идентификатор пользователя** toomap hello пользователя из Azure AD tooDocuSign пользователя сопоставления.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="bdc8a-193">Выберите hello соответствующие поля и введите соответствующее значение hello на основе заданных параметров организации.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Настройка единого входа][57]

13. <span data-ttu-id="bdc8a-195">В hello **сертификат поставщика удостоверений** щелкните **Добавление сертификата**, а затем отправьте hello сертификат, загруженный с портала Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Настройка единого входа][58]

14. <span data-ttu-id="bdc8a-197">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-197">Click **Save**.</span></span>

15. <span data-ttu-id="bdc8a-198">В hello **Поставщики удостоверений** щелкните **действия**, а затем нажмите кнопку **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Настройка единого входа][59]
 
16. <span data-ttu-id="bdc8a-200">В hello **Просмотр SAML 2.0 конечных точек** статьи на **портал администратора DocuSign**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bdc8a-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Настройка единого входа][60]
   
    <span data-ttu-id="bdc8a-202">а.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-202">a.</span></span> <span data-ttu-id="bdc8a-203">Hello копирования **URL-адрес издателя поставщика службы**и вставьте в hello **идентификатор** текстового поля на **URL-адреса и домена DocuSign** раздел hello Azure портала следующие hello шаблон: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="bdc8a-204">b.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-204">b.</span></span> <span data-ttu-id="bdc8a-205">Hello копирования **URL-адрес входа поставщика службы**и вставьте в hello **на URL-адрес входа** текстового поля на **URL-адреса и домена DocuSign** раздел hello Azure портала следующие hello шаблон: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="bdc8a-207">c.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-207">c.</span></span>  <span data-ttu-id="bdc8a-208">В нижней части страницы нажмите кнопку **Close**</span><span class="sxs-lookup"><span data-stu-id="bdc8a-208">Click **Close**</span></span>
    
17. <span data-ttu-id="bdc8a-209">Щелкните hello портал Azure, **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="bdc8a-211">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="bdc8a-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bdc8a-212">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bdc8a-213">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdc8a-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdc8a-214">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdc8a-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdc8a-215">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bdc8a-217">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bdc8a-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc8a-218">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bdc8a-220">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bdc8a-222">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bdc8a-224">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bdc8a-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bdc8a-226">а.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-226">a.</span></span> <span data-ttu-id="bdc8a-227">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdc8a-228">b.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-228">b.</span></span> <span data-ttu-id="bdc8a-229">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bdc8a-230">c.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-230">c.</span></span> <span data-ttu-id="bdc8a-231">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bdc8a-232">d.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-232">d.</span></span> <span data-ttu-id="bdc8a-233">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="bdc8a-234">Создание тестового пользователя DocuSign</span><span class="sxs-lookup"><span data-stu-id="bdc8a-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="bdc8a-235">Приложение поддерживает **непосредственно в время подготовки пользователей** и после проверки подлинности пользователей автоматически создаются в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bdc8a-236">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bdc8a-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bdc8a-237">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooDocuSign доступа.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bdc8a-239">**tooassign tooDocuSign Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bdc8a-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc8a-240">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bdc8a-242">В списке приложений hello выберите **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-242">In hello applications list, select **DocuSign**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="bdc8a-244">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bdc8a-246">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-246">Click **Add** button.</span></span> <span data-ttu-id="bdc8a-247">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bdc8a-249">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bdc8a-250">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdc8a-251">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bdc8a-252">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bdc8a-252">Testing single sign-on</span></span>

<span data-ttu-id="bdc8a-253">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bdc8a-254">При нажатии кнопки hello DocuSign плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour DocuSign.</span><span class="sxs-lookup"><span data-stu-id="bdc8a-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="bdc8a-255">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdc8a-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bdc8a-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bdc8a-256">Additional resources</span></span>

* [<span data-ttu-id="bdc8a-257">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdc8a-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdc8a-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bdc8a-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bdc8a-259">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="bdc8a-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

