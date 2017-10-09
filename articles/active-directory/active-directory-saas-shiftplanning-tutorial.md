---
title: "Учебник. Интеграция Azure Active Directory с Humanity | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и человечества."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="9cd77-103">Учебник. Интеграция Azure Active Directory с Humanity</span><span class="sxs-lookup"><span data-stu-id="9cd77-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="9cd77-104">В этом учебнике вы узнаете, как toointegrate человечества с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9cd77-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cd77-105">Интеграция с Azure AD человечества предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9cd77-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9cd77-106">Можно управлять в Azure AD, имеющего доступ tooHumanity</span><span class="sxs-lookup"><span data-stu-id="9cd77-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="9cd77-107">Можно включить на пользователей tooautomatically get вошедшего tooHumanity (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cd77-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cd77-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9cd77-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9cd77-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cd77-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cd77-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9cd77-110">Prerequisites</span></span>

<span data-ttu-id="9cd77-111">tooconfigure интеграция Azure AD с человечества требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9cd77-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="9cd77-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9cd77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cd77-113">подписка Humanity с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9cd77-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cd77-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9cd77-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cd77-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="9cd77-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cd77-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9cd77-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cd77-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cd77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cd77-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9cd77-118">Scenario description</span></span>
<span data-ttu-id="9cd77-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9cd77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cd77-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="9cd77-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cd77-121">Добавление человечества из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9cd77-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="9cd77-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cd77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="9cd77-123">Добавление человечества из галереи hello</span><span class="sxs-lookup"><span data-stu-id="9cd77-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="9cd77-124">интеграции hello tooconfigure человечества в Azure AD, вы должны tooadd человечества из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9cd77-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9cd77-125">**tooadd человечества из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9cd77-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cd77-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9cd77-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cd77-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9cd77-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9cd77-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9cd77-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9cd77-133">Введите в поле поиска hello **человечества**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-133">In hello search box, type **Humanity**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="9cd77-135">В панели результатов hello, выберите **сознания**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9cd77-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cd77-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cd77-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cd77-138">В этом разделе описана настройка и проверка единого входа Azure AD в Humanity с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cd77-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9cd77-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в человечества является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cd77-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="9cd77-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в человечества должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="9cd77-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="9cd77-141">В человечества, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="9cd77-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9cd77-142">tooconfigure и теста Azure AD единого входа с человечества, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9cd77-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9cd77-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="9cd77-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9cd77-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9cd77-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cd77-145">**[Создание тестового пользователя человечества](#creating-a-humanity-test-user)**  -toohave аналог Саймон Britta в человечества, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="9cd77-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cd77-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="9cd77-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cd77-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9cd77-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cd77-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cd77-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cd77-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении человечества.</span><span class="sxs-lookup"><span data-stu-id="9cd77-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="9cd77-150">**tooconfigure Azure AD единого входа с человечества, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9cd77-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cd77-151">В hello в hello портала Azure **сознания** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9cd77-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="9cd77-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="9cd77-155">На hello **URL-адреса и домена человечества** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9cd77-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="9cd77-157">а.</span><span class="sxs-lookup"><span data-stu-id="9cd77-157">a.</span></span> <span data-ttu-id="9cd77-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="9cd77-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="9cd77-159">b.</span><span class="sxs-lookup"><span data-stu-id="9cd77-159">b.</span></span> <span data-ttu-id="9cd77-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="9cd77-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9cd77-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9cd77-161">These values are not real.</span></span> <span data-ttu-id="9cd77-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9cd77-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9cd77-163">Обратитесь к [группа поддержки клиента человечества](https://www.humanity.com/support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="9cd77-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="9cd77-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="9cd77-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="9cd77-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9cd77-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cd77-168">На hello **конфигурации человечества** щелкните **Настройка человечества** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="9cd77-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9cd77-169">Копировать hello **SAML единого входа URL-адрес службы и URL-адрес выхода** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="9cd77-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="9cd77-171">В другом окне браузера, войдите в tooyour **человечества** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9cd77-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="9cd77-172">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="9cd77-173">![Администратор](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="9cd77-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="9cd77-174">В разделе **Integration** (Интеграция) щелкните **Single Sign-On** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="9cd77-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="9cd77-175">![Единый вход](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="9cd77-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="9cd77-176">В hello **Single Sign-On** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9cd77-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9cd77-177">![Единый вход](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="9cd77-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="9cd77-178">а.</span><span class="sxs-lookup"><span data-stu-id="9cd77-178">a.</span></span> <span data-ttu-id="9cd77-179">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="9cd77-180">b.</span><span class="sxs-lookup"><span data-stu-id="9cd77-180">b.</span></span> <span data-ttu-id="9cd77-181">Установите флажок **Allow Password Login** (Разрешить вход с паролем).</span><span class="sxs-lookup"><span data-stu-id="9cd77-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="9cd77-182">c.</span><span class="sxs-lookup"><span data-stu-id="9cd77-182">c.</span></span> <span data-ttu-id="9cd77-183">Вставить hello **SAML единого входа URL-адрес службы** значение в hello **URL-адрес издателя SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9cd77-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="9cd77-184">d.</span><span class="sxs-lookup"><span data-stu-id="9cd77-184">d.</span></span> <span data-ttu-id="9cd77-185">Вставить hello **URL-адрес выхода** значение в hello **URL-адрес удаленного выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9cd77-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="9cd77-186">д.</span><span class="sxs-lookup"><span data-stu-id="9cd77-186">e.</span></span> <span data-ttu-id="9cd77-187">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9cd77-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="9cd77-188">Нажмите кнопку **Сохранить параметры**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="9cd77-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="9cd77-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9cd77-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="9cd77-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9cd77-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cd77-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cd77-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cd77-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cd77-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd77-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9cd77-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9cd77-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cd77-196">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9cd77-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cd77-198">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cd77-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="9cd77-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cd77-202">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9cd77-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cd77-204">а.</span><span class="sxs-lookup"><span data-stu-id="9cd77-204">a.</span></span> <span data-ttu-id="9cd77-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cd77-206">b.</span><span class="sxs-lookup"><span data-stu-id="9cd77-206">b.</span></span> <span data-ttu-id="9cd77-207">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9cd77-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cd77-208">c.</span><span class="sxs-lookup"><span data-stu-id="9cd77-208">c.</span></span> <span data-ttu-id="9cd77-209">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9cd77-210">d.</span><span class="sxs-lookup"><span data-stu-id="9cd77-210">d.</span></span> <span data-ttu-id="9cd77-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="9cd77-212">Создание тестового пользователя Humanity</span><span class="sxs-lookup"><span data-stu-id="9cd77-212">Creating a Humanity test user</span></span>

<span data-ttu-id="9cd77-213">В порядке tooenable toolog пользователей Azure AD в tooHumanity их необходимо подготовить в человечества.</span><span class="sxs-lookup"><span data-stu-id="9cd77-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="9cd77-214">В случае hello сознания Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9cd77-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="9cd77-215">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9cd77-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cd77-216">Войдите в tooyour **человечества** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9cd77-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="9cd77-217">Щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="9cd77-218">![Администратор](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="9cd77-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="9cd77-219">Щелкните **Персонал**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="9cd77-220">![Персонал](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Персонал")</span><span class="sxs-lookup"><span data-stu-id="9cd77-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="9cd77-221">В разделе **Действия** щелкните **Добавление сотрудников**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="9cd77-222">![Добавить сотрудников](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Добавить сотрудников")</span><span class="sxs-lookup"><span data-stu-id="9cd77-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="9cd77-223">В hello **добавить сотрудника** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9cd77-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9cd77-224">![Сохранить сотрудников](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Сохранить сотрудников")</span><span class="sxs-lookup"><span data-stu-id="9cd77-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="9cd77-225">а.</span><span class="sxs-lookup"><span data-stu-id="9cd77-225">a.</span></span> <span data-ttu-id="9cd77-226">Тип hello **имя**, **Фамилия**, и **электронной почты** из текстовых полей, связанных с действительной учетной записи AAD, которые должны tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="9cd77-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="9cd77-227">b.</span><span class="sxs-lookup"><span data-stu-id="9cd77-227">b.</span></span> <span data-ttu-id="9cd77-228">Щелкните **Сохранить сотрудников**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="9cd77-229">Можно использовать любые другие человечества пользователя средства создания учетных записей или интерфейсы API, предоставляемые человечества tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="9cd77-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9cd77-230">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="9cd77-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9cd77-231">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHumanity доступа.</span><span class="sxs-lookup"><span data-stu-id="9cd77-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9cd77-233">**tooassign tooHumanity Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9cd77-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cd77-234">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9cd77-236">В списке приложений hello выберите **человечества**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-236">In hello applications list, select **Humanity**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="9cd77-238">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9cd77-240">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-240">Click **Add** button.</span></span> <span data-ttu-id="9cd77-241">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9cd77-243">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="9cd77-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9cd77-244">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cd77-245">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cd77-246">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9cd77-246">Testing single sign-on</span></span>

<span data-ttu-id="9cd77-247">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="9cd77-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9cd77-248">При выборе плитки человечества hello в hello панели доступа, следует получать автоматически вошедшего tooyour человечества приложения.</span><span class="sxs-lookup"><span data-stu-id="9cd77-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="9cd77-249">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9cd77-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cd77-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9cd77-250">Additional resources</span></span>

* [<span data-ttu-id="9cd77-251">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cd77-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cd77-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cd77-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

