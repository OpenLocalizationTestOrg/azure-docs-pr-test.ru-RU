---
title: "Руководство по интеграции Azure Active Directory с UserEcho | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="a79bb-103">Руководство. Интеграция Azure Active Directory с UserEcho</span><span class="sxs-lookup"><span data-stu-id="a79bb-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="a79bb-104">В этом учебнике вы узнаете, как toointegrate UserEcho с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a79bb-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a79bb-105">Интеграция с Azure AD UserEcho предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a79bb-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a79bb-106">Можно управлять в Azure AD, имеющего доступ tooUserEcho</span><span class="sxs-lookup"><span data-stu-id="a79bb-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="a79bb-107">Можно включить на пользователей tooautomatically get вошедшего tooUserEcho (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a79bb-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a79bb-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a79bb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a79bb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a79bb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a79bb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a79bb-110">Prerequisites</span></span>

<span data-ttu-id="a79bb-111">tooconfigure интеграция Azure AD с UserEcho требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a79bb-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="a79bb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a79bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a79bb-113">подписка UserEcho с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a79bb-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a79bb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a79bb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a79bb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a79bb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a79bb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a79bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a79bb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a79bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a79bb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a79bb-118">Scenario description</span></span>
<span data-ttu-id="a79bb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a79bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a79bb-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a79bb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a79bb-121">Добавление UserEcho из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a79bb-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="a79bb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a79bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="a79bb-123">Добавление UserEcho из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a79bb-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="a79bb-124">tooconfigure hello интеграции UserEcho в Azure AD, вы должны tooadd UserEcho из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a79bb-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a79bb-125">**tooadd UserEcho из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a79bb-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79bb-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a79bb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a79bb-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a79bb-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a79bb-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a79bb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a79bb-133">Введите в поле поиска hello **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-133">In hello search box, type **UserEcho**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="a79bb-135">В панели результатов hello выберите **UserEcho**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a79bb-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a79bb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a79bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a79bb-138">В этом разделе описана настройка и проверка единого входа Azure AD в UserEcho с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a79bb-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a79bb-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в UserEcho является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a79bb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="a79bb-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в UserEcho должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a79bb-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="a79bb-141">В UserEcho, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a79bb-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a79bb-142">tooconfigure и теста Azure AD единого входа с UserEcho, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a79bb-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a79bb-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a79bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a79bb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a79bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a79bb-145">**[Создание тестового пользователя UserEcho](#creating-a-userecho-test-user)**  -toohave аналог Саймон Britta в UserEcho, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a79bb-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a79bb-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a79bb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a79bb-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a79bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a79bb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a79bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a79bb-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении UserEcho.</span><span class="sxs-lookup"><span data-stu-id="a79bb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="a79bb-150">**tooconfigure Azure AD единого входа с UserEcho, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a79bb-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79bb-151">В hello в hello портала Azure **UserEcho** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a79bb-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a79bb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="a79bb-155">На hello **URL-адреса и домена UserEcho** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a79bb-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="a79bb-157">а.</span><span class="sxs-lookup"><span data-stu-id="a79bb-157">a.</span></span> <span data-ttu-id="a79bb-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="a79bb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="a79bb-159">b.</span><span class="sxs-lookup"><span data-stu-id="a79bb-159">b.</span></span> <span data-ttu-id="a79bb-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="a79bb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a79bb-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a79bb-161">These values are not real.</span></span> <span data-ttu-id="a79bb-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="a79bb-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a79bb-163">Обратитесь к [группа поддержки клиента UserEcho](https://feedback.userecho.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="a79bb-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="a79bb-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a79bb-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="a79bb-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a79bb-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a79bb-168">На hello **конфигурации UserEcho** щелкните **Настройка UserEcho** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a79bb-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a79bb-169">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a79bb-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="a79bb-171">В другом окне браузера Войдите на сайт компании UserEcho tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a79bb-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="a79bb-172">В верхней hello инструментов hello, щелкните меню hello tooexpand имя пользователя и нажмите кнопку **установки**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="a79bb-174">Щелкните **Integrations**(Интеграция).</span><span class="sxs-lookup"><span data-stu-id="a79bb-174">Click **Integrations**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="a79bb-176">Щелкните **Website** (Веб-сайт), а затем — **Single sign-on (SAML2)** (Единый вход (SAML2)).</span><span class="sxs-lookup"><span data-stu-id="a79bb-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="a79bb-178">На hello **единый вход (SAML)** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a79bb-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="a79bb-180">а.</span><span class="sxs-lookup"><span data-stu-id="a79bb-180">a.</span></span> <span data-ttu-id="a79bb-181">В поле **SAML-enabled** (Включить SAML) выберите **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="a79bb-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="a79bb-182">b.</span><span class="sxs-lookup"><span data-stu-id="a79bb-182">b.</span></span> <span data-ttu-id="a79bb-183">Вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure hello в hello **URL-адрес единого входа SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a79bb-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="a79bb-184">c.</span><span class="sxs-lookup"><span data-stu-id="a79bb-184">c.</span></span> <span data-ttu-id="a79bb-185">Вставить **URL-адрес выхода**, которого вы скопировали из портала Azure hello в hello **URL-адрес удаленного logoout** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a79bb-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="a79bb-186">d.</span><span class="sxs-lookup"><span data-stu-id="a79bb-186">d.</span></span> <span data-ttu-id="a79bb-187">Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a79bb-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="a79bb-188">д.</span><span class="sxs-lookup"><span data-stu-id="a79bb-188">e.</span></span> <span data-ttu-id="a79bb-189">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a79bb-190">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a79bb-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a79bb-191">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a79bb-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a79bb-192">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a79bb-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a79bb-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a79bb-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="a79bb-194">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a79bb-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a79bb-196">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a79bb-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79bb-197">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a79bb-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a79bb-199">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a79bb-201">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a79bb-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a79bb-203">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a79bb-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a79bb-205">а.</span><span class="sxs-lookup"><span data-stu-id="a79bb-205">a.</span></span> <span data-ttu-id="a79bb-206">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a79bb-207">b.</span><span class="sxs-lookup"><span data-stu-id="a79bb-207">b.</span></span> <span data-ttu-id="a79bb-208">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a79bb-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a79bb-209">c.</span><span class="sxs-lookup"><span data-stu-id="a79bb-209">c.</span></span> <span data-ttu-id="a79bb-210">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a79bb-211">d.</span><span class="sxs-lookup"><span data-stu-id="a79bb-211">d.</span></span> <span data-ttu-id="a79bb-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="a79bb-213">Создание тестового пользователя UserEcho</span><span class="sxs-lookup"><span data-stu-id="a79bb-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="a79bb-214">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в UserEcho.</span><span class="sxs-lookup"><span data-stu-id="a79bb-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="a79bb-215">**toocreate пользователя с именем Саймон Britta в UserEcho, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a79bb-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79bb-216">Корпоративный сайт UserEcho tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="a79bb-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="a79bb-217">В верхней hello инструментов hello, щелкните меню hello tooexpand имя пользователя и нажмите кнопку **установки**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="a79bb-219">Нажмите кнопку **пользователей**, tooexpand hello **пользователей** раздела.</span><span class="sxs-lookup"><span data-stu-id="a79bb-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="a79bb-221">Выберите раздел **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-221">Click **Users**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="a79bb-223">Щелкните **Invite a new user**(Пригласить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="a79bb-223">Click **Invite a new user**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="a79bb-225">На hello **пригласить нового пользователя** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a79bb-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="a79bb-227">а.</span><span class="sxs-lookup"><span data-stu-id="a79bb-227">a.</span></span> <span data-ttu-id="a79bb-228">В hello **имя** текстовое поле, имя типа hello пользователя как Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a79bb-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="a79bb-229">b.</span><span class="sxs-lookup"><span data-stu-id="a79bb-229">b.</span></span>  <span data-ttu-id="a79bb-230">В hello **электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a79bb-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="a79bb-231">c.</span><span class="sxs-lookup"><span data-stu-id="a79bb-231">c.</span></span> <span data-ttu-id="a79bb-232">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-232">Click **Invite**.</span></span>

<span data-ttu-id="a79bb-233">TooBritta, позволяющий ее toostart, с помощью UserEcho, отправляется приглашение.</span><span class="sxs-lookup"><span data-stu-id="a79bb-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a79bb-234">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a79bb-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a79bb-235">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooUserEcho доступа.</span><span class="sxs-lookup"><span data-stu-id="a79bb-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a79bb-237">**tooassign tooUserEcho Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a79bb-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79bb-238">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a79bb-240">В списке приложений hello выберите **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-240">In hello applications list, select **UserEcho**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="a79bb-242">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a79bb-244">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-244">Click **Add** button.</span></span> <span data-ttu-id="a79bb-245">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a79bb-247">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a79bb-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a79bb-248">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a79bb-249">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a79bb-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a79bb-250">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a79bb-250">Testing single sign-on</span></span>

<span data-ttu-id="a79bb-251">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="a79bb-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="a79bb-252">При нажатии кнопки hello UserEcho плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour UserEcho приложения.</span><span class="sxs-lookup"><span data-stu-id="a79bb-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a79bb-253">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a79bb-253">Additional resources</span></span>

* [<span data-ttu-id="a79bb-254">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a79bb-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a79bb-255">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a79bb-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

