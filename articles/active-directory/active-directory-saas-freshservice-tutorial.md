---
title: "Учебник. Интеграция Azure Active Directory с Freshservice | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="fc276-103">Учебник. Интеграция Azure Active Directory с FreshService</span><span class="sxs-lookup"><span data-stu-id="fc276-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="fc276-104">В этом учебнике вы узнаете, как toointegrate Freshservice с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fc276-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc276-105">Интеграция Freshservice с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="fc276-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fc276-106">Можно управлять в Azure AD, имеющего доступ tooFreshservice</span><span class="sxs-lookup"><span data-stu-id="fc276-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="fc276-107">Можно включить на пользователей tooautomatically get вошедшего tooFreshservice (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc276-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fc276-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="fc276-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fc276-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fc276-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc276-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fc276-110">Prerequisites</span></span>

<span data-ttu-id="fc276-111">tooconfigure интеграция Azure AD с Freshservice требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="fc276-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="fc276-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="fc276-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc276-113">подписка Freshservice с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="fc276-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fc276-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="fc276-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fc276-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="fc276-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc276-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="fc276-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc276-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc276-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fc276-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="fc276-118">Scenario description</span></span>
<span data-ttu-id="fc276-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="fc276-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc276-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="fc276-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc276-121">Добавление Freshservice из галереи hello</span><span class="sxs-lookup"><span data-stu-id="fc276-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="fc276-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc276-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="fc276-123">Добавление Freshservice из галереи hello</span><span class="sxs-lookup"><span data-stu-id="fc276-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="fc276-124">tooconfigure hello интеграции Freshservice в Azure AD, вы должны tooadd Freshservice из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="fc276-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fc276-125">**tooadd Freshservice из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fc276-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc276-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="fc276-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fc276-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="fc276-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fc276-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fc276-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="fc276-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="fc276-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="fc276-133">Введите в поле поиска hello **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="fc276-133">In hello search box, type **Freshservice**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="fc276-135">В панели результатов hello выберите **Freshservice**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fc276-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fc276-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc276-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fc276-138">В этом разделе описана настройка и проверка единого входа Azure AD во Freshservice с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc276-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fc276-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Freshservice является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc276-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="fc276-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Freshservice должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="fc276-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="fc276-141">В Freshservice, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="fc276-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fc276-142">tooconfigure и теста Azure AD единого входа с Freshservice, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="fc276-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fc276-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="fc276-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fc276-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="fc276-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc276-145">**[Создание тестового пользователя Freshservice](#creating-a-freshservice-test-user)**  -toohave аналог Саймон Britta в Freshservice, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="fc276-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc276-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="fc276-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc276-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fc276-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fc276-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc276-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fc276-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в ваше приложение Freshservice.</span><span class="sxs-lookup"><span data-stu-id="fc276-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="fc276-150">**tooconfigure Azure AD единого входа с Freshservice, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fc276-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc276-151">В hello в hello портала Azure **Freshservice** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="fc276-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="fc276-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="fc276-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="fc276-155">На hello **URL-адреса и домена Freshservice** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fc276-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="fc276-157">а.</span><span class="sxs-lookup"><span data-stu-id="fc276-157">a.</span></span> <span data-ttu-id="fc276-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="fc276-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="fc276-159">b.</span><span class="sxs-lookup"><span data-stu-id="fc276-159">b.</span></span> <span data-ttu-id="fc276-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="fc276-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fc276-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="fc276-161">These values are not real.</span></span> <span data-ttu-id="fc276-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="fc276-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fc276-163">Обратитесь к [группа поддержки клиента Freshservice](https://support.freshservice.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="fc276-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="fc276-164">На hello **сертификат подписи SAML** скопируйте **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="fc276-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="fc276-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="fc276-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fc276-168">На hello **конфигурации Freshservice** щелкните **Настройка Freshservice** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="fc276-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fc276-169">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="fc276-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="fc276-171">В другом окне браузера войти в корпоративный сайт Freshservice tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="fc276-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="fc276-172">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="fc276-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="fc276-173">![Администратор](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="fc276-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="fc276-174">В hello **портал клиента**, нажмите кнопку **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="fc276-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="fc276-175">![Безопасность](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="fc276-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="fc276-176">В hello **безопасности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fc276-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fc276-177">![Единый вход](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="fc276-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="fc276-178">а.</span><span class="sxs-lookup"><span data-stu-id="fc276-178">a.</span></span> <span data-ttu-id="fc276-179">Включите **единый вход**.</span><span class="sxs-lookup"><span data-stu-id="fc276-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="fc276-180">b.</span><span class="sxs-lookup"><span data-stu-id="fc276-180">b.</span></span> <span data-ttu-id="fc276-181">Выберите **Единый вход SAML**.</span><span class="sxs-lookup"><span data-stu-id="fc276-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="fc276-182">c.</span><span class="sxs-lookup"><span data-stu-id="fc276-182">c.</span></span> <span data-ttu-id="fc276-183">В hello **URL-адрес входа SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fc276-184">d.</span><span class="sxs-lookup"><span data-stu-id="fc276-184">d.</span></span> <span data-ttu-id="fc276-185">В hello **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fc276-186">д.</span><span class="sxs-lookup"><span data-stu-id="fc276-186">e.</span></span> <span data-ttu-id="fc276-187">В **отпечаток сертификата безопасности** текстовое поле, вставить hello **ОТПЕЧАТОК** значение сертификата, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fc276-188">f.</span><span class="sxs-lookup"><span data-stu-id="fc276-188">f.</span></span> <span data-ttu-id="fc276-189">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="fc276-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="fc276-190">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="fc276-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fc276-191">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="fc276-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fc276-192">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fc276-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fc276-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc276-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="fc276-194">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="fc276-196">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fc276-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc276-197">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="fc276-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fc276-199">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="fc276-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fc276-201">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="fc276-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fc276-203">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fc276-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fc276-205">а.</span><span class="sxs-lookup"><span data-stu-id="fc276-205">a.</span></span> <span data-ttu-id="fc276-206">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fc276-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fc276-207">b.</span><span class="sxs-lookup"><span data-stu-id="fc276-207">b.</span></span> <span data-ttu-id="fc276-208">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fc276-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fc276-209">c.</span><span class="sxs-lookup"><span data-stu-id="fc276-209">c.</span></span> <span data-ttu-id="fc276-210">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="fc276-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fc276-211">d.</span><span class="sxs-lookup"><span data-stu-id="fc276-211">d.</span></span> <span data-ttu-id="fc276-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fc276-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="fc276-213">Создание тестового пользователя Freshservice</span><span class="sxs-lookup"><span data-stu-id="fc276-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="fc276-214">Пользователи toolog tooenable Azure AD в tooFreshService, их необходимо подготовить во FreshService.</span><span class="sxs-lookup"><span data-stu-id="fc276-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="fc276-215">В случае FreshService hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="fc276-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="fc276-216">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fc276-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc276-217">Войдите в tooyour **FreshService** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="fc276-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="fc276-218">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="fc276-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="fc276-219">![Администратор](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="fc276-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="fc276-220">В hello **Управление пользователями** щелкните **инициаторы запроса**.</span><span class="sxs-lookup"><span data-stu-id="fc276-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="fc276-221">![Инициатор запроса](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Инициатор запроса")</span><span class="sxs-lookup"><span data-stu-id="fc276-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="fc276-222">Нажмите **Новый инициатор запроса**.</span><span class="sxs-lookup"><span data-stu-id="fc276-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="fc276-223">![Создание инициаторов запроса](./media/active-directory-saas-freshservice-tutorial/ic790819.png "Создание инициаторов запроса")</span><span class="sxs-lookup"><span data-stu-id="fc276-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="fc276-224">В hello **новый инициатор запроса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fc276-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fc276-225">![Создание инициатора запроса](./media/active-directory-saas-freshservice-tutorial/ic790820.png "Создание инициатора запроса")</span><span class="sxs-lookup"><span data-stu-id="fc276-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="fc276-226">а.</span><span class="sxs-lookup"><span data-stu-id="fc276-226">a.</span></span> <span data-ttu-id="fc276-227">Введите hello **имя** и **электронной почты** атрибуты действительной учетной записи Azure Active Directory, которые должны tooprovision hello связаны текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="fc276-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="fc276-228">b.</span><span class="sxs-lookup"><span data-stu-id="fc276-228">b.</span></span> <span data-ttu-id="fc276-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fc276-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="fc276-230">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной</span><span class="sxs-lookup"><span data-stu-id="fc276-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="fc276-231">Можно использовать любые другие FreshService пользователя средства создания учетных записей или интерфейсы API, предоставляемые FreshService tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="fc276-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Назначение пользователя][200] 

<span data-ttu-id="fc276-233">**tooassign tooFreshservice Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="fc276-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc276-234">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fc276-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="fc276-236">В списке приложений hello выберите **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="fc276-236">In hello applications list, select **Freshservice**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="fc276-238">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="fc276-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="fc276-240">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fc276-240">Click **Add** button.</span></span> <span data-ttu-id="fc276-241">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fc276-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="fc276-243">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="fc276-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fc276-244">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fc276-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc276-245">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="fc276-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fc276-246">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="fc276-246">Testing single sign-on</span></span>

<span data-ttu-id="fc276-247">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="fc276-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fc276-248">При нажатии кнопки hello Freshservice плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Freshservice приложения.</span><span class="sxs-lookup"><span data-stu-id="fc276-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc276-249">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fc276-249">Additional resources</span></span>

* [<span data-ttu-id="fc276-250">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc276-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc276-251">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fc276-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

