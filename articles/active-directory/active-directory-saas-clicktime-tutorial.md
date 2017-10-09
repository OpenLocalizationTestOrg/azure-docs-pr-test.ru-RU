---
title: "Учебник. Интеграция Azure Active Directory с ClickTime | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="fe754-103">Руководство. Интеграция Azure Active Directory с ClickTime</span><span class="sxs-lookup"><span data-stu-id="fe754-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="fe754-104">В этом учебнике вы узнаете, как toointegrate ClickTime с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe754-104">In this tutorial, you learn how toointegrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fe754-105">Интеграция ClickTime с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="fe754-105">Integrating ClickTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fe754-106">Можно управлять в Azure AD, имеющего доступ tooClickTime</span><span class="sxs-lookup"><span data-stu-id="fe754-106">You can control in Azure AD who has access tooClickTime</span></span>
- <span data-ttu-id="fe754-107">Можно включить на пользователей tooautomatically get вошедшего tooClickTime (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe754-107">You can enable your users tooautomatically get signed-on tooClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fe754-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="fe754-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fe754-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe754-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe754-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fe754-110">Prerequisites</span></span>

<span data-ttu-id="fe754-111">tooconfigure интеграция Azure AD с ClickTime требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="fe754-111">tooconfigure Azure AD integration with ClickTime, you need hello following items:</span></span>

- <span data-ttu-id="fe754-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="fe754-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fe754-113">подписка ClickTime с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="fe754-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe754-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="fe754-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fe754-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="fe754-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fe754-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="fe754-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fe754-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe754-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe754-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="fe754-118">Scenario description</span></span>
<span data-ttu-id="fe754-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="fe754-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fe754-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="fe754-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe754-121">Добавление ClickTime из галереи hello</span><span class="sxs-lookup"><span data-stu-id="fe754-121">Adding ClickTime from hello gallery</span></span>
2. <span data-ttu-id="fe754-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe754-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-hello-gallery"></a><span data-ttu-id="fe754-123">Добавление ClickTime из галереи hello</span><span class="sxs-lookup"><span data-stu-id="fe754-123">Adding ClickTime from hello gallery</span></span>
<span data-ttu-id="fe754-124">tooconfigure hello интеграции ClickTime в Azure AD, вы должны tooadd ClickTime из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="fe754-124">tooconfigure hello integration of ClickTime into Azure AD, you need tooadd ClickTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fe754-125">**tooadd ClickTime из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fe754-125">**tooadd ClickTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe754-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="fe754-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="fe754-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="fe754-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fe754-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fe754-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="fe754-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="fe754-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="fe754-133">Введите в поле поиска hello **ClickTime**выберите **ClickTime** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fe754-133">In hello search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ClickTime в списке результатов hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fe754-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe754-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fe754-136">В этом разделе описана настройка и проверка единого входа Azure AD в ClickTime с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe754-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fe754-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ClickTime является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe754-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ClickTime is tooa user in Azure AD.</span></span> <span data-ttu-id="fe754-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в ClickTime должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="fe754-138">In other words, a link relationship between an Azure AD user and hello related user in ClickTime needs toobe established.</span></span>

<span data-ttu-id="fe754-139">В ClickTime, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="fe754-139">In ClickTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fe754-140">tooconfigure и теста Azure AD единого входа с ClickTime, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="fe754-140">tooconfigure and test Azure AD single sign-on with ClickTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fe754-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="fe754-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fe754-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="fe754-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fe754-143">**[Создание тестового пользователя ClickTime](#create-a-clicktime-test-user)**  -toohave аналог Саймон Britta в ClickTime, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="fe754-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - toohave a counterpart of Britta Simon in ClickTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fe754-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="fe754-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fe754-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fe754-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fe754-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe754-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fe754-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fe754-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="fe754-148">**Azure AD tooconfigure единого входа с ClickTime, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fe754-148">**tooconfigure Azure AD single sign-on with ClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe754-149">В hello в hello портала Azure **ClickTime** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="fe754-149">In hello Azure portal, on hello **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="fe754-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="fe754-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="fe754-153">На hello **URL-адреса и домена ClickTime** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fe754-153">On hello **ClickTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="fe754-155">а.</span><span class="sxs-lookup"><span data-stu-id="fe754-155">a.</span></span> <span data-ttu-id="fe754-156">В hello **идентификатор** текстовом поле введите URL-адрес как:`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="fe754-156">In hello **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="fe754-157">b.</span><span class="sxs-lookup"><span data-stu-id="fe754-157">b.</span></span> <span data-ttu-id="fe754-158">В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="fe754-158">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="fe754-159">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="fe754-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="fe754-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="fe754-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fe754-163">На hello **конфигурации ClickTime** щелкните **Настройка ClickTime** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="fe754-163">On hello **ClickTime Configuration** section, click **Configure ClickTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fe754-164">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="fe754-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="fe754-166">В другом окне веб-браузера войдите на свой корпоративный веб-сайт ClickTime в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="fe754-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="fe754-167">Щелкните hello панели инструментов в верхней части hello **предпочтения**, а затем нажмите кнопку **параметры безопасности**.</span><span class="sxs-lookup"><span data-stu-id="fe754-167">In hello toolbar on hello top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="fe754-168">В hello **предпочтения-** конфигурации выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fe754-168">In hello **Single Sign-On Preferences** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fe754-169">![Параметры безопасности](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Параметры безопасности")</span><span class="sxs-lookup"><span data-stu-id="fe754-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="fe754-170">а.</span><span class="sxs-lookup"><span data-stu-id="fe754-170">a.</span></span>  <span data-ttu-id="fe754-171">Выберите "**Allow** sign-in using Single Sign-On (SSO) with **Azure AD**" (Разрешить единый вход (SSO) с помощью Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe754-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="fe754-172">b.</span><span class="sxs-lookup"><span data-stu-id="fe754-172">b.</span></span> <span data-ttu-id="fe754-173">В hello **конечная точка поставщика удостоверений** вставьте **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="fe754-173">In hello **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fe754-174">c.</span><span class="sxs-lookup"><span data-stu-id="fe754-174">c.</span></span>  <span data-ttu-id="fe754-175">Откройте hello **сертификат в кодировке base-64** загружен с портала Azure в **Блокнот**, скопируйте содержимое hello и вставьте его в hello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="fe754-175">Open hello **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="fe754-176">d.</span><span class="sxs-lookup"><span data-stu-id="fe754-176">d.</span></span>  <span data-ttu-id="fe754-177">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fe754-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fe754-178">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="fe754-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fe754-179">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="fe754-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fe754-180">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fe754-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fe754-181">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe754-181">Create an Azure AD test user</span></span>
<span data-ttu-id="fe754-182">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fe754-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="fe754-184">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fe754-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe754-185">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="fe754-185">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fe754-187">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="fe754-187">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fe754-189">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="fe754-189">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fe754-191">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fe754-191">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fe754-193">а.</span><span class="sxs-lookup"><span data-stu-id="fe754-193">a.</span></span> <span data-ttu-id="fe754-194">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe754-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fe754-195">b.</span><span class="sxs-lookup"><span data-stu-id="fe754-195">b.</span></span> <span data-ttu-id="fe754-196">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fe754-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fe754-197">c.</span><span class="sxs-lookup"><span data-stu-id="fe754-197">c.</span></span> <span data-ttu-id="fe754-198">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="fe754-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fe754-199">d.</span><span class="sxs-lookup"><span data-stu-id="fe754-199">d.</span></span> <span data-ttu-id="fe754-200">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fe754-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="fe754-201">Создание тестового пользователя ClickTime</span><span class="sxs-lookup"><span data-stu-id="fe754-201">Create a ClickTime test user</span></span>

<span data-ttu-id="fe754-202">В порядке tooenable toolog пользователей Azure AD в ClickTime их необходимо подготовить в ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fe754-202">In order tooenable Azure AD users toolog into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="fe754-203">В случае hello ClickTime Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="fe754-203">In hello case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="fe754-204">Можно использовать любые другие ClickTime пользователя средства создания учетных записей или API, предоставленные ClickTime tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe754-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime tooprovision Azure AD user accounts.</span></span>

<span data-ttu-id="fe754-205">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fe754-205">**tooprovision a user account, perform hello following steps:**</span></span>
1. <span data-ttu-id="fe754-206">Войдите в tooyour **ClickTime** клиента.</span><span class="sxs-lookup"><span data-stu-id="fe754-206">Log in tooyour **ClickTime** tenant.</span></span>
2. <span data-ttu-id="fe754-207">Щелкните hello панели инструментов в верхней части hello **компании**, а затем нажмите кнопку **людей**.</span><span class="sxs-lookup"><span data-stu-id="fe754-207">In hello toolbar on hello top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="fe754-208">![Люди](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="fe754-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="fe754-209">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="fe754-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="fe754-210">![Добавление пользователя](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="fe754-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="fe754-211">В hello раздела новый пользователь выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="fe754-211">In hello New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fe754-212">![Люди](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="fe754-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="fe754-213">а.</span><span class="sxs-lookup"><span data-stu-id="fe754-213">a.</span></span>  <span data-ttu-id="fe754-214">В hello **полное имя** введите полное имя пользователя, таких как **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fe754-214">In hello **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="fe754-215">b.</span><span class="sxs-lookup"><span data-stu-id="fe754-215">b.</span></span>  <span data-ttu-id="fe754-216">В hello **адрес электронной почты** электронной почты hello тип пользователя в текстовое поле, например  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="fe754-216">In hello **email address** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="fe754-217">Если вы хотите, можно задать дополнительные свойства объекта hello нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="fe754-217">If you want to, you can set additional properties of hello new person object.</span></span>
   
    <span data-ttu-id="fe754-218">c.</span><span class="sxs-lookup"><span data-stu-id="fe754-218">c.</span></span>  <span data-ttu-id="fe754-219">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fe754-219">Click **Save**.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fe754-220">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="fe754-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fe754-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooClickTime доступа.</span><span class="sxs-lookup"><span data-stu-id="fe754-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClickTime.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="fe754-223">**tooassign tooClickTime Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fe754-223">**tooassign Britta Simon tooClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe754-224">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fe754-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="fe754-226">В списке приложений hello выберите **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="fe754-226">In hello applications list, select **ClickTime**.</span></span>

    ![ClickTimne ссылку в списке приложений hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="fe754-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="fe754-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="fe754-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fe754-230">Click **Add** button.</span></span> <span data-ttu-id="fe754-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fe754-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="fe754-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="fe754-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fe754-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fe754-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fe754-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="fe754-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fe754-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="fe754-236">Test single sign-on</span></span>

<span data-ttu-id="fe754-237">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="fe754-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fe754-238">При нажатии кнопки hello ClickTime плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fe754-238">When you click hello ClickTime tile in hello Access Panel, you should get automatically signed-on tooyour ClickTime application.</span></span>
<span data-ttu-id="fe754-239">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fe754-239">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe754-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fe754-240">Additional resources</span></span>

* [<span data-ttu-id="fe754-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe754-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe754-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fe754-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

