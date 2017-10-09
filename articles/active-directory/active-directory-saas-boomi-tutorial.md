---
title: "Руководство по интеграции Azure Active Directory с Boomi | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="617dc-103">Руководство. Интеграция Azure Active Directory с Boomi</span><span class="sxs-lookup"><span data-stu-id="617dc-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="617dc-104">В этом учебнике вы узнаете, как toointegrate Boomi с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="617dc-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="617dc-105">Интеграция Boomi с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="617dc-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="617dc-106">Можно управлять в Azure AD, имеющего доступ tooBoomi</span><span class="sxs-lookup"><span data-stu-id="617dc-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="617dc-107">Можно включить на пользователей tooautomatically get вошедшего tooBoomi (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="617dc-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="617dc-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="617dc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="617dc-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="617dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="617dc-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="617dc-110">Prerequisites</span></span>

<span data-ttu-id="617dc-111">tooconfigure интеграция Azure AD с Boomi требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="617dc-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="617dc-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="617dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="617dc-113">Подписка с поддержкой единого входа Boomi</span><span class="sxs-lookup"><span data-stu-id="617dc-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="617dc-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="617dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="617dc-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="617dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="617dc-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="617dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="617dc-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="617dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="617dc-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="617dc-118">Scenario description</span></span>
<span data-ttu-id="617dc-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="617dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="617dc-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="617dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="617dc-121">Добавление Boomi из галереи hello</span><span class="sxs-lookup"><span data-stu-id="617dc-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="617dc-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="617dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="617dc-123">Добавление Boomi из галереи hello</span><span class="sxs-lookup"><span data-stu-id="617dc-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="617dc-124">tooconfigure hello интеграции Boomi в Azure AD, вы должны tooadd Boomi из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="617dc-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="617dc-125">**tooadd Boomi из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="617dc-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="617dc-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="617dc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="617dc-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="617dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="617dc-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="617dc-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="617dc-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="617dc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="617dc-133">Введите в поле поиска hello **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="617dc-133">In hello search box, type **Boomi**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="617dc-135">В панели результатов hello выберите **Boomi**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="617dc-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="617dc-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="617dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="617dc-138">В этом разделе описана настройка и проверка единого входа Azure AD в Boomi с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="617dc-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="617dc-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Boomi является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="617dc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="617dc-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Boomi должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="617dc-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="617dc-141">В Boomi, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="617dc-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="617dc-142">tooconfigure и теста Azure AD единого входа с Boomi, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="617dc-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="617dc-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="617dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="617dc-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="617dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="617dc-145">**[Создание тестового пользователя Boomi](#creating-a-boomi-test-user)**  -toohave аналог Саймон Britta в Boomi, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="617dc-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="617dc-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="617dc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="617dc-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="617dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="617dc-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="617dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="617dc-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Boomi приложения.</span><span class="sxs-lookup"><span data-stu-id="617dc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="617dc-150">**tooconfigure Azure AD единого входа с Boomi, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="617dc-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="617dc-151">В hello в hello портала Azure **Boomi** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="617dc-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="617dc-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="617dc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="617dc-155">На hello **URL-адреса и домена Boomi** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="617dc-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="617dc-157">а.</span><span class="sxs-lookup"><span data-stu-id="617dc-157">a.</span></span> <span data-ttu-id="617dc-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="617dc-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="617dc-159">b.</span><span class="sxs-lookup"><span data-stu-id="617dc-159">b.</span></span> <span data-ttu-id="617dc-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="617dc-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="617dc-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="617dc-161">These values are not real.</span></span> <span data-ttu-id="617dc-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="617dc-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="617dc-163">Обратитесь к [Boomi поддержки](https://boomi.com/company/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="617dc-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="617dc-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="617dc-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="617dc-166">Boomi приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="617dc-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="617dc-167">Выполните настройку следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="617dc-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="617dc-168">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="617dc-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="617dc-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="617dc-169">hello following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="617dc-171">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалоговое окно, для каждой строки, показано в следующей таблице hello выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="617dc-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="617dc-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="617dc-172">Attribute Name</span></span> | <span data-ttu-id="617dc-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="617dc-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="617dc-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="617dc-174">FEDERATION_ID</span></span> | <span data-ttu-id="617dc-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="617dc-175">user.mail</span></span> |
    
    <span data-ttu-id="617dc-176">а.</span><span class="sxs-lookup"><span data-stu-id="617dc-176">a.</span></span> <span data-ttu-id="617dc-177">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="617dc-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="617dc-180">b.</span><span class="sxs-lookup"><span data-stu-id="617dc-180">b.</span></span> <span data-ttu-id="617dc-181">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="617dc-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="617dc-182">c.</span><span class="sxs-lookup"><span data-stu-id="617dc-182">c.</span></span> <span data-ttu-id="617dc-183">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="617dc-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="617dc-184">d.</span><span class="sxs-lookup"><span data-stu-id="617dc-184">d.</span></span> <span data-ttu-id="617dc-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="617dc-185">Click **Ok**.</span></span>

6. <span data-ttu-id="617dc-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="617dc-186">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="617dc-188">На hello **конфигурации Boomi** щелкните **Настройка Boomi** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="617dc-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="617dc-189">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="617dc-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="617dc-191">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Boomi в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="617dc-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="617dc-192">Перейдите в слишком**название компании** и перейти слишком**Настройка**.</span><span class="sxs-lookup"><span data-stu-id="617dc-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="617dc-193">Нажмите кнопку hello **параметры единого входа** вкладку и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="617dc-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="617dc-195">а.</span><span class="sxs-lookup"><span data-stu-id="617dc-195">a.</span></span> <span data-ttu-id="617dc-196">Установите флажок **Enable SAML Single Sign-On** (Разрешить единый вход SAML).</span><span class="sxs-lookup"><span data-stu-id="617dc-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="617dc-197">b.</span><span class="sxs-lookup"><span data-stu-id="617dc-197">b.</span></span> <span data-ttu-id="617dc-198">Нажмите кнопку **импорта** tooupload hello загрузить сертификат из Azure AD слишком**сертификат поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="617dc-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="617dc-199">c.</span><span class="sxs-lookup"><span data-stu-id="617dc-199">c.</span></span> <span data-ttu-id="617dc-200">В hello **URL-адрес входа поставщика удостоверений** текстовое поле, помещение значения hello **SAML единого входа URL-адрес службы** из окна конфигурации приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="617dc-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="617dc-201">d.</span><span class="sxs-lookup"><span data-stu-id="617dc-201">d.</span></span> <span data-ttu-id="617dc-202">Для параметра **Federation Id Location** (Расположение идентификатора федерации) выберите переключатель **Federation Id is in FEDERATION_ID Attribute element** (Идентификатор федерации передается в элементе атрибута FEDERATION_ID).</span><span class="sxs-lookup"><span data-stu-id="617dc-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="617dc-203">д.</span><span class="sxs-lookup"><span data-stu-id="617dc-203">e.</span></span> <span data-ttu-id="617dc-204">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="617dc-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="617dc-205">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="617dc-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="617dc-206">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="617dc-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="617dc-207">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="617dc-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="617dc-208">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="617dc-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="617dc-209">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="617dc-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="617dc-211">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="617dc-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="617dc-212">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="617dc-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="617dc-214">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="617dc-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="617dc-216">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="617dc-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="617dc-218">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="617dc-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="617dc-220">а.</span><span class="sxs-lookup"><span data-stu-id="617dc-220">a.</span></span> <span data-ttu-id="617dc-221">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="617dc-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="617dc-222">b.</span><span class="sxs-lookup"><span data-stu-id="617dc-222">b.</span></span> <span data-ttu-id="617dc-223">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="617dc-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="617dc-224">c.</span><span class="sxs-lookup"><span data-stu-id="617dc-224">c.</span></span> <span data-ttu-id="617dc-225">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="617dc-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="617dc-226">d.</span><span class="sxs-lookup"><span data-stu-id="617dc-226">d.</span></span> <span data-ttu-id="617dc-227">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="617dc-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="617dc-228">Создание тестового пользователя Boomi</span><span class="sxs-lookup"><span data-stu-id="617dc-228">Creating a Boomi test user</span></span>

<span data-ttu-id="617dc-229">В порядке tooenable toolog пользователей Azure AD в tooBoomi их необходимо подготовить в Boomi.</span><span class="sxs-lookup"><span data-stu-id="617dc-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="617dc-230">В случае Boomi hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="617dc-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="617dc-231">tooprovision учетной записи пользователя, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="617dc-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="617dc-232">Войдите в систему tooyour сайт Boomi для компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="617dc-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="617dc-233">После входа в систему, перейдите слишком**Управление пользователями** и перейти слишком**пользователей**.</span><span class="sxs-lookup"><span data-stu-id="617dc-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="617dc-234">![Пользователи](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="617dc-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="617dc-235">Нажмите кнопку  **+**  значок и hello **добавить и настроить роли пользователей** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="617dc-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="617dc-236">![Пользователи](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="617dc-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="617dc-237">![Пользователи](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="617dc-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="617dc-238">а.</span><span class="sxs-lookup"><span data-stu-id="617dc-238">a.</span></span> <span data-ttu-id="617dc-239">В hello **адрес электронной почты пользователя** электронной почты hello тип пользователя в текстовое поле, например BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="617dc-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="617dc-240">b.</span><span class="sxs-lookup"><span data-stu-id="617dc-240">b.</span></span> <span data-ttu-id="617dc-241">В hello **имя** текстового поля, типа hello имя пользователя как Britta.</span><span class="sxs-lookup"><span data-stu-id="617dc-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="617dc-242">c.</span><span class="sxs-lookup"><span data-stu-id="617dc-242">c.</span></span> <span data-ttu-id="617dc-243">В hello **Фамилия** текстового поля, типа hello фамилию пользователя как Simon.</span><span class="sxs-lookup"><span data-stu-id="617dc-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="617dc-244">d.</span><span class="sxs-lookup"><span data-stu-id="617dc-244">d.</span></span> <span data-ttu-id="617dc-245">Введите пользователя hello **идентификатор федерации**.</span><span class="sxs-lookup"><span data-stu-id="617dc-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="617dc-246">Каждый пользователь должен иметь идентификатор федерации, который уникально идентифицирует hello в hello учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="617dc-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="617dc-247">д.</span><span class="sxs-lookup"><span data-stu-id="617dc-247">e.</span></span> <span data-ttu-id="617dc-248">Назначить hello **обычного пользователя** toohello пользователя роли.</span><span class="sxs-lookup"><span data-stu-id="617dc-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="617dc-249">Не назначайте hello роль администратора, поскольку это сообщило бы ему обычный доступ атмосферы, а также единого входа для доступа.</span><span class="sxs-lookup"><span data-stu-id="617dc-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="617dc-250">f.</span><span class="sxs-lookup"><span data-stu-id="617dc-250">f.</span></span> <span data-ttu-id="617dc-251">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="617dc-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="617dc-252">Hello пользователю не выдается приветствие уведомление по электронной почте содержащая пароль, который можно использовать toolog в toohello AtomSphere учетной записи, поскольку пароля осуществляется с помощью поставщика удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="617dc-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="617dc-253">Можно использовать любые другие Boomi пользователя средства создания учетных записей или интерфейсы API, предоставляемые Boomi tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="617dc-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="617dc-254">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="617dc-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="617dc-255">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBoomi доступа.</span><span class="sxs-lookup"><span data-stu-id="617dc-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="617dc-257">**tooassign tooBoomi Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="617dc-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="617dc-258">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="617dc-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="617dc-260">В списке приложений hello выберите **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="617dc-260">In hello applications list, select **Boomi**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="617dc-262">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="617dc-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="617dc-264">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="617dc-264">Click **Add** button.</span></span> <span data-ttu-id="617dc-265">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="617dc-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="617dc-267">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="617dc-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="617dc-268">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="617dc-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="617dc-269">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="617dc-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="617dc-270">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="617dc-270">Testing single sign-on</span></span>

<span data-ttu-id="617dc-271">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="617dc-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="617dc-272">При нажатии кнопки hello Boomi плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Boomi приложения.</span><span class="sxs-lookup"><span data-stu-id="617dc-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="617dc-273">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="617dc-273">Additional resources</span></span>

* [<span data-ttu-id="617dc-274">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="617dc-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="617dc-275">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="617dc-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

