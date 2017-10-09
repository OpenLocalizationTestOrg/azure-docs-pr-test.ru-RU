---
title: "Руководство по интеграции Azure Active Directory с PagerDuty | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="2d918-103">Руководство по интеграции Azure Active Directory с PagerDuty</span><span class="sxs-lookup"><span data-stu-id="2d918-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="2d918-104">В этом учебнике вы узнаете, как toointegrate PagerDuty с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d918-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d918-105">Интеграция PagerDuty с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="2d918-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2d918-106">Можно управлять в Azure AD, имеющего доступ tooPagerDuty</span><span class="sxs-lookup"><span data-stu-id="2d918-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="2d918-107">Можно включить на пользователей tooautomatically get вошедшего tooPagerDuty (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d918-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d918-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="2d918-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2d918-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d918-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d918-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2d918-110">Prerequisites</span></span>

<span data-ttu-id="2d918-111">tooconfigure интеграция Azure AD с PagerDuty требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2d918-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="2d918-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2d918-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d918-113">подписка PagerDuty с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="2d918-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d918-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="2d918-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d918-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="2d918-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d918-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="2d918-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d918-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d918-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d918-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2d918-118">Scenario description</span></span>
<span data-ttu-id="2d918-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2d918-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d918-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="2d918-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d918-121">Добавление PagerDuty из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2d918-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="2d918-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d918-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="2d918-123">Добавление PagerDuty из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2d918-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="2d918-124">tooconfigure hello интеграции PagerDuty в Azure AD, вы должны tooadd PagerDuty из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2d918-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d918-125">**tooadd PagerDuty из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2d918-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d918-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="2d918-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="2d918-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="2d918-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2d918-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2d918-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="2d918-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="2d918-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="2d918-133">Введите в поле поиска hello **PagerDuty**выберите **PagerDuty** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2d918-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2d918-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d918-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2d918-136">В этом разделе описана настройка и проверка единого входа Azure AD в PagerDuty с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d918-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2d918-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PagerDuty является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d918-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="2d918-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в PagerDuty должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="2d918-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="2d918-139">В PagerDuty, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="2d918-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2d918-140">tooconfigure и теста Azure AD единого входа с PagerDuty, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2d918-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2d918-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="2d918-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2d918-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="2d918-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d918-143">**[Создание тестового пользователя PagerDuty](#create-a-pagerduty-test-user)**  -toohave аналог Саймон Britta в PagerDuty, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="2d918-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d918-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="2d918-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d918-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2d918-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2d918-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d918-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2d918-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в PagerDuty приложения.</span><span class="sxs-lookup"><span data-stu-id="2d918-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="2d918-148">**Azure AD tooconfigure единого входа с PagerDuty, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2d918-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d918-149">В hello в hello портала Azure **PagerDuty** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="2d918-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="2d918-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="2d918-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="2d918-153">На hello **URL-адреса и домена PagerDuty** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2d918-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="2d918-155">а.</span><span class="sxs-lookup"><span data-stu-id="2d918-155">a.</span></span> <span data-ttu-id="2d918-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="2d918-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="2d918-157">b.</span><span class="sxs-lookup"><span data-stu-id="2d918-157">b.</span></span> <span data-ttu-id="2d918-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="2d918-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d918-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="2d918-159">These values are not real.</span></span> <span data-ttu-id="2d918-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="2d918-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2d918-161">Обратитесь к [группа поддержки клиент PagerDuty](https://www.pagerduty.com/support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="2d918-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="2d918-162">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="2d918-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="2d918-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2d918-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2d918-166">На hello **конфигурации PagerDuty** щелкните **Настройка PagerDuty** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="2d918-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2d918-167">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="2d918-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="2d918-169">В другом окне браузера войдите на свой сайт PagerDuty компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="2d918-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="2d918-170">В меню в верхней части hello hello выберите **параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="2d918-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="2d918-171">![Параметры учетной записи](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="2d918-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="2d918-172">Щелкните **Single Sign-on**(Единый вход).</span><span class="sxs-lookup"><span data-stu-id="2d918-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="2d918-173">![Единый вход](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="2d918-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="2d918-174">На hello **Включение единого входа (SSO)** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2d918-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d918-175">![Разрешить единый вход](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Разрешить единый вход")</span><span class="sxs-lookup"><span data-stu-id="2d918-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="2d918-176">а.</span><span class="sxs-lookup"><span data-stu-id="2d918-176">a.</span></span> <span data-ttu-id="2d918-177">Откройте сертификат кодировке base-64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля</span><span class="sxs-lookup"><span data-stu-id="2d918-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="2d918-178">b.</span><span class="sxs-lookup"><span data-stu-id="2d918-178">b.</span></span> <span data-ttu-id="2d918-179">В hello **URL-адрес входа** вставьте **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2d918-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="2d918-180">c.</span><span class="sxs-lookup"><span data-stu-id="2d918-180">c.</span></span> <span data-ttu-id="2d918-181">В hello **URL-адрес выхода** вставьте **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2d918-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="2d918-182">d.</span><span class="sxs-lookup"><span data-stu-id="2d918-182">d.</span></span> <span data-ttu-id="2d918-183">Установите флажок **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="2d918-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="2d918-184">д.</span><span class="sxs-lookup"><span data-stu-id="2d918-184">e.</span></span> <span data-ttu-id="2d918-185">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="2d918-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2d918-186">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="2d918-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2d918-187">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="2d918-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2d918-188">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d918-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2d918-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d918-189">Create an Azure AD test user</span></span>

<span data-ttu-id="2d918-190">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2d918-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="2d918-192">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2d918-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d918-193">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="2d918-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d918-195">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2d918-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d918-197">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="2d918-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d918-199">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2d918-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d918-201">а.</span><span class="sxs-lookup"><span data-stu-id="2d918-201">a.</span></span> <span data-ttu-id="2d918-202">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d918-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d918-203">b.</span><span class="sxs-lookup"><span data-stu-id="2d918-203">b.</span></span> <span data-ttu-id="2d918-204">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d918-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d918-205">c.</span><span class="sxs-lookup"><span data-stu-id="2d918-205">c.</span></span> <span data-ttu-id="2d918-206">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="2d918-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2d918-207">d.</span><span class="sxs-lookup"><span data-stu-id="2d918-207">d.</span></span> <span data-ttu-id="2d918-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2d918-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="2d918-209">Создание тестового пользователя PagerDuty</span><span class="sxs-lookup"><span data-stu-id="2d918-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="2d918-210">Пользователи toolog tooenable Azure AD в tooPagerDuty, их необходимо подготовить в PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2d918-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="2d918-211">В случае PagerDuty hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="2d918-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="2d918-212">Можно использовать любые другие Pagerduty пользователя средства создания учетных записей или API, предоставленные Pagerduty tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="2d918-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="2d918-213">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2d918-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d918-214">Войдите в tooyour **Pagerduty** клиента.</span><span class="sxs-lookup"><span data-stu-id="2d918-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="2d918-215">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2d918-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="2d918-216">Щелкните **Добавить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2d918-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="2d918-217">![Добавление пользователей](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "добавление пользователей")</span><span class="sxs-lookup"><span data-stu-id="2d918-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="2d918-218">На hello **пригласить команду** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2d918-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d918-219">![Пригласить команду](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Пригласить команду")</span><span class="sxs-lookup"><span data-stu-id="2d918-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="2d918-220">а.</span><span class="sxs-lookup"><span data-stu-id="2d918-220">a.</span></span> <span data-ttu-id="2d918-221">Тип hello **имя и фамилию** пользователя как **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2d918-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="2d918-222">b.</span><span class="sxs-lookup"><span data-stu-id="2d918-222">b.</span></span> <span data-ttu-id="2d918-223">Введите **Email** (Адрес электронной почты) для пользователя, например: **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2d918-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="2d918-224">c.</span><span class="sxs-lookup"><span data-stu-id="2d918-224">c.</span></span> <span data-ttu-id="2d918-225">Нажмите **Add** (Добавить), затем нажмите **Send Invites** (Отправить приглашения).</span><span class="sxs-lookup"><span data-stu-id="2d918-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="2d918-226">Все добавленные пользователи получат приглашение toocreate учетную запись PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2d918-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2d918-227">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="2d918-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2d918-228">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPagerDuty доступа.</span><span class="sxs-lookup"><span data-stu-id="2d918-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Назначение пользователям ролей hello][200]

<span data-ttu-id="2d918-230">**tooassign tooPagerDuty Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2d918-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d918-231">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2d918-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2d918-233">В списке приложений hello выберите **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="2d918-233">In hello applications list, select **PagerDuty**.</span></span>

    ![ссылка PagerDuty Hello в списке приложений hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="2d918-235">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="2d918-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="2d918-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2d918-237">Click **Add** button.</span></span> <span data-ttu-id="2d918-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2d918-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="2d918-240">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="2d918-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2d918-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2d918-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d918-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="2d918-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2d918-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2d918-243">Test single sign-on</span></span>

<span data-ttu-id="2d918-244">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="2d918-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2d918-245">При нажатии кнопки hello PagerDuty плитки в hello Panelyou доступа следует получать автоматически вошедшего tooyour PagerDuty приложения.</span><span class="sxs-lookup"><span data-stu-id="2d918-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="2d918-246">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d918-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d918-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2d918-247">Additional resources</span></span>

* [<span data-ttu-id="2d918-248">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d918-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d918-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2d918-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

