---
title: "Руководство по интеграции Azure Active Directory с Kantega SSO for Bitbucket | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kantega единого входа для Bitbucket."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c41cdaaf-0441-493c-94c7-569615b7b1ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: e86a9a9a42f2f80fe83191f113f6bab46cc8a37d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bitbucket"></a><span data-ttu-id="307a9-103">Руководство по интеграции Azure Active Directory с Kantega SSO for Bitbucket</span><span class="sxs-lookup"><span data-stu-id="307a9-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bitbucket</span></span>

<span data-ttu-id="307a9-104">В этом учебнике вы узнаете, как toointegrate Kantega единого входа для Bitbucket с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="307a9-104">In this tutorial, you learn how toointegrate Kantega SSO for Bitbucket with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="307a9-105">Интеграция с Azure AD Kantega единого входа для Bitbucket предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="307a9-105">Integrating Kantega SSO for Bitbucket with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="307a9-106">Можно управлять в Azure AD, имеющего доступ tooKantega единого входа для Bitbucket</span><span class="sxs-lookup"><span data-stu-id="307a9-106">You can control in Azure AD who has access tooKantega SSO for Bitbucket</span></span>
- <span data-ttu-id="307a9-107">Можно включить вашей пользователей tooautomatically get вошедшего tooKantega единого входа для Bitbucket (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="307a9-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bitbucket (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="307a9-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="307a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="307a9-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="307a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="307a9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="307a9-110">Prerequisites</span></span>

<span data-ttu-id="307a9-111">tooconfigure интеграция Azure AD с помощью единого входа Kantega для Bitbucket требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="307a9-111">tooconfigure Azure AD integration with Kantega SSO for Bitbucket, you need hello following items:</span></span>

- <span data-ttu-id="307a9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="307a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="307a9-113">подписка Kantega SSO for Bitbucket с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="307a9-113">A Kantega SSO for Bitbucket single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="307a9-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="307a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="307a9-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="307a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="307a9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="307a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="307a9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="307a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="307a9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="307a9-118">Scenario description</span></span>
<span data-ttu-id="307a9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="307a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="307a9-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="307a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="307a9-121">Добавление Kantega единого входа для Bitbucket из галереи hello</span><span class="sxs-lookup"><span data-stu-id="307a9-121">Adding Kantega SSO for Bitbucket from hello gallery</span></span>
2. <span data-ttu-id="307a9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="307a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bitbucket-from-hello-gallery"></a><span data-ttu-id="307a9-123">Добавление Kantega единого входа для Bitbucket из галереи hello</span><span class="sxs-lookup"><span data-stu-id="307a9-123">Adding Kantega SSO for Bitbucket from hello gallery</span></span>
<span data-ttu-id="307a9-124">tooconfigure hello интеграции единого входа Kantega для Bitbucket в Azure AD, необходимо tooadd Kantega единого входа для Bitbucket из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="307a9-124">tooconfigure hello integration of Kantega SSO for Bitbucket into Azure AD, you need tooadd Kantega SSO for Bitbucket from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="307a9-125">**tooadd Kantega единого входа для Bitbucket из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="307a9-125">**tooadd Kantega SSO for Bitbucket from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="307a9-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="307a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="307a9-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="307a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="307a9-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="307a9-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="307a9-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="307a9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="307a9-133">Введите в поле поиска hello **Kantega единого входа для Bitbucket**.</span><span class="sxs-lookup"><span data-stu-id="307a9-133">In hello search box, type **Kantega SSO for Bitbucket**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_search.png)

5. <span data-ttu-id="307a9-135">В панели результатов hello выберите **Kantega единого входа для Bitbucket**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="307a9-135">In hello results panel, select **Kantega SSO for Bitbucket**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="307a9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="307a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="307a9-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kantega SSO for Bitbucket с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="307a9-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bitbucket based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="307a9-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Kantega единого входа для Bitbucket является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="307a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bitbucket is tooa user in Azure AD.</span></span> <span data-ttu-id="307a9-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Kantega единого входа для Bitbucket должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="307a9-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bitbucket needs toobe established.</span></span>

<span data-ttu-id="307a9-141">В Kantega единого входа для Bitbucket, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="307a9-141">In Kantega SSO for Bitbucket, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="307a9-142">tooconfigure и выполнить проверку Azure AD единого входа с помощью единого входа Kantega Bitbucket, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="307a9-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bitbucket, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="307a9-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="307a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="307a9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="307a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="307a9-145">**[Создание Kantega единого входа для тестового пользователя Bitbucket](#creating-a-kantega-sso-for-bitbucket-test-user)**  -toohave аналог Саймон Britta в Kantega единого входа для Bitbucket, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="307a9-145">**[Creating a Kantega SSO for Bitbucket test user](#creating-a-kantega-sso-for-bitbucket-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bitbucket that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="307a9-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="307a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="307a9-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="307a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="307a9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="307a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="307a9-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей Kantega SSO для Bitbucket приложения.</span><span class="sxs-lookup"><span data-stu-id="307a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bitbucket application.</span></span>

