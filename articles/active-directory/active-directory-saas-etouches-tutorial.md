---
title: "Руководство по интеграции Azure Active Directory с etouches | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="84365-103">Руководство. Интеграция Azure Active Directory с etouches</span><span class="sxs-lookup"><span data-stu-id="84365-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="84365-104">В этом учебнике вы узнаете, как etouches toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84365-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84365-105">Интеграция с Azure AD etouches предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="84365-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="84365-106">Можно управлять в Azure AD, имеющего доступ tooetouches</span><span class="sxs-lookup"><span data-stu-id="84365-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="84365-107">Можно включить на пользователей tooautomatically get вошедшего tooetouches (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="84365-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84365-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="84365-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="84365-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84365-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84365-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84365-110">Prerequisites</span></span>

<span data-ttu-id="84365-111">tooconfigure интеграция Azure AD с etouches требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="84365-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="84365-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="84365-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84365-113">подписка etouches с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="84365-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84365-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="84365-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84365-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="84365-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84365-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="84365-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84365-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84365-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84365-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="84365-118">Scenario description</span></span>
<span data-ttu-id="84365-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="84365-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84365-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="84365-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84365-121">Добавление etouches из галереи hello</span><span class="sxs-lookup"><span data-stu-id="84365-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="84365-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="84365-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="84365-123">Добавление etouches из галереи hello</span><span class="sxs-lookup"><span data-stu-id="84365-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="84365-124">tooconfigure hello интеграции etouches в Azure AD, вы должны etouches tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="84365-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84365-125">**etouches tooadd из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84365-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84365-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="84365-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="84365-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="84365-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="84365-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="84365-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="84365-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="84365-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="84365-133">Введите в поле поиска hello **etouches**выберите **etouches** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="84365-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![etouches в списке результатов hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="84365-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="84365-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="84365-136">В этом разделе описана настройка и проверка единого входа Azure AD в etouches с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84365-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84365-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в etouches является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84365-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="84365-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в etouches должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="84365-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="84365-139">В etouches, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="84365-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="84365-140">tooconfigure и теста Azure AD единого входа с etouches, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="84365-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84365-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="84365-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84365-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="84365-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84365-143">**[Создание тестового пользователя, прошедшего etouches](#create-an-etouches-test-user)**  -toohave аналог Саймон Britta в etouches, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="84365-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="84365-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="84365-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84365-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="84365-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="84365-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="84365-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="84365-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении etouches.</span><span class="sxs-lookup"><span data-stu-id="84365-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="84365-148">**tooconfigure Azure AD единого входа с etouches, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84365-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="84365-149">В hello в hello портала Azure **etouches** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="84365-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="84365-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="84365-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="84365-153">На hello **etouches URL-адреса и домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84365-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="84365-155">а.</span><span class="sxs-lookup"><span data-stu-id="84365-155">a.</span></span> <span data-ttu-id="84365-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="84365-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="84365-157">b.</span><span class="sxs-lookup"><span data-stu-id="84365-157">b.</span></span> <span data-ttu-id="84365-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="84365-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84365-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="84365-159">These values are not real.</span></span> <span data-ttu-id="84365-160">Обновить значение hello hello фактическое вход URL-адрес и идентификатор, который описан далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="84365-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="84365-161">etouches приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="84365-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="84365-162">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="84365-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="84365-163">Вы можете управлять hello значения этих атрибутов из hello **атрибут пользователя** приложения hello.</span><span class="sxs-lookup"><span data-stu-id="84365-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="84365-164">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="84365-164">hello following screenshot shows an example for this.</span></span> 

    ![Атрибут пользователя](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="84365-166">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84365-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="84365-167">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="84365-167">Attribute Name</span></span> | <span data-ttu-id="84365-168">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="84365-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="84365-169">Email</span><span class="sxs-lookup"><span data-stu-id="84365-169">Email</span></span> | <span data-ttu-id="84365-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="84365-170">user.mail</span></span> |    
    
    <span data-ttu-id="84365-171">а.</span><span class="sxs-lookup"><span data-stu-id="84365-171">a.</span></span> <span data-ttu-id="84365-172">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="84365-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Добавление атрибута](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Диалоговое окно добавления атрибута](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="84365-175">b.</span><span class="sxs-lookup"><span data-stu-id="84365-175">b.</span></span> <span data-ttu-id="84365-176">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="84365-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="84365-177">c.</span><span class="sxs-lookup"><span data-stu-id="84365-177">c.</span></span> <span data-ttu-id="84365-178">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="84365-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="84365-179">d.</span><span class="sxs-lookup"><span data-stu-id="84365-179">d.</span></span> <span data-ttu-id="84365-180">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="84365-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="84365-181">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="84365-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="84365-183">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="84365-183">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="84365-185">tooget единого входа, настроенному для вашего приложения, выполните следующие шаги в приложении etouches hello hello.</span><span class="sxs-lookup"><span data-stu-id="84365-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![Настройка etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="84365-187">а.</span><span class="sxs-lookup"><span data-stu-id="84365-187">a.</span></span> <span data-ttu-id="84365-188">Имя входа слишком**etouches** приложения с помощью hello права администратора.</span><span class="sxs-lookup"><span data-stu-id="84365-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="84365-189">b.</span><span class="sxs-lookup"><span data-stu-id="84365-189">b.</span></span> <span data-ttu-id="84365-190">Go toohello **SAML** конфигурации.</span><span class="sxs-lookup"><span data-stu-id="84365-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="84365-191">c.</span><span class="sxs-lookup"><span data-stu-id="84365-191">c.</span></span> <span data-ttu-id="84365-192">В hello **Общие параметры** статьи, откройте загруженный сертификат из портала Azure в блокноте, hello копирования содержимого и вставьте его в текстовое поле метаданных hello поставщика Удостоверений.</span><span class="sxs-lookup"><span data-stu-id="84365-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="84365-193">d.</span><span class="sxs-lookup"><span data-stu-id="84365-193">d.</span></span> <span data-ttu-id="84365-194">Щелкните hello **сохранить & остаться** кнопки.</span><span class="sxs-lookup"><span data-stu-id="84365-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="84365-195">д.</span><span class="sxs-lookup"><span data-stu-id="84365-195">e.</span></span> <span data-ttu-id="84365-196">Щелкните hello **обновление метаданных** кнопку в hello раздел метаданных SAML.</span><span class="sxs-lookup"><span data-stu-id="84365-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="84365-197">f.</span><span class="sxs-lookup"><span data-stu-id="84365-197">f.</span></span> <span data-ttu-id="84365-198">Это приведет к открытию страницы hello и выполнить единый вход.</span><span class="sxs-lookup"><span data-stu-id="84365-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="84365-199">Один раз hello единого входа работает, а затем можно настроить имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="84365-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="84365-200">ж.</span><span class="sxs-lookup"><span data-stu-id="84365-200">g.</span></span> <span data-ttu-id="84365-201">В поле имя пользователя hello выбрать hello **emailaddress** как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="84365-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="84365-202">h.</span><span class="sxs-lookup"><span data-stu-id="84365-202">h.</span></span> <span data-ttu-id="84365-203">Копировать hello **идентификатор сущности SP** значение и вставьте его в hello **идентификатор** текстовое поле находится в **etouches URL-адреса и домена** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="84365-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="84365-204">i.</span><span class="sxs-lookup"><span data-stu-id="84365-204">i.</span></span> <span data-ttu-id="84365-205">Копировать hello **URL-адрес единого входа и ACS** значение и вставьте его в hello **URL-адрес входа** текстовое поле находится в **etouches URL-адреса и домена** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="84365-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="84365-206">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="84365-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="84365-207">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="84365-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="84365-208">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84365-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="84365-209">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="84365-209">Create an Azure AD test user</span></span>
<span data-ttu-id="84365-210">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="84365-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="84365-212">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84365-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84365-213">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="84365-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84365-215">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="84365-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84365-217">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="84365-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84365-219">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84365-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84365-221">а.</span><span class="sxs-lookup"><span data-stu-id="84365-221">a.</span></span> <span data-ttu-id="84365-222">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84365-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84365-223">b.</span><span class="sxs-lookup"><span data-stu-id="84365-223">b.</span></span> <span data-ttu-id="84365-224">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="84365-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84365-225">c.</span><span class="sxs-lookup"><span data-stu-id="84365-225">c.</span></span> <span data-ttu-id="84365-226">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="84365-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="84365-227">d.</span><span class="sxs-lookup"><span data-stu-id="84365-227">d.</span></span> <span data-ttu-id="84365-228">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="84365-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="84365-229">Создание тестового пользователя etouches</span><span class="sxs-lookup"><span data-stu-id="84365-229">Create an etouches test user</span></span>

<span data-ttu-id="84365-230">В этом разделе описано, как создать пользователя Britta Simon в приложении etouches.</span><span class="sxs-lookup"><span data-stu-id="84365-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="84365-231">Работать с [etouches клиента поддержки](https://www.etouches.com/event-software/support/customer-support/) tooadd hello пользователей на платформе etouches hello.</span><span class="sxs-lookup"><span data-stu-id="84365-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="84365-232">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="84365-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="84365-233">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooetouches доступа.</span><span class="sxs-lookup"><span data-stu-id="84365-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="84365-235">**tooassign tooetouches Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84365-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="84365-236">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="84365-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="84365-238">В списке приложений hello выберите **etouches**.</span><span class="sxs-lookup"><span data-stu-id="84365-238">In hello applications list, select **etouches**.</span></span>

    ![ссылка etouches Hello в списке приложений hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="84365-240">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="84365-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="84365-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="84365-242">Click **Add** button.</span></span> <span data-ttu-id="84365-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="84365-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="84365-245">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="84365-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="84365-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="84365-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84365-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="84365-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="84365-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="84365-248">Test single sign-on</span></span>


<span data-ttu-id="84365-249">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="84365-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="84365-250">При нажатии кнопки etouches плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour etouches приложения.</span><span class="sxs-lookup"><span data-stu-id="84365-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84365-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="84365-251">Additional resources</span></span>

* [<span data-ttu-id="84365-252">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84365-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84365-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="84365-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

