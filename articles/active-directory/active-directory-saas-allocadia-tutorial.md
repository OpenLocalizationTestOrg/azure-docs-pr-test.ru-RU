---
title: "Руководство. Интеграция Azure Active Directory с Allocadia | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a01c232f9dc50e690dd348430899db9c13f1564
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="586fd-103">Учебник. Интеграция Azure Active Directory с Allocadia</span><span class="sxs-lookup"><span data-stu-id="586fd-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="586fd-104">В этом учебнике вы узнаете, как toointegrate Allocadia с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="586fd-104">In this tutorial, you learn how toointegrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="586fd-105">Интеграция с Azure AD Allocadia предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="586fd-105">Integrating Allocadia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="586fd-106">Можно управлять в Azure AD, имеющего доступ tooAllocadia</span><span class="sxs-lookup"><span data-stu-id="586fd-106">You can control in Azure AD who has access tooAllocadia</span></span>
- <span data-ttu-id="586fd-107">Можно включить на пользователей tooautomatically get вошедшего tooAllocadia (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="586fd-107">You can enable your users tooautomatically get signed-on tooAllocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="586fd-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="586fd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="586fd-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="586fd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="586fd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="586fd-110">Prerequisites</span></span>

<span data-ttu-id="586fd-111">tooconfigure интеграция Azure AD с Allocadia требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="586fd-111">tooconfigure Azure AD integration with Allocadia, you need hello following items:</span></span>

- <span data-ttu-id="586fd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="586fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="586fd-113">подписка Allocadia с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="586fd-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="586fd-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="586fd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="586fd-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="586fd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="586fd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="586fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="586fd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="586fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="586fd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="586fd-118">Scenario description</span></span>
<span data-ttu-id="586fd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="586fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="586fd-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="586fd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="586fd-121">Добавление Allocadia из галереи hello</span><span class="sxs-lookup"><span data-stu-id="586fd-121">Adding Allocadia from hello gallery</span></span>
2. <span data-ttu-id="586fd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="586fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-hello-gallery"></a><span data-ttu-id="586fd-123">Добавление Allocadia из галереи hello</span><span class="sxs-lookup"><span data-stu-id="586fd-123">Adding Allocadia from hello gallery</span></span>
<span data-ttu-id="586fd-124">tooconfigure hello интеграции Allocadia в Azure AD, вы должны tooadd Allocadia из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="586fd-124">tooconfigure hello integration of Allocadia into Azure AD, you need tooadd Allocadia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="586fd-125">**tooadd Allocadia из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="586fd-125">**tooadd Allocadia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="586fd-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="586fd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="586fd-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="586fd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="586fd-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="586fd-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="586fd-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="586fd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="586fd-133">Введите в поле поиска hello **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="586fd-133">In hello search box, type **Allocadia**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="586fd-135">В панели результатов hello выберите **Allocadia**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="586fd-135">In hello results panel, select **Allocadia**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="586fd-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="586fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="586fd-138">В этом разделе описана настройка и проверка единого входа Azure AD в Allocadia с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="586fd-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="586fd-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Allocadia является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="586fd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Allocadia is tooa user in Azure AD.</span></span> <span data-ttu-id="586fd-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Allocadia должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="586fd-140">In other words, a link relationship between an Azure AD user and hello related user in Allocadia needs toobe established.</span></span>

<span data-ttu-id="586fd-141">В Allocadia, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="586fd-141">In Allocadia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="586fd-142">tooconfigure и теста Azure AD единого входа с Allocadia, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="586fd-142">tooconfigure and test Azure AD single sign-on with Allocadia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="586fd-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="586fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="586fd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="586fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="586fd-145">**[Создание тестового пользователя, прошедшего Allocadia](#creating-an-allocadia-test-user) ** -toohave аналог Саймон Britta в Allocadia, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="586fd-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - toohave a counterpart of Britta Simon in Allocadia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="586fd-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="586fd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="586fd-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="586fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="586fd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="586fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="586fd-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Allocadia.</span><span class="sxs-lookup"><span data-stu-id="586fd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="586fd-150">**tooconfigure Azure AD единого входа с Allocadia, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="586fd-150">**tooconfigure Azure AD single sign-on with Allocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="586fd-151">В hello в hello портала Azure **Allocadia** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="586fd-151">In hello Azure portal, on hello **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="586fd-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="586fd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="586fd-155">На hello **URL-адреса и домена Allocadia** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="586fd-155">On hello **Allocadia Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="586fd-157">а.</span><span class="sxs-lookup"><span data-stu-id="586fd-157">a.</span></span> <span data-ttu-id="586fd-158">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="586fd-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
       
     <span data-ttu-id="586fd-159">для тестовой среды: `https://na2standby.allocadia.com`;</span><span class="sxs-lookup"><span data-stu-id="586fd-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="586fd-160">для рабочей среды: `https://na2.allocadia.com`.</span><span class="sxs-lookup"><span data-stu-id="586fd-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="586fd-161">b.</span><span class="sxs-lookup"><span data-stu-id="586fd-161">b.</span></span> <span data-ttu-id="586fd-162">В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="586fd-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
     <span data-ttu-id="586fd-163">для тестовой среды: `https://na2standby.allocadia.com/allocadia/saml/SSO`;</span><span class="sxs-lookup"><span data-stu-id="586fd-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="586fd-164">для рабочей среды: `https://na2.allocadia.com/allocadia/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="586fd-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="586fd-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="586fd-165">These values are not real.</span></span> <span data-ttu-id="586fd-166">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="586fd-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="586fd-167">Обратитесь к [Allocadia поддержки](mailTo:support@allocadia.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="586fd-167">Contact [Allocadia support team](mailTo:support@allocadia.com) tooget these values.</span></span>

4. <span data-ttu-id="586fd-168">Allocadia приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="586fd-168">Allocadia application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="586fd-169">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="586fd-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="586fd-170">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="586fd-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="586fd-171">Следующий снимок экрана приветствия показан пример для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="586fd-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="586fd-173">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="586fd-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="586fd-174">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="586fd-174">Attribute Name</span></span> | <span data-ttu-id="586fd-175">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="586fd-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="586fd-176">firstname</span><span class="sxs-lookup"><span data-stu-id="586fd-176">firstname</span></span> | <span data-ttu-id="586fd-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="586fd-177">user.givenname</span></span> |
    | <span data-ttu-id="586fd-178">lastname</span><span class="sxs-lookup"><span data-stu-id="586fd-178">lastname</span></span> | <span data-ttu-id="586fd-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="586fd-179">user.surname</span></span> |
    | <span data-ttu-id="586fd-180">email</span><span class="sxs-lookup"><span data-stu-id="586fd-180">email</span></span> | <span data-ttu-id="586fd-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="586fd-181">user.mail</span></span> |
    
    <span data-ttu-id="586fd-182">а.</span><span class="sxs-lookup"><span data-stu-id="586fd-182">a.</span></span> <span data-ttu-id="586fd-183">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="586fd-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="586fd-185">b.</span><span class="sxs-lookup"><span data-stu-id="586fd-185">b.</span></span> <span data-ttu-id="586fd-186">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="586fd-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="586fd-188">c.</span><span class="sxs-lookup"><span data-stu-id="586fd-188">c.</span></span> <span data-ttu-id="586fd-189">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="586fd-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
 
    <span data-ttu-id="586fd-190">d.</span><span class="sxs-lookup"><span data-stu-id="586fd-190">d.</span></span> <span data-ttu-id="586fd-191">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="586fd-191">Click **Ok**.</span></span>



6. <span data-ttu-id="586fd-192">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="586fd-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="586fd-194">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="586fd-194">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="586fd-196">tooconfigure единого входа на **Allocadia** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Allocadia поддержки](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="586fd-196">tooconfigure single sign-on on **Allocadia** side, you need toosend hello downloaded **Metadata XML** too[Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="586fd-197">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="586fd-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="586fd-198">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="586fd-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="586fd-199">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="586fd-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="586fd-200">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="586fd-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="586fd-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="586fd-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="586fd-202">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="586fd-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="586fd-204">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="586fd-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="586fd-205">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="586fd-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="586fd-207">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="586fd-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="586fd-209">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="586fd-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="586fd-211">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="586fd-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="586fd-213">а.</span><span class="sxs-lookup"><span data-stu-id="586fd-213">a.</span></span> <span data-ttu-id="586fd-214">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="586fd-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="586fd-215">b.</span><span class="sxs-lookup"><span data-stu-id="586fd-215">b.</span></span> <span data-ttu-id="586fd-216">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="586fd-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="586fd-217">c.</span><span class="sxs-lookup"><span data-stu-id="586fd-217">c.</span></span> <span data-ttu-id="586fd-218">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="586fd-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="586fd-219">d.</span><span class="sxs-lookup"><span data-stu-id="586fd-219">d.</span></span> <span data-ttu-id="586fd-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="586fd-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="586fd-221">Создание тестового пользователя Allocadia</span><span class="sxs-lookup"><span data-stu-id="586fd-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="586fd-222">Приложение поддерживает JIT-подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="586fd-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="586fd-223">После проверки подлинности пользователей создаются в приложении hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="586fd-223">After authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="586fd-224">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="586fd-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="586fd-225">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAllocadia доступа.</span><span class="sxs-lookup"><span data-stu-id="586fd-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAllocadia.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="586fd-227">**tooassign tooAllocadia Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="586fd-227">**tooassign Britta Simon tooAllocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="586fd-228">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="586fd-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="586fd-230">В списке приложений hello выберите **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="586fd-230">In hello applications list, select **Allocadia**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="586fd-232">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="586fd-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="586fd-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="586fd-234">Click **Add** button.</span></span> <span data-ttu-id="586fd-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="586fd-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="586fd-237">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="586fd-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="586fd-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="586fd-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="586fd-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="586fd-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="586fd-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="586fd-240">Testing single sign-on</span></span>

<span data-ttu-id="586fd-241">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="586fd-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="586fd-242">При нажатии кнопки hello Allocadia плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Allocadia приложения.</span><span class="sxs-lookup"><span data-stu-id="586fd-242">When you click hello Allocadia tile in hello Access Panel, you should get automatically signed-on tooyour Allocadia application.</span></span>
<span data-ttu-id="586fd-243">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="586fd-243">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="586fd-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="586fd-244">Additional resources</span></span>

* [<span data-ttu-id="586fd-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="586fd-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="586fd-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="586fd-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