<span data-ttu-id="307a9-150">**tooconfigure Azure AD единого входа с помощью единого входа Kantega для Bitbucket, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="307a9-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bitbucket, perform hello following steps:**</span></span>

1. <span data-ttu-id="307a9-151">В hello в hello портала Azure **Kantega единого входа для Bitbucket** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="307a9-151">In hello Azure portal, on hello **Kantega SSO for Bitbucket** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="307a9-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="307a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_samlbase.png)

3. <span data-ttu-id="307a9-155">В **IDP** инициировал режим на hello **Kantega единого входа для домена Bitbucket и URL-адреса** выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="307a9-155">In **IDP** initiated mode, on hello **Kantega SSO for Bitbucket Domain and URLs** section perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url1.png)

    <span data-ttu-id="307a9-157">а.</span><span class="sxs-lookup"><span data-stu-id="307a9-157">a.</span></span> <span data-ttu-id="307a9-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="307a9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="307a9-159">b.</span><span class="sxs-lookup"><span data-stu-id="307a9-159">b.</span></span> <span data-ttu-id="307a9-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="307a9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="307a9-161">В **SP** инициируемых режим, проверка **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="307a9-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url2.png)
    
    <span data-ttu-id="307a9-163">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="307a9-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="307a9-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="307a9-164">These values are not real.</span></span> <span data-ttu-id="307a9-165">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="307a9-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="307a9-166">Эти значения будут получены во время настройки hello Bitbucket подключаемого модуля, который описывается далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="307a9-166">These values are recieved during hello configuration of Bitbucket plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="307a9-167">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="307a9-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_certificate.png) 

6. <span data-ttu-id="307a9-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="307a9-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="307a9-171">В другом окне браузера войдите в портал администрирования Bitbucket tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="307a9-171">In a different web browser window, log in tooyour Bitbucket admin portal as an administrator.</span></span>

8. <span data-ttu-id="307a9-172">Щелкните шестеренки и выберите hello **найти новые надстройки**.</span><span class="sxs-lookup"><span data-stu-id="307a9-172">Click cog and click hello **Find new add-ons**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon1.png)

9. <span data-ttu-id="307a9-174">Поиск **Kantega единого входа Bitbucket SAML & Kerberos для** и нажмите кнопку **установить** tooinstall кнопку hello нового подключаемого модуля SAML.</span><span class="sxs-lookup"><span data-stu-id="307a9-174">Search **Kantega SSO for Bitbucket SAML & Kerberos** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon2.png)

10. <span data-ttu-id="307a9-176">запускает Hello установки подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="307a9-176">hello plugin installation starts.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon31.png)

11. <span data-ttu-id="307a9-178">После завершения установки hello.</span><span class="sxs-lookup"><span data-stu-id="307a9-178">Once hello installation is complete.</span></span> <span data-ttu-id="307a9-179">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="307a9-179">Click **Close**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon33.png)

12. <span data-ttu-id="307a9-181">Нажмите кнопку **Управление**.</span><span class="sxs-lookup"><span data-stu-id="307a9-181">Click **Manage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon34.png)
    
13. <span data-ttu-id="307a9-183">Нажмите кнопку **Настройка** tooconfigure hello нового подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="307a9-183">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon35.png)

14. <span data-ttu-id="307a9-185">В hello **SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="307a9-185">In hello **SAML** section.</span></span> <span data-ttu-id="307a9-186">Выберите **Azure Active Directory (Azure AD)** из hello **добавить поставщик удостоверений** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="307a9-186">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon4.png)

15. <span data-ttu-id="307a9-188">Выберите уровень подписки **Базовый**.</span><span class="sxs-lookup"><span data-stu-id="307a9-188">Select subscription level as **Basic**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon5.png)

16. <span data-ttu-id="307a9-190">На hello **свойства приложения** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="307a9-190">On hello **App properties** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon6.png)

    <span data-ttu-id="307a9-192">а.</span><span class="sxs-lookup"><span data-stu-id="307a9-192">a.</span></span> <span data-ttu-id="307a9-193">Копировать hello **URI идентификатора приложения** и использовать его как **идентификатор, URL-адрес ответа и URL-адрес входа** на hello **Kantega единого входа для домена Bitbucket и URL-адреса** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="307a9-193">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bitbucket Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="307a9-194">b.</span><span class="sxs-lookup"><span data-stu-id="307a9-194">b.</span></span> <span data-ttu-id="307a9-195">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="307a9-195">Click **Next**.</span></span>

