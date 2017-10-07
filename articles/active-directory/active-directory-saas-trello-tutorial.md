---
title: "Руководство по интеграции Azure Active Directory с Trello | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="273e3-103">Руководство. Интеграция Azure Active Directory с Trello</span><span class="sxs-lookup"><span data-stu-id="273e3-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="273e3-104">В этом учебнике вы узнаете, как toointegrate Trello с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="273e3-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="273e3-105">Интеграция Trello с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="273e3-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="273e3-106">Можно управлять в Azure AD, имеющего доступ tooTrello</span><span class="sxs-lookup"><span data-stu-id="273e3-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="273e3-107">Можно включить на пользователей tooautomatically get вошедшего tooTrello (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="273e3-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="273e3-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="273e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="273e3-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="273e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="273e3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="273e3-110">Prerequisites</span></span>

<span data-ttu-id="273e3-111">tooconfigure интеграция Azure AD с Trello требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="273e3-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="273e3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="273e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="273e3-113">подписка Trello с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="273e3-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="273e3-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="273e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="273e3-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="273e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="273e3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="273e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="273e3-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="273e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="273e3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="273e3-118">Scenario description</span></span>
<span data-ttu-id="273e3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="273e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="273e3-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="273e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="273e3-121">Добавление Trello из галереи hello</span><span class="sxs-lookup"><span data-stu-id="273e3-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="273e3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="273e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="273e3-123">Добавление Trello из галереи hello</span><span class="sxs-lookup"><span data-stu-id="273e3-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="273e3-124">tooconfigure hello интеграции Trello в Azure AD, вы должны tooadd Trello из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="273e3-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="273e3-125">**tooadd Trello из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="273e3-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="273e3-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="273e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="273e3-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="273e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="273e3-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="273e3-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="273e3-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="273e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="273e3-133">Введите в поле поиска hello **Trello**.</span><span class="sxs-lookup"><span data-stu-id="273e3-133">In hello search box, type **Trello**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="273e3-135">В панели результатов hello выберите **Trello**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="273e3-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="273e3-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="273e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="273e3-138">В этом разделе описана настройка и проверка единого входа Azure AD в Trello с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="273e3-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="273e3-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Trello является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="273e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="273e3-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Trello должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="273e3-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="273e3-141">В Trello, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="273e3-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="273e3-142">tooconfigure и теста Azure AD единого входа с Trello, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="273e3-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="273e3-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="273e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="273e3-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="273e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="273e3-145">**[Создание тестового пользователя Trello](#creating-a-trello-test-user)**  -toohave аналог Саймон Britta в Trello, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="273e3-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="273e3-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="273e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="273e3-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="273e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="273e3-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="273e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="273e3-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Trello.</span><span class="sxs-lookup"><span data-stu-id="273e3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="273e3-150">**Azure AD tooconfigure единого входа с Trello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="273e3-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="273e3-151">В hello в hello портала Azure **Trello** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="273e3-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="273e3-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="273e3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="273e3-155">На hello **URL-адреса и домена Trello** статьи, при желании tooconfigure приложения hello в **режиме, инициированный IDP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="273e3-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="273e3-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="273e3-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="273e3-158">На hello **URL-адреса и домена Trello** статьи, при желании tooconfigure приложения hello в **режиме, инициируемая SP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="273e3-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="273e3-160">а.</span><span class="sxs-lookup"><span data-stu-id="273e3-160">a.</span></span> <span data-ttu-id="273e3-161">Щелкните hello **Показывать дополнительные параметры URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="273e3-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="273e3-162">b.</span><span class="sxs-lookup"><span data-stu-id="273e3-162">b.</span></span> <span data-ttu-id="273e3-163">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="273e3-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="273e3-164">Вы должны получить hello  **\<enterprise\>**  slug из Trello.</span><span class="sxs-lookup"><span data-stu-id="273e3-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="273e3-165">Если у вас нет значение slug hello, обратитесь в службу [Trello поддержки](mailto:support@trello.com) tooget hello slug для вас предприятия.</span><span class="sxs-lookup"><span data-stu-id="273e3-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="273e3-166">Trello приложение ожидает, что определенные атрибуты утверждения SAML toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="273e3-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="273e3-167">Настройте следующие атрибуты для данного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="273e3-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="273e3-168">Вы можете управлять hello значения этих атрибутов из hello **«Атрибуты пользователя»** приложения hello.</span><span class="sxs-lookup"><span data-stu-id="273e3-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="273e3-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="273e3-169">hello following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="273e3-171">На hello **атрибутов токена SAML** диалоговое окно, для каждой строки, показано в следующей таблице hello выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="273e3-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="273e3-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="273e3-172">Attribute Name</span></span> | <span data-ttu-id="273e3-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="273e3-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="273e3-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="273e3-174">User.Email</span></span> | <span data-ttu-id="273e3-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="273e3-175">user.mail</span></span> |
    | <span data-ttu-id="273e3-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="273e3-176">User.FirstName</span></span> | <span data-ttu-id="273e3-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="273e3-177">user.givenname</span></span> |
    | <span data-ttu-id="273e3-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="273e3-178">User.LastName</span></span> | <span data-ttu-id="273e3-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="273e3-179">user.surname</span></span> |

    <span data-ttu-id="273e3-180">а.</span><span class="sxs-lookup"><span data-stu-id="273e3-180">a.</span></span> <span data-ttu-id="273e3-181">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="273e3-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="273e3-184">b.</span><span class="sxs-lookup"><span data-stu-id="273e3-184">b.</span></span> <span data-ttu-id="273e3-185">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="273e3-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="273e3-186">c.</span><span class="sxs-lookup"><span data-stu-id="273e3-186">c.</span></span> <span data-ttu-id="273e3-187">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="273e3-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="273e3-188">d.</span><span class="sxs-lookup"><span data-stu-id="273e3-188">d.</span></span> <span data-ttu-id="273e3-189">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="273e3-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="273e3-190">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="273e3-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="273e3-192">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="273e3-192">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="273e3-194">На hello **конфигурации Trello** щелкните **Настройка Trello** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="273e3-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="273e3-195">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="273e3-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="273e3-197">tooget единого входа, настроенному для вашего приложения перейдите слишком[настройки единого входа предприятия в Trello](https://trello.com/sso-configuration) toosend страницы [Trello поддержки](mailto:support@trello.com) hello **SAML единого входа URL-адрес службы** и Присоединение hello **сертификата (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="273e3-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="273e3-198">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="273e3-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="273e3-199">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="273e3-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="273e3-200">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="273e3-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="273e3-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="273e3-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="273e3-202">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="273e3-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="273e3-204">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="273e3-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="273e3-205">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="273e3-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="273e3-207">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="273e3-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="273e3-209">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="273e3-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="273e3-211">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="273e3-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="273e3-213">а.</span><span class="sxs-lookup"><span data-stu-id="273e3-213">a.</span></span> <span data-ttu-id="273e3-214">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="273e3-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="273e3-215">b.</span><span class="sxs-lookup"><span data-stu-id="273e3-215">b.</span></span> <span data-ttu-id="273e3-216">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="273e3-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="273e3-217">c.</span><span class="sxs-lookup"><span data-stu-id="273e3-217">c.</span></span> <span data-ttu-id="273e3-218">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="273e3-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="273e3-219">d.</span><span class="sxs-lookup"><span data-stu-id="273e3-219">d.</span></span> <span data-ttu-id="273e3-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="273e3-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="273e3-221">Создание тестового пользователя приложения Trello</span><span class="sxs-lookup"><span data-stu-id="273e3-221">Creating a Trello test user</span></span>

<span data-ttu-id="273e3-222">В этом разделе описано, как создать пользователя Britta Simon в приложении Trello.</span><span class="sxs-lookup"><span data-stu-id="273e3-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="273e3-223">В этом разделе описано, как создать пользователя Britta Simon в приложении Trello.</span><span class="sxs-lookup"><span data-stu-id="273e3-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="273e3-224">Trello поддерживает подготовку just-in-time и новую учетную запись создается hello при первом входе из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="273e3-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="273e3-225">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="273e3-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="273e3-226">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTrello доступа.</span><span class="sxs-lookup"><span data-stu-id="273e3-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="273e3-228">**tooassign tooTrello Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="273e3-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="273e3-229">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="273e3-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="273e3-231">В списке приложений hello выберите **Trello**.</span><span class="sxs-lookup"><span data-stu-id="273e3-231">In hello applications list, select **Trello**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="273e3-233">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="273e3-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="273e3-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="273e3-235">Click **Add** button.</span></span> <span data-ttu-id="273e3-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="273e3-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="273e3-238">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="273e3-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="273e3-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="273e3-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="273e3-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="273e3-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="273e3-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="273e3-241">Testing single sign-on</span></span>

<span data-ttu-id="273e3-242">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="273e3-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="273e3-243">При нажатии кнопки hello Trello плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Trello.</span><span class="sxs-lookup"><span data-stu-id="273e3-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="273e3-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="273e3-244">Additional resources</span></span>

* [<span data-ttu-id="273e3-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="273e3-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="273e3-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="273e3-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

