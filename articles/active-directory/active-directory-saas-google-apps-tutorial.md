---
title: "Руководство по интеграции Azure Active Directory c Google Apps в Azure | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="845e0-103">Руководство по интеграции Azure Active Directory с Google Apps</span><span class="sxs-lookup"><span data-stu-id="845e0-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="845e0-104">В этом учебнике вы узнаете, как toointegrate Google Apps с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="845e0-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="845e0-105">Интеграция Google Apps с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="845e0-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="845e0-106">Можно управлять в Azure AD, имеющего доступ tooGoogle приложений</span><span class="sxs-lookup"><span data-stu-id="845e0-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="845e0-107">Можно включить на пользователей tooautomatically get вошедшего tooGoogle приложения (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="845e0-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="845e0-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="845e0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="845e0-109">Если требуется tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. раздел [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="845e0-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="845e0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="845e0-110">Prerequisites</span></span>

<span data-ttu-id="845e0-111">tooconfigure интеграция Azure AD с Google Apps, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="845e0-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="845e0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="845e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="845e0-113">подписка Google Apps с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="845e0-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="845e0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="845e0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="845e0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="845e0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="845e0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="845e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="845e0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="845e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="845e0-118">Видеоруководство</span><span class="sxs-lookup"><span data-stu-id="845e0-118">Video tutorial</span></span>
<span data-ttu-id="845e0-119">Как tooEnable Single Sign-On tooGoogle приложений в течение 2 минут:</span><span class="sxs-lookup"><span data-stu-id="845e0-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="845e0-120">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="845e0-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="845e0-121">**Вопрос. Поддерживают ли Chromebooks и другие устройства Chrome единый вход Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="845e0-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="845e0-122">Ответ Да, пользователи получают доступ toosign в их Chromebook устройства, используя свои учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="845e0-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="845e0-123">Сведения о том, почему учетные данные могут быть запрошены у пользователей дважды, см. в этой [статье о поддержке Google Apps](https://support.google.com/chrome/a/answer/6060880).</span><span class="sxs-lookup"><span data-stu-id="845e0-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="845e0-124">**Вопрос. Если включить единый вход, будет пользователей быть может toouse их toosign учетные данные Azure AD в любой продукт Google, например аудитории Google GMail, Google диске, YouTube и т. д.**</span><span class="sxs-lookup"><span data-stu-id="845e0-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="845e0-125">О: Да, в зависимости от [какие Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) выберите tooenable или отключить для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="845e0-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="845e0-126">**Вопрос. Можно ли включить единый вход только для подмножества пользователей Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="845e0-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="845e0-127">Ответ нет, Включение единого входа немедленно требуется все к Google Apps пользователей tooauthenticate с свои учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="845e0-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="845e0-128">Так как Google Apps не поддерживает наличие нескольких поставщиков удостоверений, hello поставщика удостоверений Google Apps среды может быть Azure AD или Google--, но не оба hello то же время.</span><span class="sxs-lookup"><span data-stu-id="845e0-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="845e0-129">**Вопрос. Если пользователь выполнил вход в Windows, являются они автоматически проверять подлинность приложений tooGoogle без будет выведено приглашение для ввода пароля?**</span><span class="sxs-lookup"><span data-stu-id="845e0-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="845e0-130">Ответ. Существует два варианта включения этого сценария.</span><span class="sxs-lookup"><span data-stu-id="845e0-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="845e0-131">Во-первых, пользователи могут входить в устройства Windows 10 посредством [присоединения к Azure Active Directory](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="845e0-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="845e0-132">Кроме того, пользователи могут войти в устройства Windows, присоединенных к домену tooan локальной Active Directory, который был включен для единого входа tooAzure AD через [служб федерации Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) развертывания.</span><span class="sxs-lookup"><span data-stu-id="845e0-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="845e0-133">Оба варианта требуют tooperform hello инструкциям hello, следуя учебника tooenable единый вход между Azure AD и Google Apps.</span><span class="sxs-lookup"><span data-stu-id="845e0-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="845e0-134">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="845e0-134">Scenario description</span></span>
<span data-ttu-id="845e0-135">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="845e0-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="845e0-136">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="845e0-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="845e0-137">Добавление Google Apps из галереи hello</span><span class="sxs-lookup"><span data-stu-id="845e0-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="845e0-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="845e0-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="845e0-139">Добавление Google Apps из галереи hello</span><span class="sxs-lookup"><span data-stu-id="845e0-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="845e0-140">tooconfigure hello интеграция Google Apps в Azure AD, вы должны tooadd Google Apps от hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="845e0-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="845e0-141">**tooadd Google Apps из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="845e0-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="845e0-142">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="845e0-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="845e0-144">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="845e0-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="845e0-145">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="845e0-145">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="845e0-147">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="845e0-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="845e0-149">Введите в поле поиска hello **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="845e0-149">In hello search box, type **Google Apps**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="845e0-151">В панели результатов hello выберите **Google Apps**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="845e0-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="845e0-153">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="845e0-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="845e0-154">В этом разделе описана настройка и проверка единого входа Azure AD в Google Apps с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="845e0-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="845e0-155">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Google Apps является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="845e0-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="845e0-156">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Google Apps должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="845e0-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="845e0-157">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Google Apps.</span><span class="sxs-lookup"><span data-stu-id="845e0-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="845e0-158">tooconfigure и теста Azure AD единого входа с Google Apps, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="845e0-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="845e0-159">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="845e0-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="845e0-160">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="845e0-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="845e0-161">**[Создание тестового пользователя Google Apps](#creating-a-google-apps-test-user)**  -toohave аналог Саймон Britta в Google Apps, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="845e0-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="845e0-162">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="845e0-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="845e0-163">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="845e0-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="845e0-164">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="845e0-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="845e0-165">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в приложение Google Apps.</span><span class="sxs-lookup"><span data-stu-id="845e0-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="845e0-166">**tooconfigure Azure AD единого входа с Google Apps, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="845e0-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="845e0-167">В hello в hello портала Azure **Google Apps** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="845e0-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="845e0-169">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="845e0-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="845e0-171">На hello **URL-адреса и домен Google Apps** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="845e0-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="845e0-173">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="845e0-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="845e0-174">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="845e0-174">This value is not real.</span></span> <span data-ttu-id="845e0-175">Обновите значение hello с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="845e0-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="845e0-176">обратитесь в службу hello [службу поддержки Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="845e0-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="845e0-177">На hello **сертификат подписи SAML** щелкните **сертификат** и сохраните hello сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="845e0-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="845e0-179">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="845e0-179">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="845e0-181">На hello **Google Apps конфигурации** щелкните **настроить Google Apps** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="845e0-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="845e0-182">Копировать hello **URL-адрес выхода, единого входа службы URL-адрес SAML и изменение пароля URL-адреса** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="845e0-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="845e0-184">Откройте новую вкладку в браузере и войдите с hello [консоли администрирования приложения Google](http://admin.google.com/) с помощью учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="845e0-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="845e0-185">Выберите пункт **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="845e0-185">Click **Security**.</span></span> <span data-ttu-id="845e0-186">Если вы не видите ссылку hello, они могут быть скрыты в hello **другие элементы** меню hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="845e0-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Выбор элемента "Безопасность"][10]

9. <span data-ttu-id="845e0-188">На hello **безопасности** щелкните **настройки единого входа (SSO).**</span><span class="sxs-lookup"><span data-stu-id="845e0-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Выбор элемента "Единый вход"][11]

10. <span data-ttu-id="845e0-190">Выполните следующие изменения конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="845e0-190">Perform hello following configuration changes:</span></span>
   
    ![Настройка единого входа][12]
   
    <span data-ttu-id="845e0-192">а.</span><span class="sxs-lookup"><span data-stu-id="845e0-192">a.</span></span> <span data-ttu-id="845e0-193">Выберите **Setup SSO with third party identity provider**(Настройка единого входа с помощью стороннего поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="845e0-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="845e0-194">b.</span><span class="sxs-lookup"><span data-stu-id="845e0-194">b.</span></span> <span data-ttu-id="845e0-195">В **входа в URL-адрес страницы** поля в Google Apps, вставьте значение hello **единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="845e0-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="845e0-196">c.</span><span class="sxs-lookup"><span data-stu-id="845e0-196">c.</span></span> <span data-ttu-id="845e0-197">В hello **URL-адрес страницы выхода** поля в Google Apps, вставьте значение hello **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="845e0-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="845e0-198">d.</span><span class="sxs-lookup"><span data-stu-id="845e0-198">d.</span></span> <span data-ttu-id="845e0-199">В hello **изменение пароля URL-адреса** поля в Google Apps, вставьте значение hello **изменение пароля URL-адреса**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="845e0-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="845e0-200">д.</span><span class="sxs-lookup"><span data-stu-id="845e0-200">e.</span></span> <span data-ttu-id="845e0-201">В Google Apps для hello **сертификат проверки**, отправить hello сертификат, загруженный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="845e0-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="845e0-202">f.</span><span class="sxs-lookup"><span data-stu-id="845e0-202">f.</span></span> <span data-ttu-id="845e0-203">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="845e0-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="845e0-204">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="845e0-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="845e0-205">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="845e0-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="845e0-206">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="845e0-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="845e0-207">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="845e0-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="845e0-208">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="845e0-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="845e0-210">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="845e0-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="845e0-211">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="845e0-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="845e0-213">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="845e0-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="845e0-215">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="845e0-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="845e0-217">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="845e0-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="845e0-219">а.</span><span class="sxs-lookup"><span data-stu-id="845e0-219">a.</span></span> <span data-ttu-id="845e0-220">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="845e0-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="845e0-221">b.</span><span class="sxs-lookup"><span data-stu-id="845e0-221">b.</span></span> <span data-ttu-id="845e0-222">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="845e0-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="845e0-223">c.</span><span class="sxs-lookup"><span data-stu-id="845e0-223">c.</span></span> <span data-ttu-id="845e0-224">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="845e0-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="845e0-225">d.</span><span class="sxs-lookup"><span data-stu-id="845e0-225">d.</span></span> <span data-ttu-id="845e0-226">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="845e0-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="845e0-227">Создание тестового пользователя Google Apps</span><span class="sxs-lookup"><span data-stu-id="845e0-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="845e0-228">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в программном обеспечении Google Apps.</span><span class="sxs-lookup"><span data-stu-id="845e0-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="845e0-229">Google Apps поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="845e0-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="845e0-230">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="845e0-230">There is no action for you in this section.</span></span> <span data-ttu-id="845e0-231">Если пользователь еще не существует в программном обеспечении Google Apps, новый создается при попытке tooaccess программного обеспечения Google Apps.</span><span class="sxs-lookup"><span data-stu-id="845e0-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="845e0-232">Если вам требуется toocreate пользователя вручную, обратитесь в службу hello [службу поддержки Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="845e0-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="845e0-233">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="845e0-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="845e0-234">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooGoogle приложений.</span><span class="sxs-lookup"><span data-stu-id="845e0-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="845e0-236">**tooassign Britta Simon tooGoogle приложений, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="845e0-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="845e0-237">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="845e0-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="845e0-239">В списке приложений hello выберите **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="845e0-239">In hello applications list, select **Google Apps**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="845e0-241">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="845e0-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="845e0-243">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="845e0-243">Click **Add** button.</span></span> <span data-ttu-id="845e0-244">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="845e0-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="845e0-246">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="845e0-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="845e0-247">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="845e0-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="845e0-248">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="845e0-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="845e0-249">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="845e0-249">Testing single sign-on</span></span>

<span data-ttu-id="845e0-250">В этом разделе Здравствуйте, единого входа параметры, откройте панель доступа по адресу tootest [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), затем войдите в hello тестовую учетную запись и нажмите кнопку **Google Apps** плитки в панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="845e0-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="845e0-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="845e0-251">Additional resources</span></span>

* [<span data-ttu-id="845e0-252">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="845e0-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="845e0-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="845e0-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="845e0-254">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="845e0-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png