17. <span data-ttu-id="307a9-196">На hello **импорта метаданных** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="307a9-196">On hello **Metadata import** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon7.png)

    <span data-ttu-id="307a9-198">а.</span><span class="sxs-lookup"><span data-stu-id="307a9-198">a.</span></span> <span data-ttu-id="307a9-199">Щелкните **Metadata file on my computer** (Файл метаданных на моем компьютере) и передайте файл метаданных, который вы скачали с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="307a9-199">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="307a9-200">b.</span><span class="sxs-lookup"><span data-stu-id="307a9-200">b.</span></span> <span data-ttu-id="307a9-201">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="307a9-201">Click **Next**.</span></span>

18. <span data-ttu-id="307a9-202">На hello **расположение единого входа и имя** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="307a9-202">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon8.png)

    <span data-ttu-id="307a9-204">а.</span><span class="sxs-lookup"><span data-stu-id="307a9-204">a.</span></span> <span data-ttu-id="307a9-205">Добавьте имя hello поставщика удостоверений в **имя поставщика удостоверений** текстового поля (например, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="307a9-205">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="307a9-206">b.</span><span class="sxs-lookup"><span data-stu-id="307a9-206">b.</span></span> <span data-ttu-id="307a9-207">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="307a9-207">Click **Next**.</span></span>

19. <span data-ttu-id="307a9-208">Проверьте сертификат подписи hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="307a9-208">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon9.png)

20. <span data-ttu-id="307a9-210">На hello **учетные записи пользователей Bitbucket** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="307a9-210">On hello **Bitbucket user accounts** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon10.png)

    <span data-ttu-id="307a9-212">а.</span><span class="sxs-lookup"><span data-stu-id="307a9-212">a.</span></span> <span data-ttu-id="307a9-213">Выберите **при необходимости создайте пользователей в каталоге внутренней Bitbucket** и введите соответствующее имя hello hello группы для пользователей (может быть несколько нет.</span><span class="sxs-lookup"><span data-stu-id="307a9-213">Select **Create users in Bitbucket's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="307a9-214">разделенных запятой).</span><span class="sxs-lookup"><span data-stu-id="307a9-214">of groups separated by comma).</span></span>

    <span data-ttu-id="307a9-215">b.</span><span class="sxs-lookup"><span data-stu-id="307a9-215">b.</span></span> <span data-ttu-id="307a9-216">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="307a9-216">Click **Next**.</span></span>

21. <span data-ttu-id="307a9-217">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="307a9-217">Click **Finish**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon11.png)

22. <span data-ttu-id="307a9-219">На hello **известные доменов для Azure AD** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="307a9-219">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon12.png)

    <span data-ttu-id="307a9-221">а.</span><span class="sxs-lookup"><span data-stu-id="307a9-221">a.</span></span> <span data-ttu-id="307a9-222">Выберите **известные домены** из hello левой панели страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="307a9-222">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="307a9-223">b.</span><span class="sxs-lookup"><span data-stu-id="307a9-223">b.</span></span> <span data-ttu-id="307a9-224">Введите имя домена в hello **известные домены** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="307a9-224">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="307a9-225">c.</span><span class="sxs-lookup"><span data-stu-id="307a9-225">c.</span></span> <span data-ttu-id="307a9-226">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="307a9-226">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="307a9-227">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="307a9-227">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="307a9-228">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="307a9-228">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="307a9-229">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="307a9-229">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="307a9-230">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="307a9-230">Creating an Azure AD test user</span></span>
<span data-ttu-id="307a9-231">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="307a9-231">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="307a9-233">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="307a9-233">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="307a9-234">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="307a9-234">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="307a9-236">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="307a9-236">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="307a9-238">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="307a9-238">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="307a9-240">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="307a9-240">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="307a9-242">а.</span><span class="sxs-lookup"><span data-stu-id="307a9-242">a.</span></span> <span data-ttu-id="307a9-243">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="307a9-243">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="307a9-244">b.</span><span class="sxs-lookup"><span data-stu-id="307a9-244">b.</span></span> <span data-ttu-id="307a9-245">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="307a9-245">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="307a9-246">c.</span><span class="sxs-lookup"><span data-stu-id="307a9-246">c.</span></span> <span data-ttu-id="307a9-247">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="307a9-247">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="307a9-248">d.</span><span class="sxs-lookup"><span data-stu-id="307a9-248">d.</span></span> <span data-ttu-id="307a9-249">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="307a9-249">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bitbucket-test-user"></a><span data-ttu-id="307a9-250">Создание тестового пользователя Kantega SSO for Bitbucket</span><span class="sxs-lookup"><span data-stu-id="307a9-250">Creating a Kantega SSO for Bitbucket test user</span></span>

