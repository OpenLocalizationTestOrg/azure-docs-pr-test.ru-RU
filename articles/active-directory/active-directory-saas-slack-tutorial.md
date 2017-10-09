---
title: "Руководство по интеграции Azure Active Directory с приложением Slack | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Slack."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="efa64-103">Учебник. Интеграция Azure Active Directory с Slack</span><span class="sxs-lookup"><span data-stu-id="efa64-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="efa64-104">В этом учебнике вы узнаете, как toointegrate временных резервов в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="efa64-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="efa64-105">Интеграция Slack с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="efa64-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="efa64-106">Можно управлять в Azure AD, имеющего доступ tooSlack</span><span class="sxs-lookup"><span data-stu-id="efa64-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="efa64-107">Можно включить на пользователей tooautomatically get вошедшего tooSlack (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa64-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="efa64-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="efa64-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="efa64-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="efa64-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efa64-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="efa64-110">Prerequisites</span></span>

<span data-ttu-id="efa64-111">tooconfigure интеграция Azure AD с Slack требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="efa64-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="efa64-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="efa64-112">An Azure AD subscription</span></span>
- <span data-ttu-id="efa64-113">подписка Slack с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="efa64-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="efa64-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="efa64-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="efa64-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="efa64-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="efa64-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="efa64-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="efa64-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efa64-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="efa64-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="efa64-118">Scenario description</span></span>
<span data-ttu-id="efa64-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="efa64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="efa64-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="efa64-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="efa64-121">Добавление Slack из галереи hello</span><span class="sxs-lookup"><span data-stu-id="efa64-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="efa64-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa64-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="efa64-123">Добавление Slack из галереи hello</span><span class="sxs-lookup"><span data-stu-id="efa64-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="efa64-124">Интеграция hello tooconfigure резерва в Azure AD, необходимо tooadd Slack из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="efa64-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="efa64-125">**tooadd Slack из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="efa64-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="efa64-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="efa64-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="efa64-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="efa64-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="efa64-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="efa64-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="efa64-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="efa64-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="efa64-133">Введите в поле поиска hello **Slack**.</span><span class="sxs-lookup"><span data-stu-id="efa64-133">In hello search box, type **Slack**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="efa64-135">В панели результатов hello выберите **Slack**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="efa64-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="efa64-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa64-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="efa64-138">В этом разделе описана настройка и проверка единого входа Azure AD в Slack с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efa64-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="efa64-139">Для единого входа toowork Azure AD необходима tooknow какой пользователь hello аналога в Slack — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efa64-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="efa64-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Slack должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="efa64-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="efa64-141">В Slack, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="efa64-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="efa64-142">tooconfigure и теста Azure AD единого входа с Slack, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="efa64-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="efa64-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="efa64-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="efa64-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="efa64-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="efa64-145">**[Создание резерв тестового пользователя](#creating-a-slack-test-user)**  -toohave аналог Саймон Britta в Slack, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="efa64-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="efa64-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="efa64-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="efa64-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="efa64-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="efa64-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa64-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="efa64-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении резерв.</span><span class="sxs-lookup"><span data-stu-id="efa64-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="efa64-150">**tooconfigure Azure AD единого входа с Slack, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="efa64-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="efa64-151">В hello в hello портала Azure **Slack** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="efa64-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="efa64-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="efa64-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="efa64-155">На hello **URL-адреса и домена Slack** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="efa64-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="efa64-157">а.</span><span class="sxs-lookup"><span data-stu-id="efa64-157">a.</span></span> <span data-ttu-id="efa64-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="efa64-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="efa64-159">b.</span><span class="sxs-lookup"><span data-stu-id="efa64-159">b.</span></span> <span data-ttu-id="efa64-160">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="efa64-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="efa64-161">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="efa64-161">hello value is not real.</span></span> <span data-ttu-id="efa64-162">У вас есть tooupdate hello значение hello фактическое на URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="efa64-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="efa64-163">Обратитесь к [Slack поддержки](https://slack.com/help/contact) значение tooget hello</span><span class="sxs-lookup"><span data-stu-id="efa64-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="efa64-164">Резерв приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="efa64-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="efa64-165">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="efa64-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="efa64-166">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="efa64-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="efa64-167">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="efa64-167">hello following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="efa64-169">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна выберите **user.mail** как **идентификатор пользователя** и для каждой строки показано в следующей таблице hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="efa64-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="efa64-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="efa64-170">Attribute Name</span></span> | <span data-ttu-id="efa64-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="efa64-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="efa64-172">first_name</span><span class="sxs-lookup"><span data-stu-id="efa64-172">first_name</span></span> | <span data-ttu-id="efa64-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="efa64-173">user.givenname</span></span> |
    | <span data-ttu-id="efa64-174">last_name</span><span class="sxs-lookup"><span data-stu-id="efa64-174">last_name</span></span> | <span data-ttu-id="efa64-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="efa64-175">user.surname</span></span> |
    | <span data-ttu-id="efa64-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="efa64-176">User.Email</span></span> | <span data-ttu-id="efa64-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="efa64-177">user.mail</span></span> |  
    | <span data-ttu-id="efa64-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="efa64-178">User.Username</span></span> | <span data-ttu-id="efa64-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="efa64-179">user.userprincipalname</span></span> |

    <span data-ttu-id="efa64-180">а.</span><span class="sxs-lookup"><span data-stu-id="efa64-180">a.</span></span> <span data-ttu-id="efa64-181">Щелкните **атрибута** tooopen **изменение атрибута** диалогового окна введите и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="efa64-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="efa64-183">а.</span><span class="sxs-lookup"><span data-stu-id="efa64-183">a.</span></span> <span data-ttu-id="efa64-184">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="efa64-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="efa64-185">b.</span><span class="sxs-lookup"><span data-stu-id="efa64-185">b.</span></span> <span data-ttu-id="efa64-186">Из hello **значение** список, выберите hello значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="efa64-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="efa64-187">c.</span><span class="sxs-lookup"><span data-stu-id="efa64-187">c.</span></span> <span data-ttu-id="efa64-188">Щелкните **ОК**</span><span class="sxs-lookup"><span data-stu-id="efa64-188">Click **OK**</span></span>

6. <span data-ttu-id="efa64-189">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="efa64-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="efa64-191">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="efa64-191">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="efa64-193">На hello **конфигурации Slack** щелкните **Настройка Slack** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="efa64-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="efa64-194">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="efa64-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="efa64-196">В другом окне браузера войдите в tooyour корпоративный сайт Slack в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="efa64-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="efa64-197">Перейдите в слишком**Microsoft Azure AD** перейдите слишком**параметры командного**.</span><span class="sxs-lookup"><span data-stu-id="efa64-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="efa64-199">В hello **параметры командного** щелкните hello **проверки подлинности** , а затем щелкните **изменение параметров**.</span><span class="sxs-lookup"><span data-stu-id="efa64-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="efa64-201">На hello **параметры проверки подлинности SAML** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="efa64-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="efa64-203">а.</span><span class="sxs-lookup"><span data-stu-id="efa64-203">a.</span></span>  <span data-ttu-id="efa64-204">В hello **конечная точка SAML 2.0 (HTTP)** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="efa64-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="efa64-205">b.</span><span class="sxs-lookup"><span data-stu-id="efa64-205">b.</span></span>  <span data-ttu-id="efa64-206">В hello **издатель поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="efa64-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="efa64-207">c.</span><span class="sxs-lookup"><span data-stu-id="efa64-207">c.</span></span>  <span data-ttu-id="efa64-208">Откройте загруженный сертификат файл в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **открытый сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="efa64-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="efa64-209">d.</span><span class="sxs-lookup"><span data-stu-id="efa64-209">d.</span></span> <span data-ttu-id="efa64-210">Задайте нужные команды резерв hello выше три параметра.</span><span class="sxs-lookup"><span data-stu-id="efa64-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="efa64-211">Дополнительные сведения о параметрах hello приведено hello **руководство по выбору конфигурации единого входа в Slack** здесь.</span><span class="sxs-lookup"><span data-stu-id="efa64-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="efa64-212">д.</span><span class="sxs-lookup"><span data-stu-id="efa64-212">e.</span></span>  <span data-ttu-id="efa64-213">Щелкните **Сохранить конфигурацию**.</span><span class="sxs-lookup"><span data-stu-id="efa64-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="efa64-214">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="efa64-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="efa64-215">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="efa64-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="efa64-216">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="efa64-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="efa64-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="efa64-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="efa64-218">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="efa64-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="efa64-220">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="efa64-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="efa64-221">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="efa64-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="efa64-223">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="efa64-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="efa64-225">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="efa64-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="efa64-227">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="efa64-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="efa64-229">а.</span><span class="sxs-lookup"><span data-stu-id="efa64-229">a.</span></span> <span data-ttu-id="efa64-230">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="efa64-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="efa64-231">b.</span><span class="sxs-lookup"><span data-stu-id="efa64-231">b.</span></span> <span data-ttu-id="efa64-232">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="efa64-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="efa64-233">c.</span><span class="sxs-lookup"><span data-stu-id="efa64-233">c.</span></span> <span data-ttu-id="efa64-234">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="efa64-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="efa64-235">d.</span><span class="sxs-lookup"><span data-stu-id="efa64-235">d.</span></span> <span data-ttu-id="efa64-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="efa64-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="efa64-237">Создание тестового пользователя Slack</span><span class="sxs-lookup"><span data-stu-id="efa64-237">Creating a Slack test user</span></span>

<span data-ttu-id="efa64-238">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Slack.</span><span class="sxs-lookup"><span data-stu-id="efa64-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="efa64-239">Приложение Slack поддерживает JIT подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="efa64-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="efa64-240">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="efa64-240">There is no action item for you in this section.</span></span> <span data-ttu-id="efa64-241">Новый пользователь создается во время попытки tooaccess Slack, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="efa64-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="efa64-242">Если требуется toocreate пользователя вручную, необходимо tooContact [Slack поддержки](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="efa64-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="efa64-243">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="efa64-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="efa64-244">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSlack доступа.</span><span class="sxs-lookup"><span data-stu-id="efa64-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="efa64-246">**tooassign tooSlack Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="efa64-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="efa64-247">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="efa64-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="efa64-249">В списке приложений hello выберите **Slack**.</span><span class="sxs-lookup"><span data-stu-id="efa64-249">In hello applications list, select **Slack**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="efa64-251">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="efa64-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="efa64-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="efa64-253">Click **Add** button.</span></span> <span data-ttu-id="efa64-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="efa64-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="efa64-256">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="efa64-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="efa64-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="efa64-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="efa64-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="efa64-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="efa64-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="efa64-259">Testing single sign-on</span></span>

<span data-ttu-id="efa64-260">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="efa64-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="efa64-261">При нажатии кнопки hello резерв плитки в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour резерв приложения.</span><span class="sxs-lookup"><span data-stu-id="efa64-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efa64-262">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="efa64-262">Additional resources</span></span>

* [<span data-ttu-id="efa64-263">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efa64-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efa64-264">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="efa64-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

