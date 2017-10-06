---
title: "Учебник. Интеграция Azure Active Directory с CloudPassage | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="ac82e-103">Учебник. Интеграция Azure Active Directory с CloudPassage</span><span class="sxs-lookup"><span data-stu-id="ac82e-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="ac82e-104">В этом учебнике вы узнаете, как toointegrate CloudPassage с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ac82e-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac82e-105">Интеграция с Azure AD CloudPassage предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ac82e-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ac82e-106">Можно управлять в Azure AD, имеющего доступ tooCloudPassage</span><span class="sxs-lookup"><span data-stu-id="ac82e-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="ac82e-107">Можно включить на пользователей tooautomatically get вошедшего tooCloudPassage (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac82e-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ac82e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ac82e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ac82e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac82e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac82e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ac82e-110">Prerequisites</span></span>

<span data-ttu-id="ac82e-111">tooconfigure интеграция Azure AD с CloudPassage требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ac82e-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="ac82e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ac82e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac82e-113">подписка CloudPassage с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ac82e-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac82e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ac82e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac82e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ac82e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac82e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ac82e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac82e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac82e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac82e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ac82e-118">Scenario description</span></span>
<span data-ttu-id="ac82e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ac82e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac82e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ac82e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac82e-121">Добавление CloudPassage из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ac82e-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="ac82e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac82e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="ac82e-123">Добавление CloudPassage из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ac82e-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="ac82e-124">tooconfigure hello интеграции CloudPassage в Azure AD, вы должны tooadd CloudPassage из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ac82e-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ac82e-125">**tooadd CloudPassage из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac82e-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac82e-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ac82e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ac82e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ac82e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ac82e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ac82e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ac82e-133">Введите в поле поиска hello **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-133">In hello search box, type **CloudPassage**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="ac82e-135">В панели результатов hello выберите **CloudPassage**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ac82e-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ac82e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac82e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ac82e-138">В этом разделе описана настройка и проверка единого входа Azure AD в CloudPassage с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac82e-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ac82e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в CloudPassage является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac82e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="ac82e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в CloudPassage должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ac82e-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="ac82e-141">В CloudPassage, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ac82e-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ac82e-142">tooconfigure и теста Azure AD единого входа с CloudPassage, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ac82e-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ac82e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ac82e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ac82e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ac82e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac82e-145">**[Создание тестового пользователя CloudPassage](#creating-a-cloudpassage-test-user) ** -toohave аналог Саймон Britta в CloudPassage, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ac82e-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac82e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ac82e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac82e-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ac82e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ac82e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac82e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ac82e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="ac82e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="ac82e-150">**tooconfigure Azure AD единого входа с CloudPassage, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac82e-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac82e-151">В hello в hello портала Azure **CloudPassage** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ac82e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ac82e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="ac82e-155">На hello **URL-адреса и домена CloudPassage** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ac82e-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="ac82e-157">а.</span><span class="sxs-lookup"><span data-stu-id="ac82e-157">a.</span></span> <span data-ttu-id="ac82e-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="ac82e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="ac82e-159">b.</span><span class="sxs-lookup"><span data-stu-id="ac82e-159">b.</span></span> <span data-ttu-id="ac82e-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="ac82e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="ac82e-161">Значение для этого атрибута можно получить, щелкнув **документации по программе установки единого входа** в hello **параметры единого входа** раздел CloudPassage портала.</span><span class="sxs-lookup"><span data-stu-id="ac82e-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="ac82e-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ac82e-163">These values are not real.</span></span> <span data-ttu-id="ac82e-164">Обновите эти значения с hello фактический URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="ac82e-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ac82e-165">Обратитесь к [группа поддержки клиента CloudPassage](https://www.cloudpassage.com/company/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ac82e-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="ac82e-166">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ac82e-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="ac82e-168">Приложение CloudPassage ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="ac82e-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="ac82e-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="ac82e-169">hello following screenshot shows an example for this.</span></span>
   
   ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="ac82e-171">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ac82e-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="ac82e-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="ac82e-172">Attribute Name</span></span> | <span data-ttu-id="ac82e-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="ac82e-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="ac82e-174">firstname</span><span class="sxs-lookup"><span data-stu-id="ac82e-174">firstname</span></span> |<span data-ttu-id="ac82e-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ac82e-175">user.givenname</span></span> |
    | <span data-ttu-id="ac82e-176">lastname</span><span class="sxs-lookup"><span data-stu-id="ac82e-176">lastname</span></span> |<span data-ttu-id="ac82e-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="ac82e-177">user.surname</span></span> |
    | <span data-ttu-id="ac82e-178">email</span><span class="sxs-lookup"><span data-stu-id="ac82e-178">email</span></span> |<span data-ttu-id="ac82e-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="ac82e-179">user.mail</span></span> |
    
    <span data-ttu-id="ac82e-180">а.</span><span class="sxs-lookup"><span data-stu-id="ac82e-180">a.</span></span> <span data-ttu-id="ac82e-181">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ac82e-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ac82e-184">b.</span><span class="sxs-lookup"><span data-stu-id="ac82e-184">b.</span></span> <span data-ttu-id="ac82e-185">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ac82e-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="ac82e-186">c.</span><span class="sxs-lookup"><span data-stu-id="ac82e-186">c.</span></span> <span data-ttu-id="ac82e-187">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ac82e-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ac82e-188">d.</span><span class="sxs-lookup"><span data-stu-id="ac82e-188">d.</span></span> <span data-ttu-id="ac82e-189">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-189">Click **Ok**.</span></span>

7. <span data-ttu-id="ac82e-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ac82e-190">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="ac82e-192">На hello **конфигурации CloudPassage** щелкните **Настройка CloudPassage** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ac82e-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ac82e-193">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ac82e-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="ac82e-195">В другом окне браузера, сайт компании CloudPassage tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="ac82e-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="ac82e-196">В меню в верхней части hello hello выберите **параметры**и нажмите кнопку **Администрирование сайта**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Настройка единого входа][12]

