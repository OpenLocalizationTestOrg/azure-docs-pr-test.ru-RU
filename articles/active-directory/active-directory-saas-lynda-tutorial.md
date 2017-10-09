---
title: "Учебник. Интеграция Azure Active Directory с Lynda.com | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="f1dd6-103">Руководство. Интеграция Azure Active Directory с Lynda.com</span><span class="sxs-lookup"><span data-stu-id="f1dd6-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="f1dd6-104">В этом учебнике вы узнаете, как toointegrate Lynda.com с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1dd6-104">In this tutorial, you learn how toointegrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1dd6-105">Интеграция Lynda.com с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f1dd6-105">Integrating Lynda.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1dd6-106">Можно управлять в Azure AD, имеющего доступ tooLynda.com</span><span class="sxs-lookup"><span data-stu-id="f1dd6-106">You can control in Azure AD who has access tooLynda.com</span></span>
- <span data-ttu-id="f1dd6-107">Можно включить на пользователей tooautomatically get вошедшего tooLynda.com (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1dd6-107">You can enable your users tooautomatically get signed-on tooLynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1dd6-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f1dd6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1dd6-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1dd6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1dd6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f1dd6-110">Prerequisites</span></span>

<span data-ttu-id="f1dd6-111">tooconfigure интеграция Azure AD с Lynda.com требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f1dd6-111">tooconfigure Azure AD integration with Lynda.com, you need hello following items:</span></span>

- <span data-ttu-id="f1dd6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f1dd6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1dd6-113">подписка Lynda.com с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1dd6-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1dd6-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f1dd6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1dd6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1dd6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1dd6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1dd6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f1dd6-118">Scenario description</span></span>
<span data-ttu-id="f1dd6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1dd6-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f1dd6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1dd6-121">Добавление Lynda.com из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f1dd6-121">Adding Lynda.com from hello gallery</span></span>
2. <span data-ttu-id="f1dd6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1dd6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-hello-gallery"></a><span data-ttu-id="f1dd6-123">Добавление Lynda.com из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f1dd6-123">Adding Lynda.com from hello gallery</span></span>
<span data-ttu-id="f1dd6-124">tooconfigure hello интеграции Lynda.com в Azure AD, вы должны tooadd Lynda.com из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-124">tooconfigure hello integration of Lynda.com into Azure AD, you need tooadd Lynda.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1dd6-125">**tooadd Lynda.com из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1dd6-125">**tooadd Lynda.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1dd6-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1dd6-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1dd6-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f1dd6-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f1dd6-133">Введите в поле поиска hello **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-133">In hello search box, type **Lynda.com**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="f1dd6-135">В панели результатов hello выберите **Lynda.com**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-135">In hello results panel, select **Lynda.com**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1dd6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1dd6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1dd6-138">В этом разделе описана настройка и проверка единого входа Azure AD в Lynda.com для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1dd6-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Lynda.com является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lynda.com is tooa user in Azure AD.</span></span> <span data-ttu-id="f1dd6-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Lynda.com должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-140">In other words, a link relationship between an Azure AD user and hello related user in Lynda.com needs toobe established.</span></span>

<span data-ttu-id="f1dd6-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lynda.com.</span></span>

<span data-ttu-id="f1dd6-142">tooconfigure и теста Azure AD единого входа с Lynda.com, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f1dd6-142">tooconfigure and test Azure AD single sign-on with Lynda.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1dd6-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1dd6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1dd6-145">**[Создание тестового пользователя Lynda.com](#creating-a-lyndacom-test-user)**  -toohave аналог Саймон Britta в Lynda.com, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - toohave a counterpart of Britta Simon in Lynda.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1dd6-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1dd6-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1dd6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1dd6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1dd6-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Lynda.com приложения.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="f1dd6-150">**Azure AD tooconfigure единого входа с Lynda.com, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1dd6-150">**tooconfigure Azure AD single sign-on with Lynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1dd6-151">В hello в hello портала Azure **Lynda.com** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-151">In hello Azure portal, on hello **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f1dd6-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="f1dd6-155">На hello **URL-адреса и домена Lynda.com** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f1dd6-155">On hello **Lynda.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="f1dd6-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="f1dd6-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1dd6-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-158">This value is not real.</span></span> <span data-ttu-id="f1dd6-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f1dd6-160">Обратитесь к [группа поддержки Lynda.com клиента](https://www.linkedin.com/help/lynda/ask) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) tooget these values.</span></span> 
 
4. <span data-ttu-id="f1dd6-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="f1dd6-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f1dd6-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1dd6-165">tooconfigure единого входа на **Lynda.com** стороны, необходимо загрузить hello toosend **метаданные в формате XML** [поддержки Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="f1dd6-165">tooconfigure single sign-on on **Lynda.com** side, you need toosend hello downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1dd6-166">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1dd6-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1dd6-167">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f1dd6-169">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1dd6-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1dd6-170">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1dd6-172">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1dd6-174">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f1dd6-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1dd6-176">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f1dd6-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1dd6-178">а.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-178">a.</span></span> <span data-ttu-id="f1dd6-179">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1dd6-180">b.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-180">b.</span></span> <span data-ttu-id="f1dd6-181">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1dd6-182">c.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-182">c.</span></span> <span data-ttu-id="f1dd6-183">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1dd6-184">d.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-184">d.</span></span> <span data-ttu-id="f1dd6-185">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="f1dd6-186">Создание тестового пользователя Lynda.com</span><span class="sxs-lookup"><span data-stu-id="f1dd6-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="f1dd6-187">Нет элемента действия для вас tooconfigure подготовки пользователей tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-187">There is no action item for you tooconfigure user provisioning tooLynda.com.</span></span>  
<span data-ttu-id="f1dd6-188">Когда назначенный пользователь пытается toolog в tooLynda.com, с помощью панели доступа hello, Lynda.com проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-188">When an assigned user tries toolog in tooLynda.com using hello access panel, Lynda.com checks whether hello user exists.</span></span>  

<span data-ttu-id="f1dd6-189">Если учетная запись пользователя отсутствует, Lynda.com автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="f1dd6-190">Можно использовать любые другие Lynda.com пользователя средства создания учетных записей или интерфейсы API, предоставляемые Lynda.com tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1dd6-191">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f1dd6-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1dd6-192">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLynda.com доступа.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLynda.com.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f1dd6-194">**tooassign tooLynda.com Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1dd6-194">**tooassign Britta Simon tooLynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1dd6-195">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f1dd6-197">В списке приложений hello выберите **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-197">In hello applications list, select **Lynda.com**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="f1dd6-199">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f1dd6-201">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-201">Click **Add** button.</span></span> <span data-ttu-id="f1dd6-202">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f1dd6-204">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1dd6-205">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1dd6-206">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1dd6-207">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f1dd6-207">Testing single sign-on</span></span>

<span data-ttu-id="f1dd6-208">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="f1dd6-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f1dd6-209">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f1dd6-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f1dd6-210">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f1dd6-210">Additional resources</span></span>

* [<span data-ttu-id="f1dd6-211">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1dd6-211">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1dd6-212">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1dd6-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

