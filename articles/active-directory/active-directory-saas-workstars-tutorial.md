---
title: "Руководство. Интеграция Azure Active Directory с Workstars | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="c4d3d-103">Учебник. Интеграция Azure Active Directory с Workstars</span><span class="sxs-lookup"><span data-stu-id="c4d3d-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="c4d3d-104">В этом учебнике вы узнаете, как toointegrate Workstars с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4d3d-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4d3d-105">Интеграция с Azure AD Workstars предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c4d3d-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4d3d-106">Можно управлять в Azure AD, имеющего доступ tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="c4d3d-107">Можно включить на пользователей tooautomatically get вошедшего tooWorkstars (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c4d3d-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c4d3d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4d3d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4d3d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c4d3d-110">Prerequisites</span></span>

<span data-ttu-id="c4d3d-111">tooconfigure интеграция Azure AD с Workstars требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c4d3d-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="c4d3d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c4d3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4d3d-113">подписка Workstars с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4d3d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4d3d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c4d3d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4d3d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4d3d-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4d3d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4d3d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c4d3d-118">Scenario description</span></span>
<span data-ttu-id="c4d3d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4d3d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c4d3d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4d3d-121">Добавление Workstars из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c4d3d-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="c4d3d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4d3d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="c4d3d-123">Добавление Workstars из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c4d3d-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="c4d3d-124">tooconfigure hello интеграции Workstars в Azure AD, вы должны tooadd Workstars из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4d3d-125">**tooadd Workstars из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4d3d-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4d3d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="c4d3d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4d3d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="c4d3d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="c4d3d-133">Введите в поле поиска hello **Workstars**выберите **Workstars** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workstars в списке результатов hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c4d3d-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4d3d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c4d3d-136">В этом разделе описана настройка и проверка единого входа Azure AD в Workstars с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4d3d-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Workstars является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="c4d3d-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Workstars должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="c4d3d-139">В Workstars, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c4d3d-140">tooconfigure и теста Azure AD единого входа с Workstars, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c4d3d-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4d3d-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4d3d-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4d3d-143">**[Создание тестового пользователя Workstars](#create-a-workstars-test-user)**  -toohave аналог Саймон Britta в Workstars, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4d3d-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4d3d-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c4d3d-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4d3d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c4d3d-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Workstars.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="c4d3d-148">**tooconfigure Azure AD единого входа с Workstars, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4d3d-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4d3d-149">В hello в hello портала Azure **Workstars** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="c4d3d-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="c4d3d-153">На hello **URL-адреса и домена Workstars** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c4d3d-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="c4d3d-155">а.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-155">a.</span></span> <span data-ttu-id="c4d3d-156">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="c4d3d-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="c4d3d-157">b.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-157">b.</span></span> <span data-ttu-id="c4d3d-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="c4d3d-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4d3d-159">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-159">hello value is not real.</span></span> <span data-ttu-id="c4d3d-160">Значение hello обновления с hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="c4d3d-161">Обратитесь к [Workstars поддержки](https://support.workstars.com) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="c4d3d-162">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="c4d3d-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c4d3d-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4d3d-166">На hello **конфигурации Workstars** щелкните **Настройка Workstars** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c4d3d-167">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c4d3d-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="c4d3d-169">В другом окне браузера Войдите на сайт компании Workstars tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="c4d3d-170">На главной панели инструментов hello, щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-170">In hello main toolbar, click **Settings**.</span></span>

    ![Настройки Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="c4d3d-172">Go слишком**входа** > **параметры**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-172">Go too**Sign On** > **Settings**.</span></span>

    ![Workstars, раздел "Вход"](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Workstars, раздел "Настройки"](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="c4d3d-175">На hello **единого входа на (SAML) - параметры** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c4d3d-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![Настройки SAML в Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="c4d3d-177">а.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-177">a.</span></span> <span data-ttu-id="c4d3d-178">В текстовом поле **Identity Provider Name** (Имя поставщика удостоверений) введите **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="c4d3d-179">b.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-179">b.</span></span> <span data-ttu-id="c4d3d-180">В hello **идентификатор сущности поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c4d3d-181">c.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-181">c.</span></span> <span data-ttu-id="c4d3d-182">Скопируйте содержимое hello hello загруженный сертификат файл в Блокноте и вставьте его в hello **x509 сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="c4d3d-183">d.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-183">d.</span></span> <span data-ttu-id="c4d3d-184">В hello **URL-адрес единого входа SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c4d3d-185">д.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-185">e.</span></span> <span data-ttu-id="c4d3d-186">В hello **URL-адрес удаленного выхода** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c4d3d-187">f.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-187">f.</span></span> <span data-ttu-id="c4d3d-188">Для параметра **Name ID** (Идентификатор имени) выберите значение **Email (Default)** (Адрес электронной почты (по умолчанию)).</span><span class="sxs-lookup"><span data-stu-id="c4d3d-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="c4d3d-189">g.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-189">g.</span></span> <span data-ttu-id="c4d3d-190">Щелкните **Confirm** (Подтвердить).</span><span class="sxs-lookup"><span data-stu-id="c4d3d-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="c4d3d-191">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c4d3d-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4d3d-192">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4d3d-193">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4d3d-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c4d3d-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4d3d-194">Create an Azure AD test user</span></span>

<span data-ttu-id="c4d3d-195">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="c4d3d-197">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4d3d-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4d3d-198">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c4d3d-200">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c4d3d-202">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c4d3d-204">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c4d3d-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c4d3d-206">а.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-206">a.</span></span> <span data-ttu-id="c4d3d-207">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4d3d-208">b.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-208">b.</span></span> <span data-ttu-id="c4d3d-209">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c4d3d-210">c.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-210">c.</span></span> <span data-ttu-id="c4d3d-211">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c4d3d-212">d.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-212">d.</span></span> <span data-ttu-id="c4d3d-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="c4d3d-214">Создание тестового пользователя Workstars</span><span class="sxs-lookup"><span data-stu-id="c4d3d-214">Create a Workstars test user</span></span>

<span data-ttu-id="c4d3d-215">В этом разделе описано, как создать пользователя Britta Simon в приложении Workstars.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="c4d3d-216">Работать с [Workstars поддержки](https://support.workstars.com) tooadd hello пользователей на платформе Workstars hello.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c4d3d-217">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c4d3d-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c4d3d-218">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWorkstars доступа.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="c4d3d-220">**tooassign tooWorkstars Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4d3d-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4d3d-221">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c4d3d-223">В списке приложений hello выберите **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-223">In hello applications list, select **Workstars**.</span></span>

    ![ссылка Workstars Hello в списке приложений hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="c4d3d-225">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="c4d3d-227">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-227">Click **Add** button.</span></span> <span data-ttu-id="c4d3d-228">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="c4d3d-230">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4d3d-231">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4d3d-232">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c4d3d-233">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c4d3d-233">Test single sign-on</span></span>

<span data-ttu-id="c4d3d-234">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c4d3d-235">При нажатии кнопки Workstars плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Workstars приложения.</span><span class="sxs-lookup"><span data-stu-id="c4d3d-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="c4d3d-236">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4d3d-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c4d3d-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c4d3d-237">Additional resources</span></span>

* [<span data-ttu-id="c4d3d-238">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4d3d-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4d3d-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4d3d-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