11. <span data-ttu-id="ac82e-198">Нажмите кнопку hello **параметры проверки подлинности** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ac82e-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![Настройка единого входа][13]

12. <span data-ttu-id="ac82e-200">В hello **параметры единого входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ac82e-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![Настройка единого входа][14]

    <span data-ttu-id="ac82e-202">а.</span><span class="sxs-lookup"><span data-stu-id="ac82e-202">a.</span></span> <span data-ttu-id="ac82e-203">Установите флажок **Enable Single sign-on(SSO)(SSO Setup Documentation)** (Включить единый вход (SSO) (Документация по настройке единого входа)).</span><span class="sxs-lookup"><span data-stu-id="ac82e-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="ac82e-204">b.</span><span class="sxs-lookup"><span data-stu-id="ac82e-204">b.</span></span> <span data-ttu-id="ac82e-205">Вставить **идентификатор сущности SAML** в hello **URL-адрес издателя SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ac82e-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="ac82e-206">c.</span><span class="sxs-lookup"><span data-stu-id="ac82e-206">c.</span></span> <span data-ttu-id="ac82e-207">Вставить **SAML единого входа URL-адрес службы** в hello **URL-адрес конечной точки SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ac82e-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="ac82e-208">d.</span><span class="sxs-lookup"><span data-stu-id="ac82e-208">d.</span></span> <span data-ttu-id="ac82e-209">Вставить **URL-адрес выхода** в hello **выхода целевая страница** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ac82e-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="ac82e-210">д.</span><span class="sxs-lookup"><span data-stu-id="ac82e-210">e.</span></span> <span data-ttu-id="ac82e-211">Откройте загруженный сертификат в блокноте, hello копирования содержимого загруженного сертификата в буфер обмена, а затем вставьте его в hello **сертификата x 509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ac82e-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="ac82e-212">f.</span><span class="sxs-lookup"><span data-stu-id="ac82e-212">f.</span></span> <span data-ttu-id="ac82e-213">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ac82e-214">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ac82e-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ac82e-215">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ac82e-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ac82e-216">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac82e-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ac82e-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac82e-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="ac82e-218">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ac82e-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ac82e-220">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac82e-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac82e-221">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ac82e-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ac82e-223">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ac82e-225">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ac82e-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ac82e-227">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ac82e-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ac82e-229">а.</span><span class="sxs-lookup"><span data-stu-id="ac82e-229">a.</span></span> <span data-ttu-id="ac82e-230">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac82e-231">b.</span><span class="sxs-lookup"><span data-stu-id="ac82e-231">b.</span></span> <span data-ttu-id="ac82e-232">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ac82e-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ac82e-233">c.</span><span class="sxs-lookup"><span data-stu-id="ac82e-233">c.</span></span> <span data-ttu-id="ac82e-234">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ac82e-235">d.</span><span class="sxs-lookup"><span data-stu-id="ac82e-235">d.</span></span> <span data-ttu-id="ac82e-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="ac82e-237">Создание тестового пользователя CloudPassage</span><span class="sxs-lookup"><span data-stu-id="ac82e-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="ac82e-238">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="ac82e-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="ac82e-239">**toocreate пользователя с именем Саймон Britta в CloudPassage, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac82e-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac82e-240">Tooyour входа **CloudPassage** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="ac82e-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="ac82e-241">Щелкните hello панели инструментов в верхней части hello **параметры**, а затем нажмите кнопку **Администрирование веб-сайтов**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Создание тестового пользователя CloudPassage][22] 

