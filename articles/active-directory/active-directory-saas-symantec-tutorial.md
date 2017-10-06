---
title: "Руководство по интеграции Azure Active Directory с Symantec Web Security Service (WSS) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и службы безопасности Symantec Web (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="55d52-103">Руководство по интеграции Azure Active Directory с Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="55d52-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="55d52-104">В этом учебнике вы узнаете, как toointegrate вашей компании Symantec Web безопасности Service (WSS) учетной записи с вашей учетной записью Azure Active Directory (Azure AD) WSS для проверки подлинности пользователь подготовлен в hello Azure AD с использованием проверки подлинности SAML и принудительное применение пользователя или правила политик на уровне группы.</span><span class="sxs-lookup"><span data-stu-id="55d52-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="55d52-105">Интеграция службы безопасности Symantec Web (WSS) с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="55d52-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="55d52-106">Управление hello конечных пользователей и групп, используемых вашей учетной записи WSS с портала Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55d52-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="55d52-107">Разрешить hello конечным пользователям tooauthenticate сами WSS, используя свои учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55d52-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="55d52-108">Включение принудительного применения hello пользователя и группы правил уровень политики, определенных в вашей учетной записи WSS.</span><span class="sxs-lookup"><span data-stu-id="55d52-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="55d52-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55d52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55d52-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="55d52-110">Prerequisites</span></span>

