---
title: "Руководство. Интеграция Azure Active Directory с Box | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e13a7979761a0b30ecdaac242f1f57a7f8da54c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="b7027-103">Руководство. Интеграция Azure Active Directory с Box</span><span class="sxs-lookup"><span data-stu-id="b7027-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="b7027-104">В этом учебнике вы узнаете, как toointegrate поле с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7027-104">In this tutorial, you learn how toointegrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7027-105">Интеграция поле с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b7027-105">Integrating Box with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b7027-106">Можно управлять в Azure AD, имеющего доступ панель инструментов</span><span class="sxs-lookup"><span data-stu-id="b7027-106">You can control in Azure AD who has access tooBox</span></span>
- <span data-ttu-id="b7027-107">Можно включить на пользователей tooautomatically get подписан на панель инструментов (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7027-107">You can enable your users tooautomatically get signed-on tooBox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b7027-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b7027-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b7027-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7027-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7027-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b7027-110">Prerequisites</span></span>

<span data-ttu-id="b7027-111">tooconfigure интеграция Azure AD, в котором требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b7027-111">tooconfigure Azure AD integration with Box, you need hello following items:</span></span>

- <span data-ttu-id="b7027-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b7027-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7027-113">подписка Box с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b7027-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7027-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b7027-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7027-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b7027-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7027-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b7027-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7027-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7027-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7027-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b7027-118">Scenario description</span></span>
<span data-ttu-id="b7027-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b7027-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7027-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b7027-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7027-121">Добавление поля из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="b7027-121">Adding Box from hello gallery</span></span>
2. <span data-ttu-id="b7027-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7027-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-hello-gallery"></a><span data-ttu-id="b7027-123">Добавление поля из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="b7027-123">Adding Box from hello gallery</span></span>
<span data-ttu-id="b7027-124">tooconfigure hello интеграции поле в Azure AD, вы должны tooadd поле из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b7027-124">tooconfigure hello integration of Box into Azure AD, you need tooadd Box from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b7027-125">**tooadd поле из коллекции hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7027-125">**tooadd Box from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7027-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b7027-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b7027-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b7027-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b7027-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b7027-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b7027-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b7027-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b7027-133">Введите в поле поиска hello **поле**.</span><span class="sxs-lookup"><span data-stu-id="b7027-133">In hello search box, type **Box**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="b7027-135">В панели результатов hello выберите **поле**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b7027-135">In hello results panel, select **Box**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b7027-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7027-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b7027-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Box с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7027-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b7027-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в поле является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7027-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Box is tooa user in Azure AD.</span></span> <span data-ttu-id="b7027-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в поле должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b7027-140">In other words, a link relationship between an Azure AD user and hello related user in Box needs toobe established.</span></span>

<span data-ttu-id="b7027-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в поле.</span><span class="sxs-lookup"><span data-stu-id="b7027-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Box.</span></span>

<span data-ttu-id="b7027-142">tooconfigure и тестирования Azure AD единого входа с полем, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b7027-142">tooconfigure and test Azure AD single sign-on with Box, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b7027-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b7027-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b7027-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b7027-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7027-145">**[Создание тестового пользователя поле](#creating-a-box-test-user)**  -toohave аналог Саймон Britta в поле, которое представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b7027-145">**[Creating a Box test user](#creating-a-box-test-user)** - toohave a counterpart of Britta Simon in Box that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7027-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b7027-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7027-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b7027-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b7027-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7027-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b7027-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении поле.</span><span class="sxs-lookup"><span data-stu-id="b7027-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="b7027-150">**tooconfigure Azure AD единого входа с полем, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7027-150">**tooconfigure Azure AD single sign-on with Box, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7027-151">В hello в hello портала Azure **поле** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b7027-151">In hello Azure portal, on hello **Box** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b7027-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b7027-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="b7027-155">На hello **URL-адреса и домена поле** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b7027-155">On hello **Box Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="b7027-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="b7027-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b7027-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="b7027-158">This value is not real.</span></span> <span data-ttu-id="b7027-159">Обновите значение hello с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="b7027-159">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="b7027-160">Обратитесь к [группа поддержки клиента поле](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="b7027-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget this value.</span></span> 
 
4. <span data-ttu-id="b7027-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b7027-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="b7027-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b7027-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b7027-165">tooget единого входа, настроенному для вашего приложения, обратитесь к [группа поддержки клиента поле](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) и предоставить им hello загрузить XML-файл.</span><span class="sxs-lookup"><span data-stu-id="b7027-165">tooget SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with hello downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="b7027-166">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b7027-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b7027-167">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b7027-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b7027-168">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b7027-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b7027-169">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7027-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="b7027-170">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b7027-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b7027-172">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7027-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7027-173">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b7027-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b7027-175">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b7027-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b7027-177">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b7027-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7027-179">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b7027-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b7027-181">а.</span><span class="sxs-lookup"><span data-stu-id="b7027-181">a.</span></span> <span data-ttu-id="b7027-182">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7027-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7027-183">b.</span><span class="sxs-lookup"><span data-stu-id="b7027-183">b.</span></span> <span data-ttu-id="b7027-184">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b7027-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b7027-185">c.</span><span class="sxs-lookup"><span data-stu-id="b7027-185">c.</span></span> <span data-ttu-id="b7027-186">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b7027-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b7027-187">d.</span><span class="sxs-lookup"><span data-stu-id="b7027-187">d.</span></span> <span data-ttu-id="b7027-188">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b7027-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="b7027-189">Создание тестового пользователя Box</span><span class="sxs-lookup"><span data-stu-id="b7027-189">Creating a Box test user</span></span>

<span data-ttu-id="b7027-190">В этом разделе вы создадите в Box пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7027-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="b7027-191">Приложение Box поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b7027-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="b7027-192">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="b7027-192">There is no action item for you in this section.</span></span> <span data-ttu-id="b7027-193">Если пользователь еще не существует в поле, новый создается при попытке tooaccess поле.</span><span class="sxs-lookup"><span data-stu-id="b7027-193">If a user doesn't already exist in Box, a new one is created when you attempt tooaccess Box.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b7027-194">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b7027-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b7027-195">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа панель инструментов.</span><span class="sxs-lookup"><span data-stu-id="b7027-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBox.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b7027-197">**tooassign Britta Simon панель инструментов, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7027-197">**tooassign Britta Simon tooBox, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7027-198">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b7027-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b7027-200">В списке приложений hello выберите **поле**.</span><span class="sxs-lookup"><span data-stu-id="b7027-200">In hello applications list, select **Box**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="b7027-202">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b7027-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b7027-204">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b7027-204">Click **Add** button.</span></span> <span data-ttu-id="b7027-205">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b7027-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b7027-207">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b7027-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b7027-208">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b7027-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7027-209">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b7027-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b7027-210">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b7027-210">Testing single sign-on</span></span>

<span data-ttu-id="b7027-211">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b7027-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b7027-212">Если щелкнуть плитку поле hello в hello панели доступа, вы должны получить входа страницы tooget вошедшего tooyour Box application.</span><span class="sxs-lookup"><span data-stu-id="b7027-212">When you click hello Box tile in hello Access Panel, you should get login page tooget signed-on tooyour Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7027-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b7027-213">Additional resources</span></span>

* [<span data-ttu-id="b7027-214">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7027-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7027-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7027-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b7027-216">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="b7027-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

