---
title: "Руководство по интеграции Azure Active Directory с Adobe Creative Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Adobe Creative Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="8403c-103">Руководство по интеграции Azure Active Directory с Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="8403c-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="8403c-104">В этом учебнике вы узнаете, как toointegrate Adobe Creative Cloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8403c-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8403c-105">Интеграция с Azure AD Adobe Creative Cloud предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8403c-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8403c-106">Можно управлять в Azure AD, имеющего доступ tooAdobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="8403c-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="8403c-107">Ваш пользователей tooautomatically get вошедшего tooAdobe Creative Cloud (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8403c-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8403c-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="8403c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="8403c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8403c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8403c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8403c-110">Prerequisites</span></span>

<span data-ttu-id="8403c-111">tooconfigure интеграция Azure AD с Adobe Creative Cloud требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8403c-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="8403c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8403c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8403c-113">подписка Adobe Creative Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8403c-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8403c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8403c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8403c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8403c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8403c-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="8403c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8403c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8403c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8403c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8403c-118">Scenario description</span></span>
<span data-ttu-id="8403c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8403c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8403c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8403c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8403c-121">Добавление Adobe Creative Cloud из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8403c-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="8403c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8403c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="8403c-123">Добавление Adobe Creative Cloud из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8403c-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="8403c-124">tooconfigure hello интеграции Adobe Creative Cloud в Azure AD, вы должны tooadd Adobe Creative Cloud из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8403c-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8403c-125">**tooadd Adobe Creative Cloud из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8403c-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8403c-126">В hello ** [портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8403c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8403c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8403c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8403c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8403c-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8403c-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8403c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8403c-133">Введите в поле поиска hello **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="8403c-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="8403c-135">В панели результатов hello выберите **Adobe Creative Cloud**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8403c-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8403c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8403c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8403c-138">В этом разделе описана настройка и проверка единого входа Azure AD в Adobe Creative Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8403c-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8403c-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Adobe Creative Cloud является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8403c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="8403c-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Adobe Creative Cloud должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8403c-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="8403c-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="8403c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="8403c-142">tooconfigure и теста Azure AD единого входа с Adobe Creative Cloud, необходимо toocomplete hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="8403c-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8403c-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8403c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8403c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8403c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8403c-145">**[Создание тестового пользователя, прошедшего Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user) ** -toohave аналог Саймон Britta в Adobe Creative Cloud, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="8403c-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8403c-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8403c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8403c-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8403c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8403c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8403c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8403c-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="8403c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="8403c-150">**tooconfigure Azure AD единого входа с Adobe Creative Cloud, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8403c-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="8403c-151">На портале управления Azure hello на hello **Adobe Creative Cloud** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8403c-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8403c-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8403c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="8403c-155">На hello **Adobe Creative облака домена и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="8403c-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="8403c-157">а.</span><span class="sxs-lookup"><span data-stu-id="8403c-157">a.</span></span> <span data-ttu-id="8403c-158">В hello **идентификатор** текстовое поле, значение типа hello как:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="8403c-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="8403c-159">b.</span><span class="sxs-lookup"><span data-stu-id="8403c-159">b.</span></span> <span data-ttu-id="8403c-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="8403c-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8403c-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="8403c-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="8403c-162">У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8403c-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8403c-163">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8403c-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="8403c-164">Если вам требуется toocreate пользователя вручную, необходимо группа поддержки Adobe Creative Cloud toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="8403c-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="8403c-165">На hello **URL-адреса и Adobe Creative облака домена** выполните hello, выполните действия, при желании tooconfigure приложения hello в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="8403c-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="8403c-167">а.</span><span class="sxs-lookup"><span data-stu-id="8403c-167">a.</span></span> <span data-ttu-id="8403c-168">Щелкните hello **Показывать дополнительные параметры URL-адреса** параметр</span><span class="sxs-lookup"><span data-stu-id="8403c-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="8403c-169">b.</span><span class="sxs-lookup"><span data-stu-id="8403c-169">b.</span></span> <span data-ttu-id="8403c-170">В hello **URL-адрес входа** текстовое поле, значение типа hello как:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="8403c-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="8403c-171">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8403c-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="8403c-173">На hello **Adobe Creative конфигурации облака** щелкните **настроить Adobe Creative Cloud** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="8403c-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8403c-174">Скопируйте hello **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** из раздела краткий справочник.</span><span class="sxs-lookup"><span data-stu-id="8403c-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="8403c-176">В другом окне браузера, клиент Adobe Creative Cloud tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="8403c-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="8403c-177">Go слишком**удостоверение** hello левой панели навигации и щелкните свой домен.</span><span class="sxs-lookup"><span data-stu-id="8403c-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="8403c-178">Выполните hello, выполните действия **единого входа на конфигурации требуется** раздела.</span><span class="sxs-lookup"><span data-stu-id="8403c-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="8403c-179">![Параметры](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="8403c-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="8403c-180">Нажмите кнопку **Обзор** tooupload hello загрузить сертификат из Azure AD слишком**сертификат поставщика Удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="8403c-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="8403c-181">В hello **издатель IDP** текстовое поле, помещение значения hello **идентификатор сущности SAML** скопирован из **Настройка входа** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8403c-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="8403c-182">В hello **URL-адрес входа поставщика Удостоверений** текстовое поле, помещение значения hello **URL-адрес службы единого входа SAML** скопирован из **Настройка входа** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8403c-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="8403c-183">Для параметра **HTTP — Redirect** (Перенаправление HTTP) выберите вариант **IDP Binding** (Привязка к поставщику удостоверений).</span><span class="sxs-lookup"><span data-stu-id="8403c-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="8403c-184">Для параметра **Email Address** (Адрес электронной почты) выберите вариант **User Login Setting** (Настройки входа пользователя).</span><span class="sxs-lookup"><span data-stu-id="8403c-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="8403c-185">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8403c-185">Click **Save** button.</span></span>

