---
title: "Руководство по интеграции Azure Active Directory с InTime | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="e149e-103">Руководство по интеграции Azure Active Directory с InTime</span><span class="sxs-lookup"><span data-stu-id="e149e-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="e149e-104">В этом учебнике вы узнаете, как toointegrate InTime с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e149e-104">In this tutorial, you learn how toointegrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e149e-105">Интеграция с Azure AD InTime предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e149e-105">Integrating InTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e149e-106">Можно управлять в Azure AD, имеющего доступ tooInTime.</span><span class="sxs-lookup"><span data-stu-id="e149e-106">You can control in Azure AD who has access tooInTime.</span></span>
- <span data-ttu-id="e149e-107">Можно включить на пользователей tooautomatically get вошедшего tooInTime (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e149e-107">You can enable your users tooautomatically get signed-on tooInTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e149e-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e149e-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e149e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e149e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e149e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e149e-110">Prerequisites</span></span>

<span data-ttu-id="e149e-111">tooconfigure интеграция Azure AD с InTime требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="e149e-111">tooconfigure Azure AD integration with InTime, you need hello following items:</span></span>

- <span data-ttu-id="e149e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e149e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e149e-113">подписка InTime с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e149e-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e149e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e149e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e149e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="e149e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e149e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e149e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e149e-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e149e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e149e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e149e-118">Scenario description</span></span>
<span data-ttu-id="e149e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e149e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e149e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="e149e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e149e-121">Добавление InTime из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e149e-121">Adding InTime from hello gallery</span></span>
2. <span data-ttu-id="e149e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e149e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-hello-gallery"></a><span data-ttu-id="e149e-123">Добавление InTime из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e149e-123">Adding InTime from hello gallery</span></span>
<span data-ttu-id="e149e-124">tooconfigure hello интеграции InTime в Azure AD, вы должны tooadd InTime из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e149e-124">tooconfigure hello integration of InTime into Azure AD, you need tooadd InTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e149e-125">**tooadd InTime из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e149e-125">**tooadd InTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e149e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e149e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="e149e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="e149e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e149e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e149e-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="e149e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e149e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="e149e-133">Введите в поле поиска hello **InTime**выберите **InTime** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e149e-133">In hello search box, type **InTime**, select **InTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![В списке результатов hello inTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e149e-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e149e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e149e-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение InTime с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e149e-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e149e-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в InTime является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e149e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InTime is tooa user in Azure AD.</span></span> <span data-ttu-id="e149e-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в InTime должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="e149e-138">In other words, a link relationship between an Azure AD user and hello related user in InTime needs toobe established.</span></span>

<span data-ttu-id="e149e-139">В InTime, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="e149e-139">In InTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e149e-140">tooconfigure и теста Azure AD единого входа с InTime, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e149e-140">tooconfigure and test Azure AD single sign-on with InTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e149e-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="e149e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e149e-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e149e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e149e-143">**[Создание InTime тестового пользователя](#create-a-intime-test-user)**  -toohave аналог Саймон Britta в InTime, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e149e-143">**[Create a InTime test user](#create-a-intime-test-user)** - toohave a counterpart of Britta Simon in InTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e149e-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="e149e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e149e-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e149e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e149e-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="e149e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e149e-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении InTime.</span><span class="sxs-lookup"><span data-stu-id="e149e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="e149e-148">**tooconfigure Azure AD единого входа с InTime, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e149e-148">**tooconfigure Azure AD single sign-on with InTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="e149e-149">В hello в hello портала Azure **InTime** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e149e-149">In hello Azure portal, on hello **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="e149e-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="e149e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="e149e-153">На hello **InTime доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e149e-153">On hello **InTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="e149e-155">а.</span><span class="sxs-lookup"><span data-stu-id="e149e-155">a.</span></span> <span data-ttu-id="e149e-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="e149e-156">In hello **Sign-on URL** textbox, type hello URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="e149e-157">b.</span><span class="sxs-lookup"><span data-stu-id="e149e-157">b.</span></span> <span data-ttu-id="e149e-158">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="e149e-158">In hello **Identifier** textbox, type hello URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="e149e-159">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e149e-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="e149e-161">Приложение InTime ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="e149e-161">Your InTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="e149e-162">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="e149e-162">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="e149e-163">значение по умолчанию Hello **идентификатор пользователя** — **user.userprincipalname** , но InTime ожидает этот toobe, сопоставленный с адресом электронной почты пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e149e-163">hello default value of **User Identifier** is **user.userprincipalname** but InTime expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="e149e-164">Для этого можно использовать **user.mail** атрибут из списка hello, или используйте hello соответствующее значение атрибута на основе конфигурации в организации</span><span class="sxs-lookup"><span data-stu-id="e149e-164">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration</span></span> 

    ![Настройка атрибута](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="e149e-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e149e-166">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e149e-168">На hello **InTime конфигурации** щелкните **Настройка InTime** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="e149e-168">On hello **InTime Configuration** section, click **Configure InTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e149e-169">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="e149e-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="e149e-171">tooconfigure единого входа на **InTime** стороны, необходимо загрузить hello toosend **метаданные в формате XML**, **URL-адрес выхода и SAML единого входа URL-адрес службы** слишком[InTime поддержки](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="e149e-171">tooconfigure single sign-on on **InTime** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** too[InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="e149e-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="e149e-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e149e-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="e149e-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e149e-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="e149e-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e149e-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e149e-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e149e-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e149e-176">Create an Azure AD test user</span></span>

<span data-ttu-id="e149e-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e149e-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="e149e-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e149e-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e149e-180">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e149e-180">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e149e-182">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e149e-182">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e149e-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e149e-184">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e149e-186">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e149e-186">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e149e-188">а.</span><span class="sxs-lookup"><span data-stu-id="e149e-188">a.</span></span> <span data-ttu-id="e149e-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e149e-189">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e149e-190">b.</span><span class="sxs-lookup"><span data-stu-id="e149e-190">b.</span></span> <span data-ttu-id="e149e-191">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e149e-191">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e149e-192">c.</span><span class="sxs-lookup"><span data-stu-id="e149e-192">c.</span></span> <span data-ttu-id="e149e-193">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="e149e-193">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e149e-194">d.</span><span class="sxs-lookup"><span data-stu-id="e149e-194">d.</span></span> <span data-ttu-id="e149e-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e149e-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="e149e-196">Создание тестового пользователя InTime</span><span class="sxs-lookup"><span data-stu-id="e149e-196">Create a InTime test user</span></span>

<span data-ttu-id="e149e-197">В этом разделе описано, как создать пользователя Britta Simon в приложении InTime.</span><span class="sxs-lookup"><span data-stu-id="e149e-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="e149e-198">Работать с [InTime поддержки](mailto:hdollard@intimesoft.com) tooadd hello пользователей на платформе InTime hello.</span><span class="sxs-lookup"><span data-stu-id="e149e-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) tooadd hello users in hello InTime platform.</span></span> <span data-ttu-id="e149e-199">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="e149e-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e149e-200">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="e149e-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e149e-201">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooInTime доступа.</span><span class="sxs-lookup"><span data-stu-id="e149e-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInTime.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="e149e-203">**tooassign tooInTime Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e149e-203">**tooassign Britta Simon tooInTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="e149e-204">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e149e-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e149e-206">В списке приложений hello выберите **InTime**.</span><span class="sxs-lookup"><span data-stu-id="e149e-206">In hello applications list, select **InTime**.</span></span>

    ![Hello InTime ссылку в списке приложений hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="e149e-208">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e149e-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="e149e-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e149e-210">Click **Add** button.</span></span> <span data-ttu-id="e149e-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e149e-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="e149e-213">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e149e-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e149e-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e149e-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e149e-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e149e-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e149e-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e149e-216">Test single sign-on</span></span>

<span data-ttu-id="e149e-217">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="e149e-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e149e-218">При нажатии кнопки InTime плитки hello в Здравствуйте панели доступа, должно появиться страница входа hello InTime приложения.</span><span class="sxs-lookup"><span data-stu-id="e149e-218">When you click hello InTime tile in hello Access Panel, you should get hello login page of your InTime application.</span></span> <span data-ttu-id="e149e-219">Нажмите кнопку hello **входа** кнопку ряд IdPs будет отображаться на список кнопок.</span><span class="sxs-lookup"><span data-stu-id="e149e-219">Click hello **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="e149e-220">Нажмите кнопку **имя поставщика Удостоверений** предоставленные [InTime поддержки](mailto:hdollard@intimesoft.com) toologin в InTime приложение.</span><span class="sxs-lookup"><span data-stu-id="e149e-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) toologin into your InTime application.</span></span> <span data-ttu-id="e149e-221">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e149e-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e149e-222">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e149e-222">Additional resources</span></span>

* [<span data-ttu-id="e149e-223">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e149e-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e149e-224">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e149e-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

