---
title: "Учебник. Интеграция Azure Active Directory с IBM Kenexa Survey Enterprise | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и корпоративный опроса Kenexa IBM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="d391a-103">Руководство по интеграции Azure Active Directory с IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="d391a-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="d391a-104">В этом учебнике вы узнаете, как toointegrate Enterprise опроса Kenexa IBM с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d391a-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d391a-105">Интеграция Enterprise опроса Kenexa IBM с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d391a-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d391a-106">Можно управлять в Azure AD, имеющего доступ tooIBM Kenexa опроса предприятия.</span><span class="sxs-lookup"><span data-stu-id="d391a-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="d391a-107">Tooautomatically пользователей при входе в tooIBM Kenexa опроса Enterprise можно включить с помощью единого входа (SSO) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d391a-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d391a-108">Можно управлять учетными записями в одном централизованном месте: hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d391a-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="d391a-109">Если требуется tooknow Дополнительные сведения о программное обеспечение как услуга (SaaS) интеграции приложений с Azure AD, см. раздел [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d391a-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d391a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d391a-110">Prerequisites</span></span>

<span data-ttu-id="d391a-111">tooconfigure интеграция Azure AD с IBM Kenexa опроса предприятия необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d391a-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="d391a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d391a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d391a-113">подписка на IBM Kenexa Survey Enterprise с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d391a-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d391a-114">При тестировании hello шаги в этом учебнике, рекомендуется не использовать в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="d391a-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="d391a-115">tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="d391a-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="d391a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d391a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d391a-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d391a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d391a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d391a-118">Scenario description</span></span>
<span data-ttu-id="d391a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d391a-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="d391a-120">Hello сценарии, описанные в учебнике hello состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d391a-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="d391a-121">Добавление IBM Kenexa опроса Enterprise из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="d391a-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="d391a-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d391a-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="d391a-123">Добавление IBM Kenexa опроса Enterprise из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="d391a-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="d391a-124">tooconfigure интеграции IBM Kenexa опроса Enterprise hello в Azure AD, добавить IBM Kenexa опроса Enterprise из hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d391a-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d391a-125">tooadd Enterprise опроса IBM Kenexa из галереи hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d391a-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="d391a-126">В hello [портал Azure](https://portal.azure.com)в левой области hello, щелкнув hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d391a-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="d391a-128">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d391a-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="d391a-130">tooadd приложение, нажмите кнопку hello **новое приложение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d391a-130">tooadd an application, click hello **New application** button.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="d391a-132">Введите в поле поиска hello **Enterprise опроса IBM Kenexa**.</span><span class="sxs-lookup"><span data-stu-id="d391a-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="d391a-134">В списке результатов hello выберите **Enterprise опроса IBM Kenexa**и нажмите кнопку hello **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d391a-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![IBM Kenexa опроса Enterprise в списке результатов hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d391a-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d391a-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d391a-137">В этом разделе описана настройка и проверка единого входа Azure AD в IBM Kenexa Survey Enterprise с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d391a-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d391a-138">Для toowork единого входа Azure AD должен tooidentify hello IBM Kenexa опроса Enterprise пользователя аналога в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d391a-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="d391a-139">Иными словами, в Azure AD необходимо установить связь между пользователем Azure AD и соответствующим пользователем в IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d391a-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="d391a-140">tooestablish hello связи, назначить значение hello hello **имя пользователя** IBM Kenexa опроса предприятия в качестве значения hello hello **Username** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d391a-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="d391a-141">tooconfigure и тестирования SSO Azure AD с IBM Kenexa опроса Enterprise, полный hello блоки в следующих двух разделах hello.</span><span class="sxs-lookup"><span data-stu-id="d391a-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="d391a-142">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="d391a-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="d391a-143">В этом разделе Включить единый вход Azure AD в hello портал Azure и настройки единого входа в вашем приложении Enterprise опроса Kenexa IBM, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="d391a-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="d391a-144">В hello в hello портала Azure **Enterprise опроса IBM Kenexa** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d391a-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка для настройки единого входа для IBM Kenexa Survey Enterprise][4]

