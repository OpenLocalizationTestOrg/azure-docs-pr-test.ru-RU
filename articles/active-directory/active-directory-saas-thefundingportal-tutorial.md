---
title: "Учебник: Интеграция Azure Active Directory с hello финансирования портала | Документы Microsoft"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и hello финансирования портала."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="d58e1-103">Учебник: Интеграция Azure Active Directory с hello финансирования портала</span><span class="sxs-lookup"><span data-stu-id="d58e1-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="d58e1-104">В этом учебнике вы узнаете, как toointegrate hello финансирования портал с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d58e1-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d58e1-105">Интеграция hello финансирования портал с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d58e1-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d58e1-106">Можно управлять в Azure AD, имеющего доступ toohello Funding портала</span><span class="sxs-lookup"><span data-stu-id="d58e1-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="d58e1-107">Можно включить на пользователей tooautomatically get вошедшего toohello Funding портала (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="d58e1-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d58e1-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d58e1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d58e1-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d58e1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d58e1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d58e1-110">Prerequisites</span></span>

<span data-ttu-id="d58e1-111">Интеграция tooconfigure Azure AD с hello Funding портал, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d58e1-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="d58e1-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d58e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d58e1-113">Подписка, настроенная для hello финансирования портала единого входа</span><span class="sxs-lookup"><span data-stu-id="d58e1-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d58e1-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d58e1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d58e1-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d58e1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d58e1-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d58e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d58e1-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d58e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d58e1-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d58e1-118">Scenario description</span></span>
<span data-ttu-id="d58e1-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d58e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d58e1-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d58e1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d58e1-121">Добавление hello портала Funding из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d58e1-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="d58e1-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d58e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="d58e1-123">Добавление hello портала Funding из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d58e1-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="d58e1-124">tooconfigure hello интеграции hello Funding портала в Azure AD, вы должны tooadd hello портала Funding из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d58e1-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d58e1-125">**tooadd hello финансирования портала из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d58e1-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d58e1-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d58e1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d58e1-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d58e1-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d58e1-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d58e1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d58e1-133">Введите в поле поиска hello **hello финансирования портала**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="d58e1-135">В панели результатов hello выберите **hello финансирования портала**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d58e1-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d58e1-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d58e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d58e1-138">В этом разделе настройки и тестирования в Azure AD единого входа с портала финансирования на основании тестового пользователя с именем «Britta Simon» hello.</span><span class="sxs-lookup"><span data-stu-id="d58e1-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d58e1-139">Для единого входа toowork Azure AD необходима tooknow какой пользователь hello аналога в hello финансирования портал — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d58e1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="d58e1-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в hello финансирования портала должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d58e1-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="d58e1-141">В hello финансирования портала, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="d58e1-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d58e1-142">tooconfigure и теста Azure AD единого входа с hello Funding портала, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d58e1-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d58e1-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d58e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d58e1-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d58e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d58e1-145">**[Создание тестового пользователя портала финансирования hello](#creating-the-funding-portal-test-user)**  -toohave аналог Саймон Britta в hello Funding портал, который является представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="d58e1-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d58e1-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d58e1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d58e1-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d58e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d58e1-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d58e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d58e1-149">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в ваш портал финансирования приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d58e1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="d58e1-150">**tooconfigure Azure AD единого входа с hello финансирования портала, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d58e1-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="d58e1-151">В hello в hello портала Azure **hello финансирования портала** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d58e1-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d58e1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="d58e1-155">На hello **hello URL-адреса и домена финансирования портала** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d58e1-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="d58e1-157">а.</span><span class="sxs-lookup"><span data-stu-id="d58e1-157">a.</span></span> <span data-ttu-id="d58e1-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="d58e1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="d58e1-159">b.</span><span class="sxs-lookup"><span data-stu-id="d58e1-159">b.</span></span> <span data-ttu-id="d58e1-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="d58e1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d58e1-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d58e1-161">These values are not real.</span></span> <span data-ttu-id="d58e1-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d58e1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d58e1-163">Обратитесь к [hello финансирования клиента портал поддержки](mailto:info@regenteducation.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="d58e1-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="d58e1-164">Hello финансирования портала приложение ожидает toocontain утверждения SAML hello атрибут с именем «externalId1».</span><span class="sxs-lookup"><span data-stu-id="d58e1-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="d58e1-165">значение Hello «externalId1» должно быть распознаваемым идентификатором studentID.</span><span class="sxs-lookup"><span data-stu-id="d58e1-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="d58e1-166">Настройка утверждений hello «externalId1» для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="d58e1-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="d58e1-167">Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d58e1-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="d58e1-168">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="d58e1-168">hello following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="d58e1-170">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d58e1-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="d58e1-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="d58e1-171">Attribute Name</span></span> | <span data-ttu-id="d58e1-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="d58e1-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="d58e1-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="d58e1-173">externalId1</span></span> | <span data-ttu-id="d58e1-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="d58e1-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="d58e1-175">а.</span><span class="sxs-lookup"><span data-stu-id="d58e1-175">a.</span></span> <span data-ttu-id="d58e1-176">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d58e1-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d58e1-179">b.</span><span class="sxs-lookup"><span data-stu-id="d58e1-179">b.</span></span> <span data-ttu-id="d58e1-180">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="d58e1-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="d58e1-181">c.</span><span class="sxs-lookup"><span data-stu-id="d58e1-181">c.</span></span> <span data-ttu-id="d58e1-182">Из hello **значение атрибута** список, выберите hello атрибутом toouse вашей реализации.</span><span class="sxs-lookup"><span data-stu-id="d58e1-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="d58e1-183">Например если hello идентификатором StudentID значения были сохранены в hello ExtensionAttribute1, выберите user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="d58e1-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="d58e1-184">d.</span><span class="sxs-lookup"><span data-stu-id="d58e1-184">d.</span></span> <span data-ttu-id="d58e1-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="d58e1-186">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="d58e1-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="d58e1-188">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d58e1-188">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d58e1-190">tooconfigure единого входа на **hello финансирования портала** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[hello финансирования портал поддержки](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="d58e1-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="d58e1-191">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="d58e1-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d58e1-192">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="d58e1-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d58e1-193">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="d58e1-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d58e1-194">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d58e1-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d58e1-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d58e1-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="d58e1-196">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d58e1-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d58e1-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d58e1-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d58e1-199">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d58e1-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d58e1-201">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d58e1-203">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="d58e1-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d58e1-205">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d58e1-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d58e1-207">а.</span><span class="sxs-lookup"><span data-stu-id="d58e1-207">a.</span></span> <span data-ttu-id="d58e1-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d58e1-209">b.</span><span class="sxs-lookup"><span data-stu-id="d58e1-209">b.</span></span> <span data-ttu-id="d58e1-210">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d58e1-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d58e1-211">c.</span><span class="sxs-lookup"><span data-stu-id="d58e1-211">c.</span></span> <span data-ttu-id="d58e1-212">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d58e1-213">d.</span><span class="sxs-lookup"><span data-stu-id="d58e1-213">d.</span></span> <span data-ttu-id="d58e1-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="d58e1-215">Создание тестового пользователя портала финансирования hello</span><span class="sxs-lookup"><span data-stu-id="d58e1-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="d58e1-216">В этом разделе создайте пользователя с именем Britta Simon в hello Funding портала.</span><span class="sxs-lookup"><span data-stu-id="d58e1-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="d58e1-217">Работать с [hello финансирования портал поддержки](mailto:info@regenteducation.com) tooadd hello тестового пользователя и Включение единого входа.</span><span class="sxs-lookup"><span data-stu-id="d58e1-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d58e1-218">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d58e1-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d58e1-219">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа toohello Funding портала.</span><span class="sxs-lookup"><span data-stu-id="d58e1-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d58e1-221">**tooassign toohello Britta Simon Funding портала, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="d58e1-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="d58e1-222">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d58e1-224">В списке приложений hello выберите **hello финансирования портала**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="d58e1-226">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d58e1-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-228">Click **Add** button.</span></span> <span data-ttu-id="d58e1-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d58e1-231">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d58e1-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d58e1-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d58e1-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d58e1-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d58e1-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d58e1-234">Testing single sign-on</span></span>

<span data-ttu-id="d58e1-235">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="d58e1-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d58e1-236">При нажатии кнопки hello hello финансирования портала плитки в панели доступа hello, вы должны получить tooyour автоматически вошедшего hello финансирования портала приложения.</span><span class="sxs-lookup"><span data-stu-id="d58e1-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d58e1-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d58e1-237">Additional resources</span></span>

* [<span data-ttu-id="d58e1-238">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d58e1-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d58e1-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d58e1-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

