---
title: "Руководство по интеграции Azure Active Directory с NetDocuments | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="dd5c6-103">Учебник. Интеграция Azure Active Directory с NetDocuments</span><span class="sxs-lookup"><span data-stu-id="dd5c6-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="dd5c6-104">В этом учебнике вы узнаете, как toointegrate NetDocuments с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd5c6-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd5c6-105">Интеграция NetDocuments с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="dd5c6-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dd5c6-106">Можно управлять в Azure AD, имеющего доступ tooNetDocuments</span><span class="sxs-lookup"><span data-stu-id="dd5c6-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="dd5c6-107">Можно включить на пользователей tooautomatically get вошедшего tooNetDocuments (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd5c6-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd5c6-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="dd5c6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dd5c6-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd5c6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd5c6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dd5c6-110">Prerequisites</span></span>

<span data-ttu-id="dd5c6-111">tooconfigure интеграция Azure AD с NetDocuments требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="dd5c6-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="dd5c6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dd5c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd5c6-113">подписка NetDocuments с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd5c6-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd5c6-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="dd5c6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd5c6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd5c6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd5c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd5c6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dd5c6-118">Scenario description</span></span>
<span data-ttu-id="dd5c6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd5c6-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="dd5c6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd5c6-121">Добавление NetDocuments из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dd5c6-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="dd5c6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd5c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="dd5c6-123">Добавление NetDocuments из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dd5c6-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="dd5c6-124">tooconfigure hello интеграции NetDocuments в Azure AD, вы должны tooadd NetDocuments из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dd5c6-125">**tooadd NetDocuments из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dd5c6-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd5c6-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd5c6-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dd5c6-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dd5c6-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dd5c6-133">Введите в поле поиска hello **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-133">In hello search box, type **NetDocuments**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="dd5c6-135">В панели результатов hello выберите **NetDocuments**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd5c6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd5c6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd5c6-138">В этом разделе описаны настройка и проверка единого входа Azure AD в NetDocuments с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd5c6-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в NetDocuments является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="dd5c6-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в NetDocuments должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="dd5c6-141">В NetDocuments, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dd5c6-142">tooconfigure и теста Azure AD единого входа с NetDocuments, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="dd5c6-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dd5c6-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dd5c6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd5c6-145">**[Создание тестового пользователя NetDocuments](#creating-a-netdocuments-test-user)**  -toohave аналог Саймон Britta в NetDocuments, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd5c6-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd5c6-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd5c6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd5c6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd5c6-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="dd5c6-150">**tooconfigure Azure AD единого входа с NetDocuments, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dd5c6-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd5c6-151">В hello в hello портала Azure **NetDocuments** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dd5c6-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="dd5c6-155">На hello **URL-адреса и домена NetDocuments** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dd5c6-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="dd5c6-157">а.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-157">a.</span></span> <span data-ttu-id="dd5c6-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="dd5c6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="dd5c6-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-159">b.</span></span> <span data-ttu-id="dd5c6-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="dd5c6-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd5c6-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-161">These values are not real.</span></span> <span data-ttu-id="dd5c6-162">Обновите эти значения с hello фактический URL-адрес входа и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="dd5c6-163">Обратитесь к [NetDocuments поддержки](https://support.netdocuments.com/hc/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="dd5c6-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="dd5c6-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dd5c6-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd5c6-168">В другом окне веб-браузера войдите на сайт NetDocuments вашей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="dd5c6-169">Go слишком**администратора**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="dd5c6-170">Щелкните **Добавление и удаление пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="dd5c6-171">![Репозиторий](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Репозиторий")</span><span class="sxs-lookup"><span data-stu-id="dd5c6-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="dd5c6-172">Щелкните **Настройка дополнительных параметров аутентификации**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="dd5c6-173">![Настройка дополнительных параметров аутентификации](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Настройка дополнительных параметров аутентификации")</span><span class="sxs-lookup"><span data-stu-id="dd5c6-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="dd5c6-174">На hello **федеративное удостоверение** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dd5c6-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd5c6-175">![Федеративное удостоверение](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Федеративное удостоверение")</span><span class="sxs-lookup"><span data-stu-id="dd5c6-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="dd5c6-176">а.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-176">a.</span></span> <span data-ttu-id="dd5c6-177">Для параметра **Federated identity server type** (Тип сервера федеративных удостоверений) выберите **Службы федерации Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="dd5c6-178">b.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-178">b.</span></span> <span data-ttu-id="dd5c6-179">Нажмите кнопку **выбрать файл**, tooupload hello скачать файл метаданных, который вы скачали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="dd5c6-180">c.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-180">c.</span></span> <span data-ttu-id="dd5c6-181">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="dd5c6-182">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="dd5c6-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dd5c6-183">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dd5c6-184">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd5c6-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd5c6-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd5c6-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd5c6-186">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dd5c6-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dd5c6-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd5c6-189">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd5c6-191">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd5c6-193">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="dd5c6-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd5c6-195">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dd5c6-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd5c6-197">а.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-197">a.</span></span> <span data-ttu-id="dd5c6-198">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd5c6-199">b.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-199">b.</span></span> <span data-ttu-id="dd5c6-200">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd5c6-201">c.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-201">c.</span></span> <span data-ttu-id="dd5c6-202">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dd5c6-203">d.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-203">d.</span></span> <span data-ttu-id="dd5c6-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="dd5c6-205">Создание тестового пользователя NetDocuments</span><span class="sxs-lookup"><span data-stu-id="dd5c6-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="dd5c6-206">Пользователи toolog tooenable Azure AD в tooNetDocuments, их необходимо подготовить в NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="dd5c6-207">В случае hello NetDocuments Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="dd5c6-208">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dd5c6-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd5c6-209">Максимум на tooyour **NetDocuments** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="dd5c6-210">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="dd5c6-211">![Администратор](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="dd5c6-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="dd5c6-212">Щелкните **Добавление и удаление пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="dd5c6-213">![Репозиторий](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Репозиторий")</span><span class="sxs-lookup"><span data-stu-id="dd5c6-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="dd5c6-214">В hello **адрес электронной почты** в текстовое поле введите адрес электронной почты hello действительной учетной записи Azure Active Directory tooprovision и нажмите кнопку **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="dd5c6-215">![Адрес электронной почты](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Адрес электронной почты")</span><span class="sxs-lookup"><span data-stu-id="dd5c6-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="dd5c6-216">Владелец учетной записи Hello Azure Active Directory получит сообщение электронной почты, который включает учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="dd5c6-217">Можно использовать любые другие NetDocuments пользователя средства создания учетных записей или интерфейсы API, предоставляемые NetDocuments tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dd5c6-218">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="dd5c6-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dd5c6-219">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNetDocuments доступа.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dd5c6-221">**tooassign tooNetDocuments Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dd5c6-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd5c6-222">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dd5c6-224">В списке приложений hello выберите **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="dd5c6-226">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dd5c6-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-228">Click **Add** button.</span></span> <span data-ttu-id="dd5c6-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dd5c6-231">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dd5c6-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd5c6-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd5c6-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dd5c6-234">Testing single sign-on</span></span>

<span data-ttu-id="dd5c6-235">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dd5c6-236">При нажатии кнопки NetDocuments плитки в панели доступа hello приветствия, вы должны получить tooyour автоматически подписан в приложение NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="dd5c6-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="dd5c6-237">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd5c6-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd5c6-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dd5c6-238">Additional resources</span></span>

* [<span data-ttu-id="dd5c6-239">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd5c6-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd5c6-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dd5c6-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