<span data-ttu-id="307a9-251">Пользователи toolog tooenable Azure AD в tooBitbucket, их необходимо подготовить в Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="307a9-251">tooenable Azure AD users toolog in tooBitbucket, they must be provisioned into Bitbucket.</span></span> <span data-ttu-id="307a9-252">В Kantega SSO for Bitbucket подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="307a9-252">In Kantega SSO for Bitbucket, provisioning is a manual task.</span></span>

<span data-ttu-id="307a9-253">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="307a9-253">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="307a9-254">Войдите в систему tooyour Bitbucket сайт компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="307a9-254">Log in tooyour Bitbucket company site as an administrator.</span></span>

2. <span data-ttu-id="307a9-255">Щелкните значок параметров.</span><span class="sxs-lookup"><span data-stu-id="307a9-255">Click on settings icon.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user1.png) 

3. <span data-ttu-id="307a9-257">В разделе **Administration** (Администрирование) щелкните **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="307a9-257">Under **Administration** tab section, click **Users**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user2.png)

4. <span data-ttu-id="307a9-259">Щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="307a9-259">Click **Create user**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user3.png)     

5. <span data-ttu-id="307a9-261">На hello **Create User** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="307a9-261">On hello **Create User** dialog page, perform hello following steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user4.png) 

    <span data-ttu-id="307a9-263">а.</span><span class="sxs-lookup"><span data-stu-id="307a9-263">a.</span></span> <span data-ttu-id="307a9-264">В hello **Username** электронной почты hello тип пользователя в текстовое поле, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="307a9-264">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="307a9-265">b.</span><span class="sxs-lookup"><span data-stu-id="307a9-265">b.</span></span> <span data-ttu-id="307a9-266">В hello **полное имя** текстовое поле, полное имя типа пользователя hello как Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="307a9-266">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="307a9-267">c.</span><span class="sxs-lookup"><span data-stu-id="307a9-267">c.</span></span> <span data-ttu-id="307a9-268">В hello **адрес электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="307a9-268">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="307a9-269">d.</span><span class="sxs-lookup"><span data-stu-id="307a9-269">d.</span></span> <span data-ttu-id="307a9-270">В hello **пароль** текстового поля, типа hello пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="307a9-270">In hello **Password** textbox, type hello password of user.</span></span>  

    <span data-ttu-id="307a9-271">д.</span><span class="sxs-lookup"><span data-stu-id="307a9-271">e.</span></span> <span data-ttu-id="307a9-272">В hello **подтверждение пароля** текстовом поле введите hello пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="307a9-272">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>

    <span data-ttu-id="307a9-273">f.</span><span class="sxs-lookup"><span data-stu-id="307a9-273">f.</span></span> <span data-ttu-id="307a9-274">Щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="307a9-274">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="307a9-275">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="307a9-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="307a9-276">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooKantega единого входа для Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="307a9-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bitbucket.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="307a9-278">**tooassign tooKantega Britta Simon единого входа для Bitbucket, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="307a9-278">**tooassign Britta Simon tooKantega SSO for Bitbucket, perform hello following steps:**</span></span>

1. <span data-ttu-id="307a9-279">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="307a9-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="307a9-281">В списке приложений hello выберите **Kantega единого входа для Bitbucket**.</span><span class="sxs-lookup"><span data-stu-id="307a9-281">In hello applications list, select **Kantega SSO for Bitbucket**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_app.png) 

3. <span data-ttu-id="307a9-283">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="307a9-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="307a9-285">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="307a9-285">Click **Add** button.</span></span> <span data-ttu-id="307a9-286">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="307a9-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="307a9-288">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="307a9-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="307a9-289">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="307a9-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="307a9-290">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="307a9-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="307a9-291">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="307a9-291">Testing single sign-on</span></span>

<span data-ttu-id="307a9-292">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="307a9-292">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="307a9-293">При нажатии кнопки hello Kantega единого входа для Bitbucket плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Kantega единого входа для приложения Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="307a9-293">When you click hello Kantega SSO for Bitbucket tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bitbucket application.</span></span>
<span data-ttu-id="307a9-294">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="307a9-294">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="307a9-295">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="307a9-295">Additional resources</span></span>

* [<span data-ttu-id="307a9-296">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="307a9-296">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="307a9-297">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="307a9-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_203.png