2. <span data-ttu-id="d391a-146">В hello **единого входа** диалогового окна hello **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d391a-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="d391a-148">В hello **URL-адреса и домена предприятия опроса Kenexa IBM** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d391a-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="d391a-150">а.</span><span class="sxs-lookup"><span data-stu-id="d391a-150">a.</span></span> <span data-ttu-id="d391a-151">В hello **идентификатор** введите URL-адрес с hello следующий шаблон:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="d391a-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="d391a-152">b.</span><span class="sxs-lookup"><span data-stu-id="d391a-152">b.</span></span> <span data-ttu-id="d391a-153">В hello **URL-адрес ответа** введите URL-адрес с hello следующий шаблон:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="d391a-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d391a-154">Hello выше значения не являются реальными.</span><span class="sxs-lookup"><span data-stu-id="d391a-154">hello preceding values are not real.</span></span> <span data-ttu-id="d391a-155">Дополнить фактический идентификатор hello и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="d391a-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="d391a-156">фактические значения, обратитесь в службу hello hello tooobtain [группа поддержки Enterprise опроса IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="d391a-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="d391a-157">В разделе **сертификат подписи SAML**, нажмите кнопку **сертификата (Base64)**и сохраните файл tooyour hello сертификат компьютера.</span><span class="sxs-lookup"><span data-stu-id="d391a-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![ссылку для скачивания сертификата (Base64) Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="d391a-159">Hello IBM Kenexa опроса корпоративное приложение ожидает утверждения безопасности утверждения Markup Language (SAML) tooreceive hello в определенном формате, поэтому требуется вы tooadd настраиваемого атрибута сопоставления toohello Настройка атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="d391a-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="d391a-160">Hello значение утверждения идентификатора пользователя hello в ответ hello должно соответствовать hello идентификатор единого входа, настроенную в системе Kenexa hello.</span><span class="sxs-lookup"><span data-stu-id="d391a-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="d391a-161">toomap hello идентификатор соответствующего пользователя в вашей организации, как протокол датаграмм SSO Интернета (IDP), работа с hello [группа поддержки Enterprise опроса IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="d391a-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="d391a-162">По умолчанию Azure AD задает идентификатор пользователя hello как значение имени участника (UPN) пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="d391a-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="d391a-163">Можно изменить это значение на hello **атрибута** вкладки, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="d391a-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="d391a-164">Интеграция Hello работает только после завершения сопоставления правильно hello.</span><span class="sxs-lookup"><span data-stu-id="d391a-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![Атрибуты пользователя Hello-диалоговое окно](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="d391a-166">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d391a-166">Click **Save**.</span></span>

    ![Настройка Hello единым входом кнопку Сохранить](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d391a-168">tooopen hello **Настройка входа** окна в разделе **конфигурация предприятия опроса IBM Kenexa**, нажмите кнопку **настроить корпоративный опроса IBM Kenexa**.</span><span class="sxs-lookup"><span data-stu-id="d391a-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![Настройка корпоративного опроса IBM Kenexa ссылку Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="d391a-170">Копировать hello **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** значения из hello **краткий справочник** раздела.</span><span class="sxs-lookup"><span data-stu-id="d391a-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="d391a-171">В hello **Настройка входа** окна в разделе **краткий справочник**, hello копирования **URL-адрес выхода**, **идентификатор сущности SAML**, и  **SAML единого входа URL-адрес службы** значения.</span><span class="sxs-lookup"><span data-stu-id="d391a-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="d391a-172">tooconfigure единого входа на hello **Enterprise опроса IBM Kenexa** стороны, отправьте загружаются hello **сертификата (Base64)**, **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** значения toohello [группа поддержки Enterprise опроса IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="d391a-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="d391a-173">Можно ссылаться tooa четкими версии этими инструкциями в hello [портал Azure](https://portal.azure.com) при настройке приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d391a-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="d391a-174">После добавления приложение hello с hello **Active Directory** > **корпоративных приложений** просто щелкните hello **единого входа** вкладку, а затем получить доступ к Hello внедренных документации с помощью hello **конфигурации** раздел в конце hello.</span><span class="sxs-lookup"><span data-stu-id="d391a-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="d391a-175">toolearn Дополнительные сведения о функции hello внедренные документации, в разделе [Azure AD внедренных документации](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d391a-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d391a-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d391a-176">Create an Azure AD test user</span></span>
<span data-ttu-id="d391a-177">В этом разделе создайте тестового пользователя Саймон Britta в hello портал Azure, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="d391a-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Создание тестового пользователя Azure AD][100]

1. <span data-ttu-id="d391a-179">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d391a-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d391a-181">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d391a-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d391a-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d391a-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d391a-185">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d391a-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d391a-187">а.</span><span class="sxs-lookup"><span data-stu-id="d391a-187">a.</span></span> <span data-ttu-id="d391a-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d391a-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d391a-189">b.</span><span class="sxs-lookup"><span data-stu-id="d391a-189">b.</span></span> <span data-ttu-id="d391a-190">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d391a-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d391a-191">c.</span><span class="sxs-lookup"><span data-stu-id="d391a-191">c.</span></span> <span data-ttu-id="d391a-192">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="d391a-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d391a-193">d.</span><span class="sxs-lookup"><span data-stu-id="d391a-193">d.</span></span> <span data-ttu-id="d391a-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d391a-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="d391a-195">Создание тестового пользователя IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="d391a-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="d391a-196">В этом разделе описано, как создать пользователя Britta Simon в приложении IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d391a-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="d391a-197">toocreate пользователей в hello IBM Kenexa опроса корпоративной системы и карты hello идентификатор единого входа для них, можно работать с hello [группа поддержки Enterprise опроса IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="d391a-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="d391a-198">Это значение идентификатора единого входа также должен быть сопоставлен toohello значение идентификатора пользователя из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d391a-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="d391a-199">Можно изменить этот параметр по умолчанию на hello **атрибута** вкладки.</span><span class="sxs-lookup"><span data-stu-id="d391a-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d391a-200">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d391a-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d391a-201">В этом разделе включите пользователя toouse Britta Simon единого входа Azure путем предоставления доступа tooIBM Kenexa опроса Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d391a-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="d391a-203">пользователь tooassign Britta Simon tooIBM Kenexa опроса Enterprise, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d391a-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="d391a-204">В hello портал Azure, откройте hello **приложений** просмотреть, перейдите toohello **каталога** представление, выберите **корпоративных приложений**и нажмите кнопку **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d391a-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Здравствуйте, «Корпоративных приложений» и «Всех приложений» ссылки][201] 

2. <span data-ttu-id="d391a-206">В hello **приложений** выберите **Enterprise опроса IBM Kenexa**.</span><span class="sxs-lookup"><span data-stu-id="d391a-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![ссылка на корпоративный опроса Kenexa IBM Hello в списке приложений hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="d391a-208">Hello левой панели щелкните **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d391a-208">In hello left pane, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="d391a-210">Нажмите кнопку hello **добавить** кнопки и затем в hello **добавить назначение** выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d391a-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="d391a-212">В hello **пользователей и групп** диалогового окна hello **пользователей** выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d391a-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="d391a-213">В hello **пользователей и групп** диалоговое окно, нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d391a-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="d391a-214">В hello **добавить назначение** диалоговое окно, нажмите кнопку hello **назначить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d391a-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d391a-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d391a-215">Test single sign-on</span></span>

<span data-ttu-id="d391a-216">В этом разделе можно проверить конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="d391a-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="d391a-217">При нажатии кнопки hello **Enterprise опроса Kenexa IBM** плитки в Здравствуйте панели доступа, вы должны автоматически входить в tooyour IBM Kenexa опроса корпоративного приложения.</span><span class="sxs-lookup"><span data-stu-id="d391a-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d391a-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d391a-218">Additional resources</span></span>

* [<span data-ttu-id="d391a-219">Список учебников по toointegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d391a-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d391a-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d391a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
