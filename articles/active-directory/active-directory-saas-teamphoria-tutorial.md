---
title: "Руководство по интеграции Azure Active Directory с Teamphoria | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="dda77-103">Руководство по интеграции Azure Active Directory с Teamphoria</span><span class="sxs-lookup"><span data-stu-id="dda77-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="dda77-104">В этом учебнике вы узнаете, как toointegrate Teamphoria с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dda77-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dda77-105">Интеграция с Azure AD Teamphoria предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="dda77-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dda77-106">Можно управлять в Azure AD, имеющего доступ tooTeamphoria</span><span class="sxs-lookup"><span data-stu-id="dda77-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="dda77-107">Можно включить на пользователей tooautomatically get вошедшего tooTeamphoria (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda77-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dda77-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="dda77-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="dda77-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dda77-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="dda77-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dda77-110">Prerequisites</span></span>

<span data-ttu-id="dda77-111">tooconfigure интеграция Azure AD с Teamphoria требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="dda77-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="dda77-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dda77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dda77-113">подписка Teamphoria с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="dda77-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dda77-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="dda77-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dda77-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="dda77-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dda77-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="dda77-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="dda77-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dda77-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dda77-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dda77-118">Scenario description</span></span>
<span data-ttu-id="dda77-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dda77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dda77-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="dda77-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dda77-121">Добавление Teamphoria из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dda77-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="dda77-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="dda77-123">Добавление Teamphoria из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dda77-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="dda77-124">tooconfigure hello интеграции Teamphoria в Azure AD, вы должны tooadd Teamphoria из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dda77-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dda77-125">**tooadd Teamphoria из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dda77-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dda77-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dda77-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dda77-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="dda77-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dda77-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dda77-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dda77-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="dda77-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dda77-133">Введите в поле поиска hello **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="dda77-133">In hello search box, type **Teamphoria**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="dda77-135">В панели результатов hello выберите **Teamphoria**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="dda77-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dda77-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda77-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dda77-138">В этом разделе описана настройка и проверка единого входа Azure AD в Teamphoria с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dda77-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dda77-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Teamphoria является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dda77-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="dda77-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Teamphoria должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="dda77-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="dda77-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="dda77-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="dda77-142">tooconfigure и теста Azure AD единого входа с Teamphoria, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="dda77-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dda77-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="dda77-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dda77-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="dda77-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dda77-145">**[Создание тестового пользователя Teamphoria](#creating-a-teamphoria-test-user)**  -toohave аналог Саймон Britta в Teamphoria, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="dda77-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="dda77-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="dda77-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dda77-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dda77-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dda77-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda77-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dda77-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="dda77-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="dda77-150">**tooconfigure Azure AD единого входа с Teamphoria, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dda77-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="dda77-151">На портале управления Azure hello на hello **Teamphoria** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dda77-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dda77-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="dda77-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="dda77-155">На hello **URL-адреса и домена Teamphoria** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dda77-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="dda77-157">а.</span><span class="sxs-lookup"><span data-stu-id="dda77-157">a.</span></span> <span data-ttu-id="dda77-158">В hello **URL-адрес входа** textbox hello введите URL-адрес, используя следующий шаблон hello:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="dda77-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="dda77-159">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="dda77-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="dda77-160">Имеется tooupdate эти значения с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="dda77-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="dda77-161">Обратитесь к [группа поддержки клиента Teamphoria](https://www.teamphoria.com/) tooget hello входа URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="dda77-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="dda77-162">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и сохраните hello сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dda77-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="dda77-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dda77-164">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dda77-166">На hello **конфигурации Teamphoria** щелкните **Настройка Teamphoria** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="dda77-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dda77-167">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="dda77-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="dda77-169">tooconfigure единого входа на **Teamphoria** стороны, приложения Teamphoria tooyour входа в систему с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="dda77-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="dda77-170">Go слишком**параметры АДМИНИСТРИРОВАНИЯ** параметр в левой панели инструментов hello и постоянно hello hello, настройте нажмите на **ЕДИНОГО входа** tooopen hello SSO конфигурации окна.</span><span class="sxs-lookup"><span data-stu-id="dda77-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="dda77-172">Щелкните **Добавление ПОСТАВЩИКА УДОСТОВЕРЕНИЙ** параметр в форме hello tooopen hello правом верхнем углу для добавления параметров hello для единого входа.</span><span class="sxs-lookup"><span data-stu-id="dda77-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="dda77-174">Введите сведения о hello в полях hello, как описано ниже-</span><span class="sxs-lookup"><span data-stu-id="dda77-174">Enter hello details in hello fields as described below-</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="dda77-176">а.</span><span class="sxs-lookup"><span data-stu-id="dda77-176">a.</span></span> <span data-ttu-id="dda77-177">**ОТОБРАЖАЕМОЕ имя** : hello отображаемое имя подключаемого модуля hello на странице администрирования hello.</span><span class="sxs-lookup"><span data-stu-id="dda77-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="dda77-178">b.</span><span class="sxs-lookup"><span data-stu-id="dda77-178">b.</span></span> <span data-ttu-id="dda77-179">**ИМЯ кнопки** : hello имя вкладки hello, которая будет отображаться на странице входа hello для ведения журнала во единого входа.</span><span class="sxs-lookup"><span data-stu-id="dda77-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="dda77-180">c.</span><span class="sxs-lookup"><span data-stu-id="dda77-180">c.</span></span> <span data-ttu-id="dda77-181">**СЕРТИФИКАТ** : Привет открыть сертификата загружен ранее из hello портал Azure в блокноте, скопируйте содержимое hello hello же и вставьте его в поле hello.</span><span class="sxs-lookup"><span data-stu-id="dda77-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="dda77-182">d.</span><span class="sxs-lookup"><span data-stu-id="dda77-182">d.</span></span> <span data-ttu-id="dda77-183">**ТОЧКА входа** : hello вставить **SAML единого входа URL-адрес службы** копируются ранней формы hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dda77-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="dda77-184">д.</span><span class="sxs-lookup"><span data-stu-id="dda77-184">e.</span></span> <span data-ttu-id="dda77-185">Переключение hello параметр слишком**ON** и выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dda77-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dda77-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dda77-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="dda77-187">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="dda77-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dda77-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dda77-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dda77-190">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dda77-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dda77-192">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="dda77-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dda77-194">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="dda77-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dda77-196">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dda77-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dda77-198">а.</span><span class="sxs-lookup"><span data-stu-id="dda77-198">a.</span></span> <span data-ttu-id="dda77-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dda77-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dda77-200">b.</span><span class="sxs-lookup"><span data-stu-id="dda77-200">b.</span></span> <span data-ttu-id="dda77-201">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dda77-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dda77-202">c.</span><span class="sxs-lookup"><span data-stu-id="dda77-202">c.</span></span> <span data-ttu-id="dda77-203">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="dda77-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dda77-204">d.</span><span class="sxs-lookup"><span data-stu-id="dda77-204">d.</span></span> <span data-ttu-id="dda77-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dda77-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="dda77-206">Создание тестового пользователя Teamphoria</span><span class="sxs-lookup"><span data-stu-id="dda77-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="dda77-207">В порядке tooenable toolog пользователей Azure AD в Teamphoria их необходимо подготовить в Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="dda77-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="dda77-208">В случае Teamphoria hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="dda77-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="dda77-209">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="dda77-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="dda77-210">Войдите в систему tooyour Teamphoria сайт компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="dda77-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="dda77-211">Щелкните **АДМИНИСТРАТОРА** параметры на левой панели инструментов hello и внутри hello **УПРАВЛЕНИЕ** вкладке щелкните на **пользователей** страницу администрирования hello tooopen для пользователей.</span><span class="sxs-lookup"><span data-stu-id="dda77-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="dda77-213">Щелкните hello **ПРИГЛАСИТЬ вручную** параметр.</span><span class="sxs-lookup"><span data-stu-id="dda77-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="dda77-215">На этой странице сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="dda77-215">On this page, perform following action.</span></span> 
    
    ![Приглашение пользователей](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="dda77-217">а.</span><span class="sxs-lookup"><span data-stu-id="dda77-217">a.</span></span> <span data-ttu-id="dda77-218">В hello **адрес электронной почты** текстовом hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dda77-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dda77-219">b.</span><span class="sxs-lookup"><span data-stu-id="dda77-219">b.</span></span> <span data-ttu-id="dda77-220">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dda77-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="dda77-221">c.</span><span class="sxs-lookup"><span data-stu-id="dda77-221">c.</span></span> <span data-ttu-id="dda77-222">В hello **ФАМИЛИЯ** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dda77-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="dda77-223">d.</span><span class="sxs-lookup"><span data-stu-id="dda77-223">d.</span></span> <span data-ttu-id="dda77-224">Нажмите кнопку **INVITE 1 USER** (Пригласить одного пользователя).</span><span class="sxs-lookup"><span data-stu-id="dda77-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="dda77-225">Пользователь должен tooget приглашение hello tooaccept, созданные в системе hello.</span><span class="sxs-lookup"><span data-stu-id="dda77-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dda77-226">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="dda77-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dda77-227">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooTeamphoria доступа.</span><span class="sxs-lookup"><span data-stu-id="dda77-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dda77-229">**tooassign tooTeamphoria Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dda77-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="dda77-230">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dda77-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dda77-232">В списке приложений hello выберите **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="dda77-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="dda77-234">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="dda77-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dda77-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dda77-236">Click **Add** button.</span></span> <span data-ttu-id="dda77-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dda77-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dda77-239">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="dda77-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dda77-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dda77-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dda77-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dda77-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dda77-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dda77-242">Testing single sign-on</span></span>

<span data-ttu-id="dda77-243">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="dda77-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dda77-244">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="dda77-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="dda77-245">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="dda77-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dda77-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dda77-246">Additional resources</span></span>

* [<span data-ttu-id="dda77-247">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dda77-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dda77-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dda77-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

