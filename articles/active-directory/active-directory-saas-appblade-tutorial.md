---
title: "Руководство. Интеграция Azure Active Directory с AppBlade | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="52466-103">Руководство. Интеграция Azure Active Directory с AppBlade</span><span class="sxs-lookup"><span data-stu-id="52466-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="52466-104">В этом учебнике вы узнаете, как toointegrate AppBlade с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52466-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52466-105">Интеграция с Azure AD AppBlade предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="52466-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="52466-106">Можно управлять в Azure AD, имеющего доступ tooAppBlade</span><span class="sxs-lookup"><span data-stu-id="52466-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="52466-107">Можно включить на пользователей tooautomatically get вошедшего tooAppBlade (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="52466-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52466-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="52466-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="52466-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52466-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52466-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="52466-110">Prerequisites</span></span>

<span data-ttu-id="52466-111">tooconfigure интеграция Azure AD с AppBlade требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="52466-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="52466-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="52466-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52466-113">подписка AppBlade с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="52466-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52466-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="52466-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52466-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="52466-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52466-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="52466-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52466-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52466-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52466-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="52466-118">Scenario description</span></span>
<span data-ttu-id="52466-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="52466-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52466-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="52466-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52466-121">Добавление AppBlade из галереи hello</span><span class="sxs-lookup"><span data-stu-id="52466-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="52466-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52466-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="52466-123">Добавление AppBlade из галереи hello</span><span class="sxs-lookup"><span data-stu-id="52466-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="52466-124">tooconfigure hello интеграции AppBlade в Azure AD, вы должны tooadd AppBlade из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="52466-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="52466-125">**tooadd AppBlade из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="52466-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="52466-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="52466-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52466-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="52466-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="52466-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="52466-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="52466-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="52466-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="52466-133">Введите в поле поиска hello **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="52466-133">In hello search box, type **AppBlade**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="52466-135">В панели результатов hello выберите **AppBlade**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="52466-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52466-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52466-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52466-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение AppBlade с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52466-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="52466-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в AppBlade является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52466-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="52466-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в AppBlade должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="52466-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="52466-141">В AppBlade, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="52466-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="52466-142">tooconfigure и теста Azure AD единого входа с AppBlade, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="52466-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="52466-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="52466-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="52466-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="52466-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52466-145">**[Создание тестового пользователя, прошедшего AppBlade](#creating-an-appblade-test-user)**  -toohave аналог Саймон Britta в AppBlade, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="52466-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="52466-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="52466-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52466-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="52466-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52466-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52466-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52466-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении AppBlade.</span><span class="sxs-lookup"><span data-stu-id="52466-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="52466-150">**tooconfigure Azure AD единого входа с AppBlade, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="52466-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="52466-151">В hello в hello портала Azure **AppBlade** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="52466-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="52466-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="52466-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="52466-155">На hello **URL-адреса и домена AppBlade** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="52466-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="52466-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="52466-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52466-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="52466-158">This value is not real.</span></span> <span data-ttu-id="52466-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="52466-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="52466-160">Обратитесь к [группа поддержки клиента AppBlade](mailto:support@appblade.com) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="52466-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="52466-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="52466-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="52466-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="52466-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52466-165">tooconfigure единого входа на **AppBlade** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[AppBlade поддержки](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="52466-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="52466-166">Кроме того, попросите их tooconfigure hello **URL-адрес издателя единого входа** как `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="52466-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="52466-167">Этот параметр является обязательным для toowork.</span><span class="sxs-lookup"><span data-stu-id="52466-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="52466-168">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="52466-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="52466-169">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="52466-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="52466-170">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52466-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52466-171">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="52466-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="52466-172">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="52466-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="52466-174">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="52466-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="52466-175">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="52466-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52466-177">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="52466-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52466-179">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="52466-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52466-181">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="52466-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52466-183">а.</span><span class="sxs-lookup"><span data-stu-id="52466-183">a.</span></span> <span data-ttu-id="52466-184">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52466-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52466-185">b.</span><span class="sxs-lookup"><span data-stu-id="52466-185">b.</span></span> <span data-ttu-id="52466-186">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52466-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52466-187">c.</span><span class="sxs-lookup"><span data-stu-id="52466-187">c.</span></span> <span data-ttu-id="52466-188">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="52466-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="52466-189">d.</span><span class="sxs-lookup"><span data-stu-id="52466-189">d.</span></span> <span data-ttu-id="52466-190">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="52466-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="52466-191">Создание тестового пользователя AppBlade</span><span class="sxs-lookup"><span data-stu-id="52466-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="52466-192">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в AppBlade.</span><span class="sxs-lookup"><span data-stu-id="52466-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="52466-193">Приложение AppBlade поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="52466-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="52466-194">**Убедитесь, что ваше доменное имя настроено в AppBlade для подготовки пользователей. После этого только hello в время подготовки пользователей работает.**</span><span class="sxs-lookup"><span data-stu-id="52466-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="52466-195">Если пользователь hello имеет адрес электронной почты, заканчивая hello домена, настроенного с AppBlade для вашей учетной записи, то hello пользователя автоматически соединит как член с уровнем разрешений hello, указываемые hello учетной записи, которая является одной из «Basic» (basic пользователя, которому можно установить только приложения), «Участник» (пользователь, который можно отправить новых версий приложения и управления проектами) или «Administrator» (учетная запись toohello права полного администратора).</span><span class="sxs-lookup"><span data-stu-id="52466-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="52466-196">Обычно один бы выбрать Basic и затем продвинуть пользователей вручную через имя входа администратора (AppBlade должен tooconfigure либо имя входа администратора на основе электронной почты заранее или повысить пользователя от имени клиента hello после входа в систему).</span><span class="sxs-lookup"><span data-stu-id="52466-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="52466-197">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="52466-197">There is no action item for you in this section.</span></span> <span data-ttu-id="52466-198">Новый пользователь создается во время попытки tooaccess AppBlade, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="52466-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="52466-199">Если требуется toocreate пользователя вручную, необходимо toocontact hello [AppBlade поддержки](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="52466-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="52466-200">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="52466-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="52466-201">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAppBlade доступа.</span><span class="sxs-lookup"><span data-stu-id="52466-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="52466-203">**tooassign tooAppBlade Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="52466-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="52466-204">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="52466-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="52466-206">В списке приложений hello выберите **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="52466-206">In hello applications list, select **AppBlade**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="52466-208">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="52466-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="52466-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="52466-210">Click **Add** button.</span></span> <span data-ttu-id="52466-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="52466-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="52466-213">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="52466-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="52466-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="52466-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52466-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="52466-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52466-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="52466-216">Testing single sign-on</span></span>

<span data-ttu-id="52466-217">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="52466-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="52466-218">При нажатии кнопки hello AppBlade плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour AppBlade приложения.</span><span class="sxs-lookup"><span data-stu-id="52466-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="52466-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="52466-219">Additional resources</span></span>

* [<span data-ttu-id="52466-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52466-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52466-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52466-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

