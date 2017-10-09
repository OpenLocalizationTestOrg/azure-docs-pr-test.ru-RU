---
title: "Руководство по интеграции Azure Active Directory с Cezanne HR Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Cezanne HR программного обеспечения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="6f3c9-103">Руководство по интеграции Azure Active Directory с Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="6f3c9-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="6f3c9-104">В этом учебнике вы узнаете, как toointegrate Cezanne HR программного обеспечения в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f3c9-105">Интеграция Cezanne HR программного обеспечения в Azure AD предоставляет следующие преимущества hello.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="6f3c9-106">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-106">You can:</span></span>

- <span data-ttu-id="6f3c9-107">Управление Azure AD, имеющего доступ tooCezanne HR программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="6f3c9-108">Включите tooautomatically пользователей при входе в tooCezanne HR программного обеспечения с помощью единого входа (SSO) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6f3c9-109">Управление учетными записями в одном централизованном месте: hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="6f3c9-110">toolearn Дополнительные сведения о программное обеспечение как услуга (SaaS) интеграции приложений с Azure AD, в разделе [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f3c9-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6f3c9-111">Prerequisites</span></span>

<span data-ttu-id="6f3c9-112">tooconfigure интеграция Azure AD с Cezanne HR программного обеспечения необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="6f3c9-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6f3c9-113">An Azure AD subscription</span></span>
- <span data-ttu-id="6f3c9-114">подписка Cezanne HR Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f3c9-115">tootest hello шаги в этом учебнике, рекомендуется не использовать рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="6f3c9-116">tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="6f3c9-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f3c9-118">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f3c9-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6f3c9-119">Scenario description</span></span>
<span data-ttu-id="6f3c9-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="6f3c9-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="6f3c9-122">Добавление программного обеспечения Cezanne HR из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6f3c9-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="6f3c9-123">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="6f3c9-124">Добавление Cezanne HR программного обеспечения из библиотеки hello</span><span class="sxs-lookup"><span data-stu-id="6f3c9-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="6f3c9-125">Интеграция hello tooconfigure Cezanne HR программного обеспечения в Azure AD, добавить Cezanne HR программного обеспечения из hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f3c9-126">tooadd Cezanne HR программного обеспечения из галереи hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="6f3c9-127">В hello  **[портал Azure](https://portal.azure.com)**в левой области hello, выберите hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![Кнопка «Azure Active Directory» Hello][1]

2. <span data-ttu-id="6f3c9-129">Щелкните **Корпоративные приложения** > **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Здравствуйте, «Все приложения» ссылки][2]
    
3. <span data-ttu-id="6f3c9-131">новое приложение hello верхней части hello tooadd **все приложения** выберите **новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    ![Здравствуйте, «Новое приложение» кнопки][3]

