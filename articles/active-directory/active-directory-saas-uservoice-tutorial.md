---
title: "Руководство по интеграции Azure Active Directory с UserVoice | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="a6829-103">Руководство по интеграции Azure Active Directory с UserVoice</span><span class="sxs-lookup"><span data-stu-id="a6829-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="a6829-104">В этом учебнике вы узнаете, как toointegrate UserVoice с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6829-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6829-105">Интеграция UserVoice с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a6829-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a6829-106">Можно управлять в Azure AD, имеющего доступ tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="a6829-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="a6829-107">Можно включить на пользователей tooautomatically get вошедшего tooUserVoice (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6829-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a6829-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a6829-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a6829-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6829-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6829-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a6829-110">Prerequisites</span></span>

<span data-ttu-id="a6829-111">tooconfigure интеграция Azure AD с UserVoice требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a6829-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="a6829-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a6829-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6829-113">подписка UserVoice с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a6829-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6829-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a6829-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6829-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a6829-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6829-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a6829-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6829-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6829-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6829-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a6829-118">Scenario description</span></span>
<span data-ttu-id="a6829-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a6829-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6829-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a6829-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6829-121">Добавление UserVoice из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a6829-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="a6829-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6829-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="a6829-123">Добавление UserVoice из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a6829-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="a6829-124">tooconfigure hello интеграции UserVoice в Azure AD, вы должны tooadd UserVoice из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a6829-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a6829-125">**tooadd UserVoice из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a6829-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6829-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a6829-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="a6829-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a6829-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a6829-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a6829-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="a6829-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a6829-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="a6829-133">Введите в поле поиска hello **UserVoice**выберите **UserVoice** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a6829-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![UserVoice в списке результатов hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a6829-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6829-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a6829-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение UserVoice с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6829-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a6829-137">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в UserVoice — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6829-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="a6829-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в UserVoice должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a6829-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="a6829-139">В UserVoice, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a6829-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a6829-140">tooconfigure и теста Azure AD единого входа с UserVoice, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a6829-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a6829-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a6829-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a6829-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a6829-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6829-143">**[Создание тестового пользователя UserVoice](#create-a-uservoice-test-user)**  -toohave аналог Саймон Britta в UserVoice, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a6829-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6829-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a6829-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6829-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a6829-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a6829-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6829-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a6829-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении UserVoice.</span><span class="sxs-lookup"><span data-stu-id="a6829-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="a6829-148">**Azure AD tooconfigure единого входа с UserVoice, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a6829-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6829-149">В hello в hello портала Azure **UserVoice** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a6829-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="a6829-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a6829-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="a6829-153">На hello **URL-адреса и домена UserVoice** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a6829-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="a6829-155">а.</span><span class="sxs-lookup"><span data-stu-id="a6829-155">a.</span></span> <span data-ttu-id="a6829-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="a6829-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="a6829-157">b.</span><span class="sxs-lookup"><span data-stu-id="a6829-157">b.</span></span> <span data-ttu-id="a6829-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="a6829-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6829-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a6829-159">These values are not real.</span></span> <span data-ttu-id="a6829-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="a6829-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a6829-161">Обратитесь к [группа поддержки клиент UserVoice](https://www.uservoice.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="a6829-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="a6829-162">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="a6829-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="a6829-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a6829-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a6829-166">На hello **конфигурации UserVoice** щелкните **Настройка UserVoice** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a6829-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a6829-167">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a6829-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="a6829-169">В другом окне браузера Войдите на сайте компании UserVoice tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="a6829-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="a6829-170">Щелкните hello панели инструментов в верхней части hello **параметры**и выберите **веб-портале** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="a6829-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="a6829-171">![Раздел параметров на стороне приложения](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="a6829-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="a6829-172">На hello **веб-портале** hello на вкладке **проверки подлинности пользователя** щелкните **изменить** tooopen hello **изменение проверки подлинности пользователей** диалоговое окно страница.</span><span class="sxs-lookup"><span data-stu-id="a6829-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="a6829-173">![Вкладка веб-портала](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Веб-портал")</span><span class="sxs-lookup"><span data-stu-id="a6829-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="a6829-174">На hello **изменение проверки подлинности пользователей** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a6829-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a6829-175">![Изменение проверки подлинности пользователя](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Изменение проверки подлинности пользователя")</span><span class="sxs-lookup"><span data-stu-id="a6829-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="a6829-176">а.</span><span class="sxs-lookup"><span data-stu-id="a6829-176">a.</span></span> <span data-ttu-id="a6829-177">Выберите **Единый вход (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="a6829-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="a6829-178">b.</span><span class="sxs-lookup"><span data-stu-id="a6829-178">b.</span></span> <span data-ttu-id="a6829-179">Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **SSO удаленный вход** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a6829-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="a6829-180">c.</span><span class="sxs-lookup"><span data-stu-id="a6829-180">c.</span></span> <span data-ttu-id="a6829-181">Вставить hello **URL-адрес выхода** значение, которое было скопировано из hello портал Azure в hello **textbox удаленный единый выход SSO**.</span><span class="sxs-lookup"><span data-stu-id="a6829-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="a6829-182">d.</span><span class="sxs-lookup"><span data-stu-id="a6829-182">d.</span></span> <span data-ttu-id="a6829-183">Вставить hello **отпечаток** значение, которое было скопировано из портала Azure в **текущий отпечаток сертификата SHA1** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a6829-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="a6829-184">д.</span><span class="sxs-lookup"><span data-stu-id="a6829-184">e.</span></span> <span data-ttu-id="a6829-185">Нажмите кнопку **Сохранить параметры проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="a6829-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="a6829-186">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a6829-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a6829-187">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a6829-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a6829-188">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6829-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a6829-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6829-189">Create an Azure AD test user</span></span>

<span data-ttu-id="a6829-190">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a6829-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="a6829-192">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a6829-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6829-193">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a6829-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a6829-195">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a6829-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a6829-197">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a6829-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a6829-199">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a6829-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a6829-201">а.</span><span class="sxs-lookup"><span data-stu-id="a6829-201">a.</span></span> <span data-ttu-id="a6829-202">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6829-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6829-203">b.</span><span class="sxs-lookup"><span data-stu-id="a6829-203">b.</span></span> <span data-ttu-id="a6829-204">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a6829-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a6829-205">c.</span><span class="sxs-lookup"><span data-stu-id="a6829-205">c.</span></span> <span data-ttu-id="a6829-206">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="a6829-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a6829-207">d.</span><span class="sxs-lookup"><span data-stu-id="a6829-207">d.</span></span> <span data-ttu-id="a6829-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a6829-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="a6829-209">Создание тестового пользователя UserVoice</span><span class="sxs-lookup"><span data-stu-id="a6829-209">Create a UserVoice test user</span></span>

<span data-ttu-id="a6829-210">Пользователи toolog tooenable Azure AD в tooUserVoice, их необходимо подготовить в UserVoice.</span><span class="sxs-lookup"><span data-stu-id="a6829-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="a6829-211">В случае hello объекта UserVoice Подготовка осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="a6829-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="a6829-212">tooprovision учетной записи пользователя, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a6829-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="a6829-213">Войдите в tooyour **UserVoice** клиента.</span><span class="sxs-lookup"><span data-stu-id="a6829-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="a6829-214">Go слишком**параметры**.</span><span class="sxs-lookup"><span data-stu-id="a6829-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="a6829-215">![Параметры](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="a6829-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="a6829-216">Выберите пункт **Общие**.</span><span class="sxs-lookup"><span data-stu-id="a6829-216">Click **General**.</span></span>

4. <span data-ttu-id="a6829-217">Выберите пункт **Агенты и разрешения**.</span><span class="sxs-lookup"><span data-stu-id="a6829-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="a6829-218">![Агенты и разрешения](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Агенты и разрешения")</span><span class="sxs-lookup"><span data-stu-id="a6829-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="a6829-219">Нажмите кнопку **Добавить администраторов**.</span><span class="sxs-lookup"><span data-stu-id="a6829-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="a6829-220">![Добавление администраторов](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Добавление администраторов")</span><span class="sxs-lookup"><span data-stu-id="a6829-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="a6829-221">На hello **пригласить администраторов** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a6829-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="a6829-222">![Пригласить администраторов](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Пригласить администраторов")</span><span class="sxs-lookup"><span data-stu-id="a6829-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="a6829-223">а.</span><span class="sxs-lookup"><span data-stu-id="a6829-223">a.</span></span> <span data-ttu-id="a6829-224">В текстовом поле hello сообщения электронной почты, введите адрес электронной почты hello hello учетной записи tooprovision и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="a6829-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="a6829-225">b.</span><span class="sxs-lookup"><span data-stu-id="a6829-225">b.</span></span> <span data-ttu-id="a6829-226">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="a6829-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="a6829-227">Можно использовать любые другие UserVoice пользователя средства создания учетных записей или интерфейсы API, предоставляемые UserVoice tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="a6829-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a6829-228">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a6829-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a6829-229">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooUserVoice доступа.</span><span class="sxs-lookup"><span data-stu-id="a6829-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="a6829-231">**tooassign tooUserVoice Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a6829-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6829-232">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a6829-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a6829-234">В списке приложений hello выберите **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="a6829-234">In hello applications list, select **UserVoice**.</span></span>

    ![ссылка UserVoice Hello в списке приложений hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="a6829-236">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a6829-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="a6829-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a6829-238">Click **Add** button.</span></span> <span data-ttu-id="a6829-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a6829-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="a6829-241">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a6829-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a6829-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a6829-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6829-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a6829-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a6829-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a6829-244">Test single sign-on</span></span>

<span data-ttu-id="a6829-245">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a6829-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a6829-246">При нажатии кнопки hello UserVoice плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour UserVoice.</span><span class="sxs-lookup"><span data-stu-id="a6829-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="a6829-247">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a6829-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a6829-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a6829-248">Additional resources</span></span>

* [<span data-ttu-id="a6829-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6829-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6829-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6829-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

