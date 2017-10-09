---
title: "Учебник. Интеграция Azure Active Directory с Concur | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1012bf8c6f036306d0ca90689415d5e22e449989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="b7f83-103">Руководство. Интеграция Azure Active Directory с Concur</span><span class="sxs-lookup"><span data-stu-id="b7f83-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="b7f83-104">В этом учебнике вы узнаете, как toointegrate согласуются с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7f83-104">In this tutorial, you learn how toointegrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7f83-105">Интеграция Concur с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b7f83-105">Integrating Concur with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b7f83-106">Можно управлять в Azure AD, имеющего доступ tooConcur</span><span class="sxs-lookup"><span data-stu-id="b7f83-106">You can control in Azure AD who has access tooConcur</span></span>
- <span data-ttu-id="b7f83-107">Можно включить на пользователей tooautomatically get вошедшего tooConcur (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7f83-107">You can enable your users tooautomatically get signed-on tooConcur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b7f83-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b7f83-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b7f83-109">Если требуется tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. раздел [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7f83-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7f83-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b7f83-110">Prerequisites</span></span>

<span data-ttu-id="b7f83-111">tooconfigure интеграция Azure AD с Concur требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b7f83-111">tooconfigure Azure AD integration with Concur, you need hello following items:</span></span>

- <span data-ttu-id="b7f83-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b7f83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7f83-113">подписка с поддержкой единого входа Concur.</span><span class="sxs-lookup"><span data-stu-id="b7f83-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7f83-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b7f83-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7f83-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b7f83-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7f83-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b7f83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7f83-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7f83-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7f83-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b7f83-118">Scenario description</span></span>
<span data-ttu-id="b7f83-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b7f83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7f83-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b7f83-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7f83-121">Добавление Concur из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b7f83-121">Adding Concur from hello gallery</span></span>
2. <span data-ttu-id="b7f83-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7f83-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="b7f83-123">Конфигурация Hello подписки Concur для федеративной SSO посредством SAML представляет собой отдельную задачу, которой необходимо обратиться к [группа поддержки клиента Concur](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="b7f83-123">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 

## <a name="adding-concur-from-hello-gallery"></a><span data-ttu-id="b7f83-124">Добавление Concur из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b7f83-124">Adding Concur from hello gallery</span></span>
<span data-ttu-id="b7f83-125">tooconfigure hello интеграции Concur в Azure AD, вы должны tooadd Concur из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b7f83-125">tooconfigure hello integration of Concur into Azure AD, you need tooadd Concur from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b7f83-126">**tooadd Concur из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7f83-126">**tooadd Concur from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7f83-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b7f83-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b7f83-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b7f83-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b7f83-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b7f83-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b7f83-134">Введите в поле поиска hello **Concur**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-134">In hello search box, type **Concur**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="b7f83-136">В панели результатов hello выберите **Concur**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b7f83-136">In hello results panel, select **Concur**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b7f83-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7f83-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b7f83-139">В этом разделе описаны настройка и проверка единого входа Azure AD в Concur с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7f83-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b7f83-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Concur является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7f83-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Concur is tooa user in Azure AD.</span></span> <span data-ttu-id="b7f83-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Concur должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b7f83-141">In other words, a link relationship between an Azure AD user and hello related user in Concur needs toobe established.</span></span>

<span data-ttu-id="b7f83-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Concur.</span><span class="sxs-lookup"><span data-stu-id="b7f83-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Concur.</span></span>

<span data-ttu-id="b7f83-143">tooconfigure и теста Azure AD единого входа с Concur, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b7f83-143">tooconfigure and test Azure AD single sign-on with Concur, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b7f83-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b7f83-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b7f83-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b7f83-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7f83-146">**[Создание тестового пользователя Concur](#creating-a-concur-test-user)**  -toohave аналог Саймон Britta в Concur, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b7f83-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - toohave a counterpart of Britta Simon in Concur that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7f83-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b7f83-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7f83-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b7f83-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b7f83-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7f83-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b7f83-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Concur приложения.</span><span class="sxs-lookup"><span data-stu-id="b7f83-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="b7f83-151">**Azure AD tooconfigure единого входа с Concur, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7f83-151">**tooconfigure Azure AD single sign-on with Concur, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7f83-152">В hello в hello портала Azure **Concur** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-152">In hello Azure portal, on hello **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b7f83-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b7f83-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="b7f83-156">На hello **Concur доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b7f83-156">On hello **Concur Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="b7f83-158">а.</span><span class="sxs-lookup"><span data-stu-id="b7f83-158">a.</span></span> <span data-ttu-id="b7f83-159">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="b7f83-159">In hello **Sign on URL** textbox, type hello value using hello following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="b7f83-160">b.</span><span class="sxs-lookup"><span data-stu-id="b7f83-160">b.</span></span> <span data-ttu-id="b7f83-161">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="b7f83-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b7f83-162">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="b7f83-162">These values are not hello real.</span></span> <span data-ttu-id="b7f83-163">Обновление, эти значения с hello фактическое вход URL-адрес и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b7f83-163">Update these values with hello actual Sign on URL and Identifier.</span></span> <span data-ttu-id="b7f83-164">Обратитесь к [группа поддержки клиента Concur](https://www.concur.co.in/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b7f83-164">Contact [Concur Client support team](https://www.concur.co.in/contact) tooget these values.</span></span> 

4. <span data-ttu-id="b7f83-165">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b7f83-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="b7f83-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b7f83-167">Click **Save** button.</span></span>

    <span data-ttu-id="b7f83-168">![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="b7f83-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="b7f83-169">tooconfigure единого входа на **Concur** стороны, необходимо загрузить hello toosend **метаданные в формате XML** tooConcur поддержки.</span><span class="sxs-lookup"><span data-stu-id="b7f83-169">tooconfigure single sign-on on **Concur** side, you need toosend hello downloaded **Metadata XML** tooConcur support.</span></span> <span data-ttu-id="b7f83-170">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="b7f83-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="b7f83-171">Конфигурация Hello подписки Concur для федеративной SSO посредством SAML представляет собой отдельную задачу, которой необходимо обратиться к [группа поддержки клиента Concur](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="b7f83-171">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="b7f83-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b7f83-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b7f83-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b7f83-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b7f83-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b7f83-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b7f83-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7f83-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="b7f83-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f83-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b7f83-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7f83-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7f83-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b7f83-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b7f83-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b7f83-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b7f83-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7f83-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b7f83-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b7f83-187">а.</span><span class="sxs-lookup"><span data-stu-id="b7f83-187">a.</span></span> <span data-ttu-id="b7f83-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7f83-189">b.</span><span class="sxs-lookup"><span data-stu-id="b7f83-189">b.</span></span> <span data-ttu-id="b7f83-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b7f83-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b7f83-191">c.</span><span class="sxs-lookup"><span data-stu-id="b7f83-191">c.</span></span> <span data-ttu-id="b7f83-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b7f83-193">d.</span><span class="sxs-lookup"><span data-stu-id="b7f83-193">d.</span></span> <span data-ttu-id="b7f83-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="b7f83-195">Создание тестового пользователя Concur</span><span class="sxs-lookup"><span data-stu-id="b7f83-195">Creating a Concur test user</span></span>

<span data-ttu-id="b7f83-196">Приложение поддерживает hello непосредственно в подготовки пользователей время и после проверки подлинности пользователей автоматически создаются в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="b7f83-196">Application supports hello Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b7f83-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b7f83-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b7f83-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooConcur доступа.</span><span class="sxs-lookup"><span data-stu-id="b7f83-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConcur.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b7f83-200">**tooassign tooConcur Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7f83-200">**tooassign Britta Simon tooConcur, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7f83-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b7f83-203">В списке приложений hello выберите **Concur**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-203">In hello applications list, select **Concur**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="b7f83-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b7f83-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-207">Click **Add** button.</span></span> <span data-ttu-id="b7f83-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b7f83-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b7f83-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b7f83-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7f83-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b7f83-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b7f83-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b7f83-213">Testing single sign-on</span></span>

<span data-ttu-id="b7f83-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b7f83-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b7f83-215">При выборе плитки Concur hello в hello панели доступа, должно появиться страница входа Concur приложения.</span><span class="sxs-lookup"><span data-stu-id="b7f83-215">When you click hello Concur tile in hello Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="b7f83-216">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b7f83-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b7f83-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b7f83-217">Additional resources</span></span>

* [<span data-ttu-id="b7f83-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7f83-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7f83-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7f83-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b7f83-220">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="b7f83-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

