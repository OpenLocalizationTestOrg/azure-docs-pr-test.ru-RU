---
title: "Руководство по интеграции Azure Active Directory с Evernote | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="cc948-103">Руководство по интеграции Azure Active Directory с Evernote</span><span class="sxs-lookup"><span data-stu-id="cc948-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="cc948-104">В этом учебнике вы узнаете, как toointegrate Evernote с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc948-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc948-105">Интеграция с Azure AD Evernote предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="cc948-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc948-106">Можно управлять в Azure AD, имеющего доступ tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="cc948-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="cc948-107">Можно включить на пользователей tooautomatically get вошедшего tooEvernote (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc948-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cc948-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cc948-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="cc948-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc948-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc948-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cc948-110">Prerequisites</span></span>

<span data-ttu-id="cc948-111">tooconfigure интеграция Azure AD с Evernote требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="cc948-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="cc948-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="cc948-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc948-113">подписка с поддержкой единого входа Evernote.</span><span class="sxs-lookup"><span data-stu-id="cc948-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc948-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="cc948-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc948-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="cc948-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc948-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="cc948-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc948-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc948-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc948-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="cc948-118">Scenario description</span></span>
<span data-ttu-id="cc948-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="cc948-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc948-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="cc948-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc948-121">Добавление Evernote из галереи hello</span><span class="sxs-lookup"><span data-stu-id="cc948-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="cc948-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc948-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="cc948-123">Добавление Evernote из галереи hello</span><span class="sxs-lookup"><span data-stu-id="cc948-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="cc948-124">tooconfigure hello интеграции Evernote в Azure AD, вы должны tooadd Evernote из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="cc948-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc948-125">**tooadd Evernote из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cc948-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc948-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="cc948-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="cc948-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="cc948-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc948-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cc948-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="cc948-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="cc948-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="cc948-133">Введите в поле поиска hello **Evernote**выберите **Evernote** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cc948-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evernote в списке результатов hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cc948-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc948-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cc948-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Evernote с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc948-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc948-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Evernote является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc948-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="cc948-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Evernote должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="cc948-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="cc948-139">В Evernote, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="cc948-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cc948-140">tooconfigure и теста Azure AD единого входа с Evernote, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="cc948-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc948-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="cc948-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc948-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="cc948-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc948-143">**[Создание тестового пользователя, прошедшего Evernote](#create-an-evernote-test-user)**  -toohave аналог Саймон Britta в Evernote, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc948-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc948-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="cc948-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc948-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cc948-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cc948-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc948-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cc948-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Evernote.</span><span class="sxs-lookup"><span data-stu-id="cc948-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="cc948-148">**tooconfigure Azure AD единого входа с Evernote, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cc948-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc948-149">В hello в hello портала Azure **Evernote** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="cc948-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="cc948-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="cc948-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="cc948-153">На hello **URL-адреса и домена Evernote** выполните следующие шаги при необходимости приложение hello tooconfigure в IDP инициировал режим hello:</span><span class="sxs-lookup"><span data-stu-id="cc948-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="cc948-155">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="cc948-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="cc948-156">Проверьте **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг при желании tooconfigure приложения hello в hello **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="cc948-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="cc948-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="cc948-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="cc948-159">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="cc948-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="cc948-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="cc948-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="cc948-163">На hello **конфигурации Evernote** щелкните **Настройка Evernote** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="cc948-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc948-164">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="cc948-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="cc948-166">В другом окне веб-браузера войдите на сайт компании Evernote в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="cc948-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="cc948-167">Go слишком**«Консоли администрирования»**</span><span class="sxs-lookup"><span data-stu-id="cc948-167">Go too**'Admin Console'**</span></span>

    ![Консоль администрирования](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="cc948-169">Из hello **«Консоли администрирования»**, перейдите в слишком**«Безопасность»** и выберите **"единый вход"**</span><span class="sxs-lookup"><span data-stu-id="cc948-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="cc948-171">Настройте hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="cc948-171">Configure hello following values:</span></span>

    ![Настройка сертификата](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="cc948-173">а.</span><span class="sxs-lookup"><span data-stu-id="cc948-173">a.</span></span>  <span data-ttu-id="cc948-174">**Включение единого входа:** единый вход включен по умолчанию (щелкните **отключить Single Sign-on** требование SSO hello tooremove)</span><span class="sxs-lookup"><span data-stu-id="cc948-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="cc948-175">b.</span><span class="sxs-lookup"><span data-stu-id="cc948-175">b.</span></span> <span data-ttu-id="cc948-176">Вставить **SAML единого входа для URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес SAML HTTP запроса** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="cc948-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="cc948-177">c.</span><span class="sxs-lookup"><span data-stu-id="cc948-177">c.</span></span> <span data-ttu-id="cc948-178">Откройте загруженный сертификат hello из Azure AD в Блокноте и скопируйте содержимое hello, включая «BEGIN» и «END сертификата» и вставьте его в hello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="cc948-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="cc948-179">Щелкните **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="cc948-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="cc948-180">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="cc948-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc948-181">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="cc948-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc948-182">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc948-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cc948-183">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc948-183">Create an Azure AD test user</span></span>

<span data-ttu-id="cc948-184">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cc948-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="cc948-186">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cc948-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc948-187">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="cc948-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cc948-189">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="cc948-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cc948-191">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="cc948-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cc948-193">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="cc948-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cc948-195">а.</span><span class="sxs-lookup"><span data-stu-id="cc948-195">a.</span></span> <span data-ttu-id="cc948-196">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc948-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc948-197">b.</span><span class="sxs-lookup"><span data-stu-id="cc948-197">b.</span></span> <span data-ttu-id="cc948-198">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="cc948-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="cc948-199">c.</span><span class="sxs-lookup"><span data-stu-id="cc948-199">c.</span></span> <span data-ttu-id="cc948-200">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="cc948-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="cc948-201">d.</span><span class="sxs-lookup"><span data-stu-id="cc948-201">d.</span></span> <span data-ttu-id="cc948-202">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cc948-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="cc948-203">Создание тестового пользователя Evernote</span><span class="sxs-lookup"><span data-stu-id="cc948-203">Create an Evernote test user</span></span>

<span data-ttu-id="cc948-204">В порядке tooenable toolog пользователей Azure AD в Evernote их необходимо подготовить в Evernote.</span><span class="sxs-lookup"><span data-stu-id="cc948-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="cc948-205">В случае Evernote hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="cc948-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="cc948-206">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="cc948-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc948-207">Войдите в систему tooyour Evernote сайт компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="cc948-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="cc948-208">Нажмите кнопку hello **«Консоли администрирования»**.</span><span class="sxs-lookup"><span data-stu-id="cc948-208">Click hello **'Admin Console'**.</span></span>

    ![Консоль администрирования](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="cc948-210">Из hello **«Консоли администрирования»**, перейдите в слишком**«Добавление пользователей»**.</span><span class="sxs-lookup"><span data-stu-id="cc948-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![Добавление тестового пользователя](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="cc948-212">**Добавление членов команды** в hello **электронной почты** текстовое поле, введите адрес электронной почты hello учетной записи пользователя и нажмите кнопку **приглашения.**</span><span class="sxs-lookup"><span data-stu-id="cc948-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![Добавление тестового пользователя](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="cc948-214">После отправки приглашения hello владельцем учетной записи Azure Active Directory получит по электронной почте приглашение tooaccept hello.</span><span class="sxs-lookup"><span data-stu-id="cc948-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cc948-215">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="cc948-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cc948-216">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooEvernote доступа.</span><span class="sxs-lookup"><span data-stu-id="cc948-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="cc948-218">**tooassign tooEvernote Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cc948-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc948-219">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cc948-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="cc948-221">В списке приложений hello выберите **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="cc948-221">In hello applications list, select **Evernote**.</span></span>

    ![ссылка Evernote Hello в списке приложений hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="cc948-223">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="cc948-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="cc948-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cc948-225">Click **Add** button.</span></span> <span data-ttu-id="cc948-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cc948-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="cc948-228">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="cc948-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc948-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cc948-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc948-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="cc948-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cc948-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="cc948-231">Test single sign-on</span></span>

<span data-ttu-id="cc948-232">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="cc948-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc948-233">Если щелкнуть плитку Evernote hello в hello панели доступа, следует получать вошедшего tooyour Evernote приложения.</span><span class="sxs-lookup"><span data-stu-id="cc948-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="cc948-234">Вы сможете вход как учетная запись организации, но затем toolog необходимость личную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="cc948-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cc948-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cc948-235">Additional resources</span></span>

* [<span data-ttu-id="cc948-236">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc948-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc948-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc948-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

