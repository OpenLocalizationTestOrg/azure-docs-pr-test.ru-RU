---
title: "Руководство по интеграции Azure Active Directory с Bonusly | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="57dc4-103">Руководство. Интеграция Azure Active Directory с Bonusly</span><span class="sxs-lookup"><span data-stu-id="57dc4-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="57dc4-104">В этом учебнике вы узнаете, как toointegrate Bonusly с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57dc4-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57dc4-105">Интеграция с Azure AD Bonusly предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="57dc4-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="57dc4-106">Можно управлять в Azure AD, имеющего доступ tooBonusly</span><span class="sxs-lookup"><span data-stu-id="57dc4-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="57dc4-107">Можно включить на пользователей tooautomatically get вошедшего tooBonusly (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="57dc4-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57dc4-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="57dc4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="57dc4-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57dc4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57dc4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="57dc4-110">Prerequisites</span></span>

<span data-ttu-id="57dc4-111">tooconfigure интеграция Azure AD с Bonusly требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="57dc4-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="57dc4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="57dc4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57dc4-113">подписка Bonusly с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="57dc4-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57dc4-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="57dc4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57dc4-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="57dc4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57dc4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="57dc4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57dc4-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57dc4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57dc4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="57dc4-118">Scenario description</span></span>
<span data-ttu-id="57dc4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="57dc4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57dc4-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="57dc4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57dc4-121">Добавление Bonusly из галереи hello</span><span class="sxs-lookup"><span data-stu-id="57dc4-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="57dc4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="57dc4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="57dc4-123">Добавление Bonusly из галереи hello</span><span class="sxs-lookup"><span data-stu-id="57dc4-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="57dc4-124">tooconfigure hello интеграции Bonusly в Azure AD, вы должны tooadd Bonusly из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="57dc4-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="57dc4-125">**tooadd Bonusly из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57dc4-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="57dc4-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="57dc4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="57dc4-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="57dc4-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="57dc4-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="57dc4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="57dc4-133">Введите в поле поиска hello **Bonusly**выберите **Bonusly** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="57dc4-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Bonusly в списке результатов hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="57dc4-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="57dc4-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="57dc4-136">В этом разделе описана настройка и проверка единого входа Azure AD в Bonusly с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57dc4-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57dc4-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Bonusly является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57dc4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="57dc4-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Bonusly должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="57dc4-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="57dc4-139">В Bonusly, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="57dc4-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="57dc4-140">tooconfigure и теста Azure AD единого входа с Bonusly, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="57dc4-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="57dc4-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="57dc4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="57dc4-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="57dc4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57dc4-143">**[Создание Bonusly тестового пользователя](#create-a-bonusly-test-user) ** -toohave аналог Саймон Britta в Bonusly, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="57dc4-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="57dc4-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="57dc4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57dc4-145">**[Тестирование единого входа](#test-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="57dc4-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="57dc4-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="57dc4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="57dc4-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Bonusly.</span><span class="sxs-lookup"><span data-stu-id="57dc4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="57dc4-148">**tooconfigure Azure AD единого входа с Bonusly, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57dc4-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="57dc4-149">В hello в hello портала Azure **Bonusly** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="57dc4-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="57dc4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="57dc4-153">На hello **Bonusly доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="57dc4-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах для единого входа в приложение Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="57dc4-155">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="57dc4-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57dc4-156">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="57dc4-156">hello value is not real.</span></span> <span data-ttu-id="57dc4-157">Значение hello обновления с hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="57dc4-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="57dc4-158">Обратитесь к [Bonusly поддержки](https://Bonusly/contact) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="57dc4-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="57dc4-159">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение на основе сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="57dc4-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="57dc4-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="57dc4-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57dc4-163">На hello **Bonusly конфигурации** щелкните **Настройка Bonusly** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="57dc4-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="57dc4-164">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="57dc4-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="57dc4-166">В другом окне браузера войдите в tooyour **Bonusly** клиента.</span><span class="sxs-lookup"><span data-stu-id="57dc4-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="57dc4-167">Hello инструментов в верхней части hello, щелкните **параметры**, а затем выберите **интеграции и приложения**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="57dc4-168">![Социальный раздел Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="57dc4-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="57dc4-169">В разделе **Single Sign-On** (Единый вход) выберите **SAML**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="57dc4-170">На hello **SAML** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="57dc4-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="57dc4-171">![Диалоговое окно SAML в Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="57dc4-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="57dc4-172">а.</span><span class="sxs-lookup"><span data-stu-id="57dc4-172">a.</span></span> <span data-ttu-id="57dc4-173">В hello **URL-адрес назначения IdP SSO** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="57dc4-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="57dc4-174">b.</span><span class="sxs-lookup"><span data-stu-id="57dc4-174">b.</span></span> <span data-ttu-id="57dc4-175">В hello **издатель IdP** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="57dc4-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="57dc4-176">c.</span><span class="sxs-lookup"><span data-stu-id="57dc4-176">c.</span></span> <span data-ttu-id="57dc4-177">В hello **URL-адрес входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="57dc4-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="57dc4-178">d.</span><span class="sxs-lookup"><span data-stu-id="57dc4-178">d.</span></span> <span data-ttu-id="57dc4-179">Вставить **отпечаток** значение копируется из портала Azure hello **отпечаток сертификата** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="57dc4-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="57dc4-180">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="57dc4-181">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="57dc4-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="57dc4-182">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="57dc4-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="57dc4-183">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57dc4-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="57dc4-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="57dc4-184">Create an Azure AD test user</span></span>
<span data-ttu-id="57dc4-185">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="57dc4-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="57dc4-187">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57dc4-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="57dc4-188">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="57dc4-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57dc4-190">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57dc4-192">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="57dc4-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57dc4-194">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="57dc4-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57dc4-196">а.</span><span class="sxs-lookup"><span data-stu-id="57dc4-196">a.</span></span> <span data-ttu-id="57dc4-197">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57dc4-198">b.</span><span class="sxs-lookup"><span data-stu-id="57dc4-198">b.</span></span> <span data-ttu-id="57dc4-199">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57dc4-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57dc4-200">c.</span><span class="sxs-lookup"><span data-stu-id="57dc4-200">c.</span></span> <span data-ttu-id="57dc4-201">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="57dc4-202">d.</span><span class="sxs-lookup"><span data-stu-id="57dc4-202">d.</span></span> <span data-ttu-id="57dc4-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="57dc4-204">Создание тестового пользователя приложения Bonusly</span><span class="sxs-lookup"><span data-stu-id="57dc4-204">Create a Bonusly test user</span></span>

<span data-ttu-id="57dc4-205">В порядке tooenable toolog пользователей Azure AD в tooBonusly их необходимо подготовить в Bonusly.</span><span class="sxs-lookup"><span data-stu-id="57dc4-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="57dc4-206">В случае Bonusly hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="57dc4-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="57dc4-207">Можно использовать любые другие Bonusly пользователя средства создания учетных записей или интерфейсы API, предоставляемые Bonusly tooprovision AAD учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="57dc4-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="57dc4-208">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57dc4-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="57dc4-209">В окне браузера войдите в tooyour Bonusly клиента.</span><span class="sxs-lookup"><span data-stu-id="57dc4-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="57dc4-210">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="57dc4-211">![Параметры](./media/active-directory-saas-bonus-tutorial/ic781041.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="57dc4-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="57dc4-212">Нажмите кнопку hello **пользователи и премии** вкладки.</span><span class="sxs-lookup"><span data-stu-id="57dc4-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="57dc4-213">![Пользователи и бонусы](./media/active-directory-saas-bonus-tutorial/ic781042.png "Пользователи и бонусы")</span><span class="sxs-lookup"><span data-stu-id="57dc4-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="57dc4-214">Выберите **Manage Users**(Управление пользователями).</span><span class="sxs-lookup"><span data-stu-id="57dc4-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="57dc4-215">![Управление пользователями](./media/active-directory-saas-bonus-tutorial/ic781043.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="57dc4-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="57dc4-216">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="57dc4-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="57dc4-217">![Добавление пользователя](./media/active-directory-saas-bonus-tutorial/ic781044.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="57dc4-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="57dc4-218">На hello **добавить пользователя** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="57dc4-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="57dc4-219">![Добавление пользователя](./media/active-directory-saas-bonus-tutorial/ic781045.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="57dc4-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="57dc4-220">а.</span><span class="sxs-lookup"><span data-stu-id="57dc4-220">a.</span></span> <span data-ttu-id="57dc4-221">В hello **имя** текстовом поле введите имя пользователя, такие как hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="57dc4-222">b.</span><span class="sxs-lookup"><span data-stu-id="57dc4-222">b.</span></span> <span data-ttu-id="57dc4-223">В hello **Фамилия** текстовом поле введите фамилию пользователя как hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="57dc4-224">c.</span><span class="sxs-lookup"><span data-stu-id="57dc4-224">c.</span></span> <span data-ttu-id="57dc4-225">В hello **электронной почты** текстовом поле введите адрес электронной почты hello пользователя как ** brittasimon@contoso.com **.</span><span class="sxs-lookup"><span data-stu-id="57dc4-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="57dc4-226">d.</span><span class="sxs-lookup"><span data-stu-id="57dc4-226">d.</span></span> <span data-ttu-id="57dc4-227">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="57dc4-228">Владелец учетной записи Azure AD Hello получает сообщение электронной почты, который включает учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="57dc4-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="57dc4-229">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="57dc4-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="57dc4-230">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBonusly доступа.</span><span class="sxs-lookup"><span data-stu-id="57dc4-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="57dc4-232">**tooassign tooBonusly Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57dc4-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="57dc4-233">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="57dc4-235">В списке приложений hello выберите **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-235">In hello applications list, select **Bonusly**.</span></span>

    ![Hello Bonusly ссылку в списке приложений hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="57dc4-237">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="57dc4-239">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-239">Click **Add** button.</span></span> <span data-ttu-id="57dc4-240">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="57dc4-242">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="57dc4-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="57dc4-243">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57dc4-244">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="57dc4-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="57dc4-245">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="57dc4-245">Test single sign-on</span></span>

<span data-ttu-id="57dc4-246">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="57dc4-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="57dc4-247">При нажатии кнопки Bonusly плитки hello в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour Bonusly приложения.</span><span class="sxs-lookup"><span data-stu-id="57dc4-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57dc4-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="57dc4-248">Additional resources</span></span>

* [<span data-ttu-id="57dc4-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57dc4-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57dc4-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57dc4-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

