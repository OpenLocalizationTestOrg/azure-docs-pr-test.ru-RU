---
title: "Руководство по интеграции Azure Active Directory с Sprinklr | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="3480b-103">Учебник. Интеграция Azure Active Directory с Sprinklr</span><span class="sxs-lookup"><span data-stu-id="3480b-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="3480b-104">В этом учебнике вы узнаете, как toointegrate Sprinklr с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3480b-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3480b-105">Интеграция Sprinklr с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3480b-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3480b-106">Можно управлять в Azure AD, имеющего доступ tooSprinklr</span><span class="sxs-lookup"><span data-stu-id="3480b-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="3480b-107">Можно включить на пользователей tooautomatically get вошедшего tooSprinklr (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="3480b-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3480b-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3480b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3480b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3480b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3480b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3480b-110">Prerequisites</span></span>

<span data-ttu-id="3480b-111">tooconfigure интеграция Azure AD с Sprinklr требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3480b-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="3480b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3480b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3480b-113">подписка Sprinklr с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3480b-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3480b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3480b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3480b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3480b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3480b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3480b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3480b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3480b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3480b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3480b-118">Scenario description</span></span>
<span data-ttu-id="3480b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3480b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3480b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3480b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3480b-121">Добавление Sprinklr из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3480b-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="3480b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3480b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="3480b-123">Добавление Sprinklr из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3480b-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="3480b-124">tooconfigure hello интеграции Sprinklr в Azure AD, вы должны tooadd Sprinklr из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3480b-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3480b-125">**tooadd Sprinklr из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3480b-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3480b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3480b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3480b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3480b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3480b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3480b-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3480b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3480b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3480b-133">Введите в поле поиска hello **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="3480b-133">In hello search box, type **Sprinklr**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="3480b-135">В панели результатов hello выберите **Sprinklr**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3480b-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3480b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3480b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3480b-138">В этом разделе описана настройка и проверка единого входа Azure AD в Sprinklr для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3480b-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3480b-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Sprinklr является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3480b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="3480b-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Sprinklr должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3480b-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="3480b-141">В Sprinklr, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="3480b-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3480b-142">tooconfigure и теста Azure AD единого входа с Sprinklr, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3480b-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3480b-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3480b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3480b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3480b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3480b-145">**[Создание тестового пользователя Sprinklr](#creating-a-sprinklr-test-user)**  -toohave аналог Саймон Britta в Sprinklr, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3480b-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3480b-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3480b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3480b-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3480b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3480b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3480b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3480b-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="3480b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="3480b-150">**Azure AD tooconfigure единого входа с Sprinklr, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3480b-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="3480b-151">В hello в hello портала Azure **Sprinklr** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3480b-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3480b-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3480b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="3480b-155">На hello **URL-адреса и домена Sprinklr** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3480b-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="3480b-157">а.</span><span class="sxs-lookup"><span data-stu-id="3480b-157">a.</span></span> <span data-ttu-id="3480b-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="3480b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="3480b-159">b.</span><span class="sxs-lookup"><span data-stu-id="3480b-159">b.</span></span> <span data-ttu-id="3480b-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="3480b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3480b-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3480b-161">These values are not real.</span></span> <span data-ttu-id="3480b-162">Обновите значение hello с hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="3480b-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3480b-163">Обратитесь к [группа поддержки клиент Sprinklr](https://www.sprinklr.com/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="3480b-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="3480b-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3480b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="3480b-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3480b-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3480b-168">На hello **конфигурации Sprinklr** щелкните **Настройка Sprinklr** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="3480b-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3480b-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="3480b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="3480b-170">В другом окне браузера войти в корпоративный сайт Sprinklr tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3480b-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="3480b-171">Go слишком**администрирования \> параметры**.</span><span class="sxs-lookup"><span data-stu-id="3480b-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="3480b-172">![Администрирование](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="3480b-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="3480b-173">Go слишком**управление партнера \> единого входа** на левой панели щелкните hello.</span><span class="sxs-lookup"><span data-stu-id="3480b-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="3480b-174">![Управление партнером](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Управление партнером")</span><span class="sxs-lookup"><span data-stu-id="3480b-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="3480b-175">Щелкните **+ Добавить параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3480b-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="3480b-176">![Единый вход](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="3480b-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="3480b-177">На hello **единого входа в систему** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3480b-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="3480b-178">![Единый вход](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="3480b-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="3480b-179">а.</span><span class="sxs-lookup"><span data-stu-id="3480b-179">a.</span></span> <span data-ttu-id="3480b-180">В hello **имя** текстовом поле введите имя для конфигурации (например: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="3480b-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="3480b-181">b.</span><span class="sxs-lookup"><span data-stu-id="3480b-181">b.</span></span> <span data-ttu-id="3480b-182">Щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="3480b-182">Select **Enabled**.</span></span>

    <span data-ttu-id="3480b-183">c.</span><span class="sxs-lookup"><span data-stu-id="3480b-183">c.</span></span> <span data-ttu-id="3480b-184">Установите флажок **Использовать новый сертификат единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3480b-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="3480b-185">д.</span><span class="sxs-lookup"><span data-stu-id="3480b-185">e.</span></span> <span data-ttu-id="3480b-186">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="3480b-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="3480b-187">f.</span><span class="sxs-lookup"><span data-stu-id="3480b-187">f.</span></span> <span data-ttu-id="3480b-188">Вставить hello **идентификатор сущности SAML** значение, которое было скопировано из портала Azure в hello **идентификатор сущности** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="3480b-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="3480b-189">ж.</span><span class="sxs-lookup"><span data-stu-id="3480b-189">g.</span></span> <span data-ttu-id="3480b-190">Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из портала Azure в hello **URL-адрес входа поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="3480b-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="3480b-191">h.</span><span class="sxs-lookup"><span data-stu-id="3480b-191">h.</span></span> <span data-ttu-id="3480b-192">Вставить hello **URL-адрес выхода** значение, которое было скопировано из портала Azure в hello **URL-адрес выхода поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="3480b-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="3480b-193">i.</span><span class="sxs-lookup"><span data-stu-id="3480b-193">i.</span></span> <span data-ttu-id="3480b-194">В поле **SAML User ID Type** (Тип идентификатора пользователя SAML) выберите значение **Assertion contains User”s sprinklr.com username** (Утверждение содержит имя пользователя sprinklr.com).</span><span class="sxs-lookup"><span data-stu-id="3480b-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="3480b-195">j.</span><span class="sxs-lookup"><span data-stu-id="3480b-195">j.</span></span> <span data-ttu-id="3480b-196">Как **местоположение идентификатора пользователя SAML**выберите **идентификатор пользователя находится в элемент идентификатора имени hello hello оператора Subject**.</span><span class="sxs-lookup"><span data-stu-id="3480b-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="3480b-197">k.</span><span class="sxs-lookup"><span data-stu-id="3480b-197">k.</span></span> <span data-ttu-id="3480b-198">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3480b-198">Click **Save**.</span></span>
       
    <span data-ttu-id="3480b-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="3480b-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="3480b-200">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3480b-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3480b-201">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3480b-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3480b-202">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3480b-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3480b-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3480b-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="3480b-204">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3480b-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3480b-206">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3480b-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3480b-207">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3480b-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3480b-209">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3480b-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3480b-211">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="3480b-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3480b-213">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3480b-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3480b-215">а.</span><span class="sxs-lookup"><span data-stu-id="3480b-215">a.</span></span> <span data-ttu-id="3480b-216">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3480b-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3480b-217">b.</span><span class="sxs-lookup"><span data-stu-id="3480b-217">b.</span></span> <span data-ttu-id="3480b-218">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3480b-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3480b-219">c.</span><span class="sxs-lookup"><span data-stu-id="3480b-219">c.</span></span> <span data-ttu-id="3480b-220">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3480b-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3480b-221">d.</span><span class="sxs-lookup"><span data-stu-id="3480b-221">d.</span></span> <span data-ttu-id="3480b-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3480b-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="3480b-223">Создание тестового пользователя Skilljar</span><span class="sxs-lookup"><span data-stu-id="3480b-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="3480b-224">Войдите в tooyour корпоративный сайт Sprinklr с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3480b-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="3480b-225">Go слишком**администрирования \> параметры**.</span><span class="sxs-lookup"><span data-stu-id="3480b-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="3480b-226">![Администрирование](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="3480b-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="3480b-227">Go слишком**управление клиента \> пользователей** hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="3480b-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="3480b-228">![Параметры](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="3480b-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="3480b-229">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="3480b-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="3480b-230">![Параметры](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="3480b-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="3480b-231">На hello **пользователя изменить** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3480b-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="3480b-232">![Изменение пользователя](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Изменение пользователя")</span><span class="sxs-lookup"><span data-stu-id="3480b-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="3480b-233">а.</span><span class="sxs-lookup"><span data-stu-id="3480b-233">a.</span></span> <span data-ttu-id="3480b-234">В hello **электронной почты**, **имя** и **Фамилия** текстовые поля, типа hello сведения учетной записи пользователя в Azure AD, вы хотите tooprovision.</span><span class="sxs-lookup"><span data-stu-id="3480b-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="3480b-235">b.</span><span class="sxs-lookup"><span data-stu-id="3480b-235">b.</span></span> <span data-ttu-id="3480b-236">Установите флажок **Пароль отключен**.</span><span class="sxs-lookup"><span data-stu-id="3480b-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="3480b-237">c.</span><span class="sxs-lookup"><span data-stu-id="3480b-237">c.</span></span> <span data-ttu-id="3480b-238">Выберите **Язык**.</span><span class="sxs-lookup"><span data-stu-id="3480b-238">Select **Language**.</span></span>

    <span data-ttu-id="3480b-239">г)</span><span class="sxs-lookup"><span data-stu-id="3480b-239">d.</span></span> <span data-ttu-id="3480b-240">Выберите **Тип пользователя**.</span><span class="sxs-lookup"><span data-stu-id="3480b-240">Select **User Type**.</span></span>

    <span data-ttu-id="3480b-241">д.</span><span class="sxs-lookup"><span data-stu-id="3480b-241">e.</span></span> <span data-ttu-id="3480b-242">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="3480b-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="3480b-243">**Пароль отключен** должен быть выбранного tooenable в toolog пользователя через поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="3480b-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="3480b-244">Go слишком**роли**, а затем выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3480b-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="3480b-245">![Роли партнера](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Роли партнера")</span><span class="sxs-lookup"><span data-stu-id="3480b-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="3480b-246">а.</span><span class="sxs-lookup"><span data-stu-id="3480b-246">a.</span></span> <span data-ttu-id="3480b-247">Из hello **Global** выберите **все\_разрешений**.</span><span class="sxs-lookup"><span data-stu-id="3480b-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="3480b-248">b.</span><span class="sxs-lookup"><span data-stu-id="3480b-248">b.</span></span> <span data-ttu-id="3480b-249">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="3480b-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="3480b-250">Можно использовать любые другие Sprinklr пользователя средства создания учетных записей или API, предоставленные Sprinklr tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3480b-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3480b-251">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3480b-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3480b-252">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSprinklr доступа.</span><span class="sxs-lookup"><span data-stu-id="3480b-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3480b-254">**tooassign tooSprinklr Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3480b-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="3480b-255">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3480b-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3480b-257">В списке приложений hello выберите **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="3480b-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="3480b-259">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3480b-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3480b-261">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3480b-261">Click **Add** button.</span></span> <span data-ttu-id="3480b-262">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3480b-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3480b-264">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3480b-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3480b-265">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3480b-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3480b-266">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3480b-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3480b-267">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3480b-267">Testing single sign-on</span></span>

<span data-ttu-id="3480b-268">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="3480b-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3480b-269">При нажатии кнопки hello Sprinklr плитки в панели доступа hello, вы должны получить tooyour автоматически подписью в приложении Sprinklr Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3480b-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3480b-270">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3480b-270">Additional resources</span></span>

* [<span data-ttu-id="3480b-271">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3480b-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3480b-272">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3480b-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