<span data-ttu-id="55d52-111">tooconfigure интеграция Azure AD с Symantec Web безопасности Service (WSS) необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="55d52-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="55d52-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="55d52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55d52-113">Учетная запись Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="55d52-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="55d52-114">в этом учебнике шаги tootest hello, не рекомендуется WSS учетной записью, используются в настоящее время для производственных целей.</span><span class="sxs-lookup"><span data-stu-id="55d52-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="55d52-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="55d52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55d52-116">Без крайней необходимости не используйте для этого теста учетную запись WSS, которая используется в производственных целях.</span><span class="sxs-lookup"><span data-stu-id="55d52-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="55d52-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55d52-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55d52-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="55d52-118">Scenario description</span></span>
<span data-ttu-id="55d52-119">В этом учебнике вы настроите к Azure AD tooenable единого входа tooWSS с помощью учетных данных пользователя hello, определенных в вашей учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55d52-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="55d52-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="55d52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55d52-121">Добавление приложения hello Symantec Web безопасности Service (WSS) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="55d52-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="55d52-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="55d52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="55d52-123">Добавление службы безопасности Symantec Web (WSS) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="55d52-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="55d52-124">tooconfigure hello Интеграция безопасности службы Symantec Web (WSS) в Azure AD, вы должны tooadd Symantec Web безопасности Service (WSS) из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="55d52-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="55d52-125">**tooadd Symantec Web безопасности Service (WSS) из коллекции hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="55d52-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="55d52-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="55d52-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="55d52-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="55d52-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="55d52-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="55d52-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="55d52-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="55d52-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="55d52-133">Введите в поле поиска hello **Symantec Web безопасности Service (WSS)**выберите **Symantec Web безопасности Service (WSS)** из панели результатов щелкните **добавить** кнопку tooadd hello приложение.</span><span class="sxs-lookup"><span data-stu-id="55d52-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Symantec Web безопасности Service (WSS) в списке результатов hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="55d52-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="55d52-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="55d52-136">В этом разделе описана настройка и проверка единого входа Azure AD в Symantec Web Security Service (WSS) с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55d52-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55d52-137">Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello в Symantec Web безопасности Service (WSS) является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55d52-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="55d52-138">Иными словами связи между пользователя Azure AD и связанных пользователей hello в Symantec Web безопасности Service (WSS) необходимо установить toobe.</span><span class="sxs-lookup"><span data-stu-id="55d52-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="55d52-139">В компании Symantec Web безопасности Service (WSS), присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="55d52-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="55d52-140">tooconfigure и тестирования Azure AD единого входа с Symantec Web безопасности Service (WSS), необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="55d52-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="55d52-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="55d52-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="55d52-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="55d52-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55d52-143">**[Создание тестового пользователя Symantec Web безопасности Service (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave аналог Саймон Britta в Symantec Web безопасности Service (WSS), являющийся представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="55d52-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="55d52-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="55d52-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55d52-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="55d52-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="55d52-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="55d52-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="55d52-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении службы безопасности Symantec Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="55d52-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="55d52-148">**tooconfigure Azure AD единого входа с Symantec Web безопасности Service (WSS), выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="55d52-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="55d52-149">В hello в hello портала Azure **Symantec Web безопасности Service (WSS)** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="55d52-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="55d52-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="55d52-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="55d52-153">На hello **Symantec Web безопасности службы (WSS) домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="55d52-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Информация о домене и URL-адресах для единого входа в службе Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="55d52-155">а.</span><span class="sxs-lookup"><span data-stu-id="55d52-155">a.</span></span> <span data-ttu-id="55d52-156">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="55d52-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="55d52-157">b.</span><span class="sxs-lookup"><span data-stu-id="55d52-157">b.</span></span> <span data-ttu-id="55d52-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес hello:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="55d52-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="55d52-159">Обратитесь в службу hello [группа поддержки Symantec Web безопасности Service (WSS) клиента](https://www.symantec.com/contact-us) Если hello значений для hello **идентификатор** и **URL-адрес ответа** не работает ни в какой-либо причине.</span><span class="sxs-lookup"><span data-stu-id="55d52-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="55d52-160">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="55d52-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="55d52-162">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="55d52-162">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="55d52-164">tooconfigure единого входа на hello стороне Symantec Web безопасности Service (WSS), см. электронную документацию toohello WSS.</span><span class="sxs-lookup"><span data-stu-id="55d52-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="55d52-165">загружаются Hello **метаданные в формате XML** файла потребуется toobe импортируются в портал WSS hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="55d52-166">Обратитесь в службу hello [поддержки Symantec Web безопасности Service (WSS)](https://www.symantec.com/contact-us) Если вам нужна помощь с конфигурацией hello на портале WSS hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="55d52-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="55d52-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="55d52-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="55d52-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55d52-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="55d52-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="55d52-170">Create an Azure AD test user</span></span>

<span data-ttu-id="55d52-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="55d52-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="55d52-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="55d52-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="55d52-174">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="55d52-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="55d52-176">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="55d52-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="55d52-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="55d52-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="55d52-180">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="55d52-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="55d52-182">а.</span><span class="sxs-lookup"><span data-stu-id="55d52-182">a.</span></span> <span data-ttu-id="55d52-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55d52-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55d52-184">b.</span><span class="sxs-lookup"><span data-stu-id="55d52-184">b.</span></span> <span data-ttu-id="55d52-185">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="55d52-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="55d52-186">c.</span><span class="sxs-lookup"><span data-stu-id="55d52-186">c.</span></span> <span data-ttu-id="55d52-187">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="55d52-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="55d52-188">d.</span><span class="sxs-lookup"><span data-stu-id="55d52-188">d.</span></span> <span data-ttu-id="55d52-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="55d52-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="55d52-190">Создание тестового пользователя Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="55d52-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="55d52-191">В этом разделе описано, как создать пользователя Britta Simon в Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="55d52-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="55d52-192">Hello соответствующего конечного пользователя можно создать вручную на портале WSS hello или можно подождать hello пользователи и группы подготовки на портале WSS toohello toobe синхронизации Azure AD hello через несколько минут (~ 15 минут).</span><span class="sxs-lookup"><span data-stu-id="55d52-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="55d52-193">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="55d52-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="55d52-194">общедоступный IP-адрес Hello машины hello конечного пользователя, который будет использоваться toobrowse веб-сайтов также должны toobe подготовки портала hello Symantec Web безопасности Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="55d52-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="55d52-195">Проверьте [щелкните здесь](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget компьютере открытый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="55d52-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="55d52-196">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="55d52-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="55d52-197">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSymantec службы Web Security (WSS).</span><span class="sxs-lookup"><span data-stu-id="55d52-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="55d52-199">**tooassign tooSymantec Britta Simon Web безопасности Service (WSS) выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="55d52-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="55d52-200">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="55d52-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="55d52-202">В списке приложений hello выберите **Symantec Web безопасности Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="55d52-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![ссылка Symantec Web безопасности Service (WSS) Hello в списке приложений hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="55d52-204">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="55d52-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="55d52-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="55d52-206">Click **Add** button.</span></span> <span data-ttu-id="55d52-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="55d52-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="55d52-209">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="55d52-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="55d52-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55d52-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="55d52-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="55d52-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="55d52-212">Test single sign-on</span></span>

<span data-ttu-id="55d52-213">В этом разделе вы сможете протестировать hello единого входа функции настройки вашей toouse WSS учетной записи в Azure AD для проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="55d52-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="55d52-214">После настройки веб-браузера tooproxy трафика, tooWSS при открытии веб-браузере и повторите toobrowse tooa сайта, то вы будете перенаправлены toohello входа Azure на странице.</span><span class="sxs-lookup"><span data-stu-id="55d52-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="55d52-215">Введите учетные данные hello hello тестирования конечного пользователя, предоставленное в hello Azure AD (то есть, BrittaSimon) и связанный пароль.</span><span class="sxs-lookup"><span data-stu-id="55d52-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="55d52-216">Пройдя проверку подлинности, вы будете иметь доступ toobrowse toohello веб-сайт, выбранный.</span><span class="sxs-lookup"><span data-stu-id="55d52-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="55d52-217">Следует ли создать правила политики на tooblock стороне hello WSS BrittaSimon с просмотра tooa конкретного сайта, при попытке сайта toothat toobrowse имени пользователя BrittaSimon должен отобразиться страница блок WSS hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55d52-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="55d52-218">Additional resources</span></span>

* [<span data-ttu-id="55d52-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55d52-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55d52-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55d52-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