15. <span data-ttu-id="8403c-186">панель мониторинга Hello теперь будет представлять hello XML **«Скачать метаданные»** файла.</span><span class="sxs-lookup"><span data-stu-id="8403c-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="8403c-187">Он содержит URL-адреса компании Adobe для описания сущности (EntityDescriptor) и URL-адреса службы утверждений (AssertionConsumerService).</span><span class="sxs-lookup"><span data-stu-id="8403c-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="8403c-188">Откройте файл hello и настроить их в hello приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8403c-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="8403c-191">а.</span><span class="sxs-lookup"><span data-stu-id="8403c-191">a.</span></span> <span data-ttu-id="8403c-192">Используйте hello EntityDescriptor значение Adobe следующие материалы для **идентификатор** на hello **Настройка параметров приложения** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8403c-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="8403c-193">b.</span><span class="sxs-lookup"><span data-stu-id="8403c-193">b.</span></span> <span data-ttu-id="8403c-194">Используйте hello AssertionConsumerService значение Adobe следующие материалы для **URL-адрес ответа** на hello **Настройка параметров приложения** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8403c-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8403c-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8403c-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="8403c-196">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8403c-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8403c-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8403c-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8403c-199">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8403c-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8403c-201">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="8403c-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8403c-203">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8403c-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8403c-205">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8403c-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8403c-207">а.</span><span class="sxs-lookup"><span data-stu-id="8403c-207">a.</span></span> <span data-ttu-id="8403c-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8403c-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8403c-209">b.</span><span class="sxs-lookup"><span data-stu-id="8403c-209">b.</span></span> <span data-ttu-id="8403c-210">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8403c-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8403c-211">c.</span><span class="sxs-lookup"><span data-stu-id="8403c-211">c.</span></span> <span data-ttu-id="8403c-212">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8403c-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8403c-213">d.</span><span class="sxs-lookup"><span data-stu-id="8403c-213">d.</span></span> <span data-ttu-id="8403c-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8403c-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="8403c-215">Создание тестового пользователя Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="8403c-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="8403c-216">В порядке tooenable toolog пользователей Azure AD в Adobe Creative Cloud их необходимо подготовить в Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="8403c-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="8403c-217">В случае hello Adobe Creative Cloud Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="8403c-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="8403c-218">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="8403c-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="8403c-219">Войдите в tooyour корпоративный сайт Adobe Creative Cloud с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8403c-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="8403c-220">Выберите параметр **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8403c-220">Click **People**.</span></span>

    <span data-ttu-id="8403c-221">![Люди](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="8403c-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="8403c-222">Нажмите кнопку **Пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8403c-222">Click **Invite User**.</span></span>

    <span data-ttu-id="8403c-223">![Приглашение пользователей](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "приглашение пользователей")</span><span class="sxs-lookup"><span data-stu-id="8403c-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="8403c-224">На hello **пригласить пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8403c-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="8403c-225">![Приглашение участников](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="8403c-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="8403c-226">а.</span><span class="sxs-lookup"><span data-stu-id="8403c-226">a.</span></span> <span data-ttu-id="8403c-227">В hello **электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8403c-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="8403c-228">b.</span><span class="sxs-lookup"><span data-stu-id="8403c-228">b.</span></span> <span data-ttu-id="8403c-229">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="8403c-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8403c-230">Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="8403c-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8403c-231">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8403c-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8403c-232">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooAdobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="8403c-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8403c-234">**tooassign tooAdobe Britta Simon Creative Cloud выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="8403c-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="8403c-235">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8403c-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8403c-237">В списке приложений hello выберите **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="8403c-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="8403c-239">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8403c-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8403c-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8403c-241">Click **Add** button.</span></span> <span data-ttu-id="8403c-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8403c-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8403c-244">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8403c-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8403c-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8403c-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8403c-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8403c-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8403c-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8403c-247">Testing single sign-on</span></span>

<span data-ttu-id="8403c-248">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8403c-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8403c-249">При выборе плитки Adobe Creative Cloud hello в hello панели доступа, следует получать автоматически вошедшего tooyour Adobe Creative облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="8403c-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8403c-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8403c-250">Additional resources</span></span>

* [<span data-ttu-id="8403c-251">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8403c-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8403c-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8403c-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png