4. <span data-ttu-id="6f3c9-133">Введите в поле поиска hello **программного обеспечения HR Cezanne**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![поле поиска Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="6f3c9-135">В списке результатов hello выберите **программного обеспечения HR Cezanne** , а затем выберите hello **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![список результатов Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6f3c9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3c9-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6f3c9-138">В этом разделе описано, как настроить и проверить единый вход Azure AD в Cezanne HR Software с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6f3c9-139">Для toowork единого входа Azure AD необходима hello tooknow Cezanne HR аналог программного обеспечения toohello пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="6f3c9-140">Другими словами необходимо установить связи между пользователя Azure AD и связанных пользователей hello в hello Cezanne HR программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="6f3c9-141">tooestablish hello связи, hello назначения программного обеспечения Cezanne HR **имя пользователя** значение как hello Azure AD **Username** значение.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="6f3c9-142">tooconfigure и Azure AD SSO с помощью программного обеспечения Cezanne HR, полный hello следующие стандартные блоки тестов.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="6f3c9-143">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3c9-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="6f3c9-144">В этом разделе можно включить единый вход Azure AD в hello портал Azure и настройки единого входа в приложении Cezanne HR программного обеспечения, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="6f3c9-145">В hello в hello портала Azure **программного обеспечения HR Cezanne** странице интеграции приложений выберите **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Здравствуйте, команда «Единый вход»][4]

2. <span data-ttu-id="6f3c9-147">tooenable единого входа, в hello **единого входа** диалоговое окно, выберите hello **режим** как **входа на базе SAML**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![поле «Режим» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="6f3c9-149">В разделе **URL-адреса и домена программного обеспечения HR Cezanne**, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![Hello раздел «Cezanne HR программного обеспечения доменов и URL-адреса»](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="6f3c9-151">а.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-151">a.</span></span> <span data-ttu-id="6f3c9-152">В hello **URL-адрес входа** введите URL-адрес имеет hello синтаксис:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="6f3c9-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="6f3c9-153">b.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-153">b.</span></span> <span data-ttu-id="6f3c9-154">В hello **URL-адрес ответа** введите URL-адрес имеет hello синтаксис:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="6f3c9-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="6f3c9-155">Hello выше значения не являются реальными.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-155">hello preceding values are not real.</span></span> <span data-ttu-id="6f3c9-156">Обновите их с URL-адрес ответа фактическое hello и hello URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="6f3c9-157">значения tooobtain hello, обратитесь в службу hello [группа поддержки клиентского программного обеспечения Cezanne HR](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="6f3c9-158">В разделе **сертификат подписи SAML**выберите **сертификата (Base64)**и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![раздел «Сертификат подписи SAML» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="6f3c9-160">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-160">Select **Save**.</span></span>

    ![кнопка «Сохранить» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6f3c9-162">В разделе **конфигурации программного обеспечения HR Cezanne**выберите **Настройка программного обеспечения Cezanne HR** tooopen hello **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="6f3c9-163">Копировать hello **идентификатор сущности SAML** и **SAML единого входа службы** URL-адрес из hello **краткий справочник** раздела.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![раздел «Конфигурации программного обеспечения Cezanne HR» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="6f3c9-165">В другом окне браузера Войдите на tooyour Cezanne HR программного обеспечения клиента с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="6f3c9-166">Выберите в левой области hello **настройки системы**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="6f3c9-167">Выберите **Security Settings** > **Single Sign-On Configuration** ("Параметры безопасности" > "Конфигурация единого входа").</span><span class="sxs-lookup"><span data-stu-id="6f3c9-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![связь «Один настройки единого входа» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="6f3c9-169">В hello **разрешить пользователям toolog hello следующие службы единого входа (SSO) с помощью** области, выберите hello **SAML 2.0** флажок и выберите hello **Расширенная настройка** параметр.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Параметры служб единого входа](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="6f3c9-171">Нажмите кнопку **Add New** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-171">Select **Add New**.</span></span>

    ![Hello кнопку «Добавить»](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="6f3c9-173">В разделе **Поставщики удостоверений SAML 2.0**, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![раздел «Поставщики удостоверений SAML 2.0» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="6f3c9-175">а.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-175">a.</span></span> <span data-ttu-id="6f3c9-176">В hello **отображаемое имя** введите название hello поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="6f3c9-177">b.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-177">b.</span></span> <span data-ttu-id="6f3c9-178">В hello **идентификатор сущности** вставьте hello **идентификатор сущности SAML** , скопированный из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="6f3c9-179">c.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-179">c.</span></span> <span data-ttu-id="6f3c9-180">В hello **привязки SAML** выберите **POST**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="6f3c9-181">d.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-181">d.</span></span> <span data-ttu-id="6f3c9-182">В hello **конечную точку службы маркеров безопасности** вставьте hello **SAML единого входа службы** URL-адрес, скопированный из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="6f3c9-183">д.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-183">e.</span></span> <span data-ttu-id="6f3c9-184">В hello **имя атрибута идентификатора пользователя** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="6f3c9-185">f.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-185">f.</span></span> <span data-ttu-id="6f3c9-186">tooupload hello загрузить сертификат из Azure AD, выберите hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="6f3c9-187">ж.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-187">g.</span></span> <span data-ttu-id="6f3c9-188">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-188">Select **OK**.</span></span> 

12. <span data-ttu-id="6f3c9-189">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-189">Select **Save**.</span></span>

    ![кнопка «Сохранить» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="6f3c9-191">При настройке приложения hello, могут читать четкими версию перед инструкции в hello hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6f3c9-192">После добавления приложение hello с hello **Active Directory** > **корпоративных приложений** раздел, выберите hello **единого входа** вкладки. Hello доступа внедряются документации из hello **конфигурации** раздела.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="6f3c9-193">toolearn Дополнительные сведения о функции hello внедренные документации, в разделе [Azure AD внедренных документации]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6f3c9-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3c9-194">Create an Azure AD test user</span></span>
<span data-ttu-id="6f3c9-195">В этом разделе создайте тестового пользователя Саймон Britta в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![Hello тестового пользователя Саймон Britta][100]

<span data-ttu-id="6f3c9-197">Здравствуйте toocreate тестового пользователя в Azure AD, следующие:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="6f3c9-198">В hello **портал Azure**в левой области hello, выберите hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![Кнопка «Azure Active Directory» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f3c9-200">список пользователей, выберите toodisplay hello **пользователей и групп** > **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Здравствуйте, «Все пользователи» ссылки](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="6f3c9-202">Hello **всех пользователей** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="6f3c9-203">tooopen hello **пользователя** выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Кнопка «Добавить» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f3c9-205">В hello **пользователя** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![диалоговое окно «User» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f3c9-207">а.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-207">a.</span></span> <span data-ttu-id="6f3c9-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f3c9-209">b.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-209">b.</span></span> <span data-ttu-id="6f3c9-210">В hello **имя пользователя** введите пользователя Britta Simon **адрес электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="6f3c9-211">c.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-211">c.</span></span> <span data-ttu-id="6f3c9-212">Выберите hello **Показать пароль** флажок, а затем значение hello примечание, созданный в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="6f3c9-213">d.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-213">d.</span></span> <span data-ttu-id="6f3c9-214">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="6f3c9-215">Создание тестового пользователя Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="6f3c9-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="6f3c9-216">Пользователи toosign tooenable Azure AD в программном обеспечении tooCezanne отдела Кадров, их необходимо подготовить в отделе Кадров Cezanne программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="6f3c9-217">В случае hello программного обеспечения Cezanne HR Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="6f3c9-218">Подготовка учетной записи пользователя, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="6f3c9-219">Войдите в tooyour Cezanne HR программного обеспечения корпоративный сайт с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="6f3c9-220">Выберите в левой области hello **установки System** > **Управление пользователями** > **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="6f3c9-221">![ссылка «Добавить пользователя» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "нового пользователя")</span><span class="sxs-lookup"><span data-stu-id="6f3c9-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="6f3c9-222">В разделе **сведения о лице**, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="6f3c9-223">![Hello раздела «Подробности лица»](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "нового пользователя")</span><span class="sxs-lookup"><span data-stu-id="6f3c9-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="6f3c9-224">а.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-224">a.</span></span> <span data-ttu-id="6f3c9-225">Установите для параметра **Internal User** (Внутренний пользователь) значение **OFF** (Выключено).</span><span class="sxs-lookup"><span data-stu-id="6f3c9-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="6f3c9-226">b.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-226">b.</span></span> <span data-ttu-id="6f3c9-227">В hello **имя** поле, тип hello имя пользователя, например, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="6f3c9-228">c.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-228">c.</span></span> <span data-ttu-id="6f3c9-229">В hello **Фамилия** поле, тип hello фамилию пользователя, например, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="6f3c9-230">d.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-230">d.</span></span> <span data-ttu-id="6f3c9-231">В hello **электронной почты** введите hello адрес электронной почты пользователя, например, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="6f3c9-232">В разделе **сведения об учетной записи**, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6f3c9-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="6f3c9-233">![раздел «Сведения об учетной записи» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "нового пользователя")</span><span class="sxs-lookup"><span data-stu-id="6f3c9-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="6f3c9-234">а.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-234">a.</span></span> <span data-ttu-id="6f3c9-235">В hello **Username** введите hello адрес электронной почты пользователя, например, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="6f3c9-236">b.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-236">b.</span></span> <span data-ttu-id="6f3c9-237">В hello **пароль** введите пароль пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="6f3c9-238">c.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-238">c.</span></span> <span data-ttu-id="6f3c9-239">В hello **роль безопасности** выберите **HR Professional**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="6f3c9-240">d.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-240">d.</span></span> <span data-ttu-id="6f3c9-241">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-241">Select **OK**.</span></span>

5. <span data-ttu-id="6f3c9-242">На hello **единого входа** hello на вкладке **идентификаторов SAML 2.0** выберите **добавить новое**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="6f3c9-243">![Hello кнопку «Добавить»](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "пользователя")</span><span class="sxs-lookup"><span data-stu-id="6f3c9-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="6f3c9-244">В hello **поставщика удостоверений** выберите поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="6f3c9-245">В hello **идентификатор пользователя** введите hello адрес электронной почты для учетной записи тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="6f3c9-246">![Здравствуйте, «Поставщик удостоверений» и «Идентификатор пользователя» поля](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "пользователя")</span><span class="sxs-lookup"><span data-stu-id="6f3c9-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="6f3c9-247">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-247">Select **Save**.</span></span>

    <span data-ttu-id="6f3c9-248">![кнопка «Сохранить» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "пользователя")</span><span class="sxs-lookup"><span data-stu-id="6f3c9-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6f3c9-249">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="6f3c9-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6f3c9-250">В этом разделе включите тестового пользователя toouse Britta Simon Azure единого входа путем предоставления программного доступа tooCezanne HR.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Проверка доступа пользователей][200] 

1. <span data-ttu-id="6f3c9-252">В hello портал Azure откройте представление приложения hello, а затем перейдите toohello представления каталога.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="6f3c9-253">Щелкните **Корпоративные приложения** > **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Здравствуйте, «Все приложения» ссылки][201] 

2. <span data-ttu-id="6f3c9-255">В списке приложений hello выберите **программного обеспечения HR Cezanne**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![список «Приложения» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="6f3c9-257">Выберите в меню hello слева hello, **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="6f3c9-259">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-259">Select **Add**.</span></span> <span data-ttu-id="6f3c9-260">Затем в hello **добавить назначение** выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][203]

5. <span data-ttu-id="6f3c9-262">В hello **пользователей и групп** диалогового окна hello **пользователей** выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="6f3c9-263">В hello **пользователей и групп** выберите **выберите**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="6f3c9-264">В hello **добавить назначение** выберите **назначить**.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="6f3c9-265">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6f3c9-265">Test SSO</span></span>

<span data-ttu-id="6f3c9-266">В этом разделе можно проверить конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="6f3c9-267">При выборе плитки программного обеспечения Cezanne HR hello в панель доступа hello входа автоматически tooyour Cezanne HR программного приложения.</span><span class="sxs-lookup"><span data-stu-id="6f3c9-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f3c9-268">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f3c9-268">Next steps</span></span>

* [<span data-ttu-id="6f3c9-269">Список учебников по toointegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f3c9-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f3c9-270">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6f3c9-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

