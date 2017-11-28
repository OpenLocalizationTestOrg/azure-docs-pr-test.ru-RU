---
title: "Руководство по интеграции Azure Active Directory с Kantega SSO for Bamboo | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kantega единого входа для Bamboo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="119fe-103">Руководство по интеграции Azure Active Directory с Kantega SSO for Bamboo</span><span class="sxs-lookup"><span data-stu-id="119fe-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="119fe-104">В этом учебнике вы узнаете, как toointegrate Kantega единого входа для Bamboo в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="119fe-104">In this tutorial, you learn how toointegrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="119fe-105">Интеграция с Azure AD Kantega единого входа для Bamboo предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="119fe-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="119fe-106">Можно управлять в Azure AD, имеющего доступ tooKantega единого входа для Bamboo</span><span class="sxs-lookup"><span data-stu-id="119fe-106">You can control in Azure AD who has access tooKantega SSO for Bamboo</span></span>
- <span data-ttu-id="119fe-107">Можно включить на пользователей tooautomatically get вошедшего tooKantega единого входа для Bamboo (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="119fe-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="119fe-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="119fe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="119fe-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="119fe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="119fe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="119fe-110">Prerequisites</span></span>

<span data-ttu-id="119fe-111">tooconfigure интеграция Azure AD с помощью единого входа Kantega для Bamboo требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="119fe-111">tooconfigure Azure AD integration with Kantega SSO for Bamboo, you need hello following items:</span></span>

- <span data-ttu-id="119fe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="119fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="119fe-113">подписка Kantega SSO for Bamboo с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="119fe-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="119fe-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="119fe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="119fe-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="119fe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="119fe-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="119fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="119fe-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="119fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="119fe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="119fe-118">Scenario description</span></span>
<span data-ttu-id="119fe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="119fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="119fe-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="119fe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="119fe-121">Добавление Kantega единого входа для Bamboo из галереи hello</span><span class="sxs-lookup"><span data-stu-id="119fe-121">Adding Kantega SSO for Bamboo from hello gallery</span></span>
2. <span data-ttu-id="119fe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="119fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a><span data-ttu-id="119fe-123">Добавление Kantega единого входа для Bamboo из галереи hello</span><span class="sxs-lookup"><span data-stu-id="119fe-123">Adding Kantega SSO for Bamboo from hello gallery</span></span>
<span data-ttu-id="119fe-124">tooconfigure hello интеграции Kantega SSO Bamboo в Azure AD, необходимо tooadd Kantega единого входа для Bamboo из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="119fe-124">tooconfigure hello integration of Kantega SSO for Bamboo into Azure AD, you need tooadd Kantega SSO for Bamboo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="119fe-125">**tooadd Kantega единого входа для Bamboo из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="119fe-125">**tooadd Kantega SSO for Bamboo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="119fe-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="119fe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="119fe-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="119fe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="119fe-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="119fe-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="119fe-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="119fe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="119fe-133">Введите в поле поиска hello **Kantega единого входа для Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="119fe-133">In hello search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="119fe-135">В панели результатов hello выберите **Kantega единого входа для Bamboo**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="119fe-135">In hello results panel, select **Kantega SSO for Bamboo**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="119fe-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="119fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="119fe-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kantega SSO for Bamboo с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="119fe-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="119fe-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Kantega SSO Bamboo является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="119fe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bamboo is tooa user in Azure AD.</span></span> <span data-ttu-id="119fe-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Kantega SSO Bamboo должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="119fe-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bamboo needs toobe established.</span></span>

<span data-ttu-id="119fe-141">В Kantega единого входа для Bamboo, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="119fe-141">In Kantega SSO for Bamboo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="119fe-142">tooconfigure и выполнить проверку Azure AD единого входа с помощью единого входа Kantega Bamboo, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="119fe-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="119fe-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="119fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="119fe-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="119fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="119fe-145">**[Создание Kantega единого входа для тестового пользователя Bamboo](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave аналог Саймон Britta в Kantega единого входа для Bamboo, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="119fe-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="119fe-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="119fe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="119fe-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="119fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="119fe-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="119fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="119fe-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей Kantega SSO для Bamboo приложения.</span><span class="sxs-lookup"><span data-stu-id="119fe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="119fe-150">**tooconfigure Azure AD единого входа с помощью единого входа Kantega для Bamboo, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="119fe-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="119fe-151">В hello в hello портала Azure **Kantega единого входа для Bamboo** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="119fe-151">In hello Azure portal, on hello **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="119fe-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="119fe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="119fe-155">В **IDP** инициировал режим на hello **Kantega единого входа для домена Bamboo и URL-адреса** выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="119fe-155">In **IDP** initiated mode, on hello **Kantega SSO for Bamboo Domain and URLs** section perform hello following step :</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="119fe-157">а.</span><span class="sxs-lookup"><span data-stu-id="119fe-157">a.</span></span> <span data-ttu-id="119fe-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="119fe-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="119fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="119fe-159">b.</span></span> <span data-ttu-id="119fe-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="119fe-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="119fe-161">В **SP** инициируемых режим, проверка **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="119fe-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step :</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="119fe-163">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="119fe-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="119fe-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="119fe-164">These values are not real.</span></span> <span data-ttu-id="119fe-165">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="119fe-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="119fe-166">Эти значения будут получены во время настройки hello Bamboo подключаемого модуля, который описывается далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="119fe-166">These values are recieved during hello configuration of Bamboo plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="119fe-167">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="119fe-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="119fe-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="119fe-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="119fe-171">В другом окне браузера войдите в tooyour Bamboo на локальном сервере, с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="119fe-171">In a different web browser window, log in tooyour Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="119fe-172">Наведите указатель мыши на шестеренки и выберите hello **надстройки**.</span><span class="sxs-lookup"><span data-stu-id="119fe-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="119fe-174">На вкладке "Add-ons" (Надстройки) щелкните **Find new add-ons** (Найти новые надстройки).</span><span class="sxs-lookup"><span data-stu-id="119fe-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="119fe-175">Поиск **Kantega единого входа для Bamboo SAML (Kerberos)** и нажмите кнопку **установить** tooinstall кнопку hello нового подключаемого модуля SAML.</span><span class="sxs-lookup"><span data-stu-id="119fe-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="119fe-177">Установка подключаемого модуля Hello начнется.</span><span class="sxs-lookup"><span data-stu-id="119fe-177">hello plugin installation will start.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="119fe-179">После завершения установки hello.</span><span class="sxs-lookup"><span data-stu-id="119fe-179">Once hello installation is complete.</span></span> <span data-ttu-id="119fe-180">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="119fe-180">Click **Close**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="119fe-182">Нажмите кнопку **Управление**.</span><span class="sxs-lookup"><span data-stu-id="119fe-182">Click **Manage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="119fe-184">Нажмите кнопку **Настройка** tooconfigure hello нового подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="119fe-184">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="119fe-186">В hello **SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="119fe-186">In hello **SAML** section.</span></span> <span data-ttu-id="119fe-187">Выберите **Azure Active Directory (Azure AD)** из hello **добавить поставщик удостоверений** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="119fe-187">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="119fe-189">Выберите уровень подписки **Базовый**.</span><span class="sxs-lookup"><span data-stu-id="119fe-189">Select subscription level as **Basic**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="119fe-191">На hello **свойства приложения** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="119fe-191">On hello **App properties** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="119fe-193">а.</span><span class="sxs-lookup"><span data-stu-id="119fe-193">a.</span></span> <span data-ttu-id="119fe-194">Копировать hello **URI идентификатора приложения** и использовать его как **идентификатор, URL-адрес ответа и URL-адрес входа** на hello **Kantega единого входа для домена Bamboo и URL-адреса** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="119fe-194">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="119fe-195">b.</span><span class="sxs-lookup"><span data-stu-id="119fe-195">b.</span></span> <span data-ttu-id="119fe-196">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="119fe-196">Click **Next**.</span></span>

17. <span data-ttu-id="119fe-197">На hello **импорта метаданных** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="119fe-197">On hello **Metadata import** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="119fe-199">а.</span><span class="sxs-lookup"><span data-stu-id="119fe-199">a.</span></span> <span data-ttu-id="119fe-200">Щелкните **Metadata file on my computer** (Файл метаданных на моем компьютере) и передайте файл метаданных, который вы скачали с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="119fe-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="119fe-201">b.</span><span class="sxs-lookup"><span data-stu-id="119fe-201">b.</span></span> <span data-ttu-id="119fe-202">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="119fe-202">Click **Next**.</span></span>

18. <span data-ttu-id="119fe-203">На hello **расположение единого входа и имя** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="119fe-203">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="119fe-205">а.</span><span class="sxs-lookup"><span data-stu-id="119fe-205">a.</span></span> <span data-ttu-id="119fe-206">Добавьте имя hello поставщика удостоверений в **имя поставщика удостоверений** текстового поля (например, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="119fe-206">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="119fe-207">b.</span><span class="sxs-lookup"><span data-stu-id="119fe-207">b.</span></span> <span data-ttu-id="119fe-208">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="119fe-208">Click **Next**.</span></span>

19. <span data-ttu-id="119fe-209">Проверьте сертификат подписи hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="119fe-209">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="119fe-211">На hello **учетные записи пользователей Bamboo** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="119fe-211">On hello **Bamboo user accounts** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="119fe-213">а.</span><span class="sxs-lookup"><span data-stu-id="119fe-213">a.</span></span> <span data-ttu-id="119fe-214">Выберите **при необходимости создайте пользователей в каталоге внутренней Bamboo** и введите соответствующее имя hello hello группы для пользователей (может быть несколько нет.</span><span class="sxs-lookup"><span data-stu-id="119fe-214">Select **Create users in Bamboo's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="119fe-215">разделенных запятой).</span><span class="sxs-lookup"><span data-stu-id="119fe-215">of groups separated by comma).</span></span>

    <span data-ttu-id="119fe-216">b.</span><span class="sxs-lookup"><span data-stu-id="119fe-216">b.</span></span> <span data-ttu-id="119fe-217">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="119fe-217">Click **Next**.</span></span>

21. <span data-ttu-id="119fe-218">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="119fe-218">Click **Finish**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="119fe-220">На hello **известные доменов для Azure AD** статьи, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="119fe-220">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="119fe-222">а.</span><span class="sxs-lookup"><span data-stu-id="119fe-222">a.</span></span> <span data-ttu-id="119fe-223">Выберите **известные домены** из hello левой панели страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="119fe-223">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="119fe-224">b.</span><span class="sxs-lookup"><span data-stu-id="119fe-224">b.</span></span> <span data-ttu-id="119fe-225">Введите имя домена в hello **известные домены** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="119fe-225">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="119fe-226">c.</span><span class="sxs-lookup"><span data-stu-id="119fe-226">c.</span></span> <span data-ttu-id="119fe-227">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="119fe-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="119fe-228">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="119fe-228">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="119fe-229">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="119fe-229">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="119fe-230">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="119fe-230">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="119fe-231">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="119fe-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="119fe-232">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="119fe-232">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="119fe-234">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="119fe-234">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="119fe-235">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="119fe-235">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="119fe-237">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="119fe-237">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="119fe-239">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="119fe-239">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="119fe-241">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="119fe-241">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="119fe-243">а.</span><span class="sxs-lookup"><span data-stu-id="119fe-243">a.</span></span> <span data-ttu-id="119fe-244">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="119fe-244">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="119fe-245">b.</span><span class="sxs-lookup"><span data-stu-id="119fe-245">b.</span></span> <span data-ttu-id="119fe-246">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="119fe-246">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="119fe-247">c.</span><span class="sxs-lookup"><span data-stu-id="119fe-247">c.</span></span> <span data-ttu-id="119fe-248">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="119fe-248">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="119fe-249">d.</span><span class="sxs-lookup"><span data-stu-id="119fe-249">d.</span></span> <span data-ttu-id="119fe-250">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="119fe-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="119fe-251">Создание тестового пользователя Kantega SSO for Bamboo</span><span class="sxs-lookup"><span data-stu-id="119fe-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="119fe-252">Пользователи toolog tooenable Azure AD в tooBamboo, их необходимо подготовить в Bamboo.</span><span class="sxs-lookup"><span data-stu-id="119fe-252">tooenable Azure AD users toolog in tooBamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="119fe-253">В Kantega SSO for Bamboo подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="119fe-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="119fe-254">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="119fe-254">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="119fe-255">Войдите в tooyour Bamboo на локальном сервере от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="119fe-255">Log in tooyour Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="119fe-256">Наведите указатель мыши на шестеренки и выберите hello **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="119fe-256">Hover on cog and click hello **User management**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="119fe-258">Выберите раздел **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="119fe-258">Click **Users**.</span></span> <span data-ttu-id="119fe-259">В разделе hello **добавить пользователя** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="119fe-259">Under hello **Add user** section, Perform follwing steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="119fe-261">а.</span><span class="sxs-lookup"><span data-stu-id="119fe-261">a.</span></span> <span data-ttu-id="119fe-262">В hello **Username** электронной почты hello тип пользователя в текстовое поле, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="119fe-262">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="119fe-263">b.</span><span class="sxs-lookup"><span data-stu-id="119fe-263">b.</span></span> <span data-ttu-id="119fe-264">В hello **пароль** текстового поля, типа hello пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="119fe-264">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="119fe-265">c.</span><span class="sxs-lookup"><span data-stu-id="119fe-265">c.</span></span> <span data-ttu-id="119fe-266">В hello **подтверждение пароля** текстовом поле введите hello пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="119fe-266">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>
    
    <span data-ttu-id="119fe-267">d.</span><span class="sxs-lookup"><span data-stu-id="119fe-267">d.</span></span> <span data-ttu-id="119fe-268">В hello **полное имя** текстовое поле, полное имя типа пользователя hello как Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="119fe-268">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="119fe-269">д.</span><span class="sxs-lookup"><span data-stu-id="119fe-269">e.</span></span> <span data-ttu-id="119fe-270">В hello **электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="119fe-270">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="119fe-271">f.</span><span class="sxs-lookup"><span data-stu-id="119fe-271">f.</span></span> <span data-ttu-id="119fe-272">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="119fe-272">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="119fe-273">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="119fe-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="119fe-274">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooKantega единого входа для Bamboo.</span><span class="sxs-lookup"><span data-stu-id="119fe-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bamboo.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="119fe-276">**tooassign tooKantega Britta Simon единого входа для Bamboo, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="119fe-276">**tooassign Britta Simon tooKantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="119fe-277">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="119fe-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="119fe-279">В списке приложений hello выберите **Kantega единого входа для Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="119fe-279">In hello applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="119fe-281">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="119fe-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="119fe-283">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="119fe-283">Click **Add** button.</span></span> <span data-ttu-id="119fe-284">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="119fe-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="119fe-286">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="119fe-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="119fe-287">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="119fe-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="119fe-288">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="119fe-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="119fe-289">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="119fe-289">Testing single sign-on</span></span>

<span data-ttu-id="119fe-290">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="119fe-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="119fe-291">При нажатии кнопки hello Kantega единого входа для Bamboo плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Kantega единого входа для приложения Bamboo.</span><span class="sxs-lookup"><span data-stu-id="119fe-291">When you click hello Kantega SSO for Bamboo tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="119fe-292">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="119fe-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="119fe-293">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="119fe-293">Additional resources</span></span>

* [<span data-ttu-id="119fe-294">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="119fe-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="119fe-295">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="119fe-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