3. <span data-ttu-id="ac82e-243">Нажмите кнопку hello **пользователей** , а затем щелкните **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Создание тестового пользователя CloudPassage][23]

4. <span data-ttu-id="ac82e-245">В hello **добавить пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ac82e-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![Создание тестового пользователя CloudPassage][24]
    
    <span data-ttu-id="ac82e-247">а.</span><span class="sxs-lookup"><span data-stu-id="ac82e-247">a.</span></span> <span data-ttu-id="ac82e-248">В hello **имя** текстовом поле введите Britta.</span><span class="sxs-lookup"><span data-stu-id="ac82e-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="ac82e-249">b.</span><span class="sxs-lookup"><span data-stu-id="ac82e-249">b.</span></span> <span data-ttu-id="ac82e-250">В hello **Фамилия** текстовом поле введите Simon.</span><span class="sxs-lookup"><span data-stu-id="ac82e-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="ac82e-251">c.</span><span class="sxs-lookup"><span data-stu-id="ac82e-251">c.</span></span> <span data-ttu-id="ac82e-252">В hello **имя пользователя** текстовом hello **электронной почты** текстового поля и hello **электронной почты, повторите ввод** текстовое поле, введите имя пользователя Britta в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac82e-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="ac82e-253">d.</span><span class="sxs-lookup"><span data-stu-id="ac82e-253">d.</span></span> <span data-ttu-id="ac82e-254">Для параметра **Access Type** (Тип доступа) выберите **Enable Halo Portal Access** (Включить доступ к порталу Halo).</span><span class="sxs-lookup"><span data-stu-id="ac82e-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="ac82e-255">д.</span><span class="sxs-lookup"><span data-stu-id="ac82e-255">e.</span></span> <span data-ttu-id="ac82e-256">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ac82e-257">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ac82e-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ac82e-258">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooCloudPassage доступа.</span><span class="sxs-lookup"><span data-stu-id="ac82e-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ac82e-260">**tooassign tooCloudPassage Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac82e-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac82e-261">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ac82e-263">В списке приложений hello выберите **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-263">In hello applications list, select **CloudPassage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="ac82e-265">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ac82e-267">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-267">Click **Add** button.</span></span> <span data-ttu-id="ac82e-268">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ac82e-270">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ac82e-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ac82e-271">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac82e-272">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ac82e-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ac82e-273">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ac82e-273">Testing single sign-on</span></span>

<span data-ttu-id="ac82e-274">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="ac82e-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ac82e-275">При нажатии кнопки hello CloudPassage плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour CloudPassage приложения.</span><span class="sxs-lookup"><span data-stu-id="ac82e-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac82e-276">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ac82e-276">Additional resources</span></span>

* [<span data-ttu-id="ac82e-277">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac82e-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac82e-278">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac82e-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

