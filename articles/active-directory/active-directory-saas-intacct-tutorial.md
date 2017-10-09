---
title: "Учебник. Интеграция Azure Active Directory с Intacct | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="68256-103">Руководство. Интеграция Azure Active Directory с Intacct</span><span class="sxs-lookup"><span data-stu-id="68256-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="68256-104">В этом учебнике вы узнаете, как toointegrate Intacct с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68256-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68256-105">Интеграция Intacct с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="68256-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="68256-106">Можно управлять в Azure AD, имеющего доступ tooIntacct</span><span class="sxs-lookup"><span data-stu-id="68256-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="68256-107">Можно включить на пользователей tooautomatically get вошедшего tooIntacct (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="68256-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68256-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="68256-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="68256-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68256-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68256-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="68256-110">Prerequisites</span></span>

<span data-ttu-id="68256-111">tooconfigure интеграция Azure AD с Intacct требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="68256-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="68256-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="68256-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68256-113">подписка с поддержкой единого входа Intacct.</span><span class="sxs-lookup"><span data-stu-id="68256-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68256-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="68256-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68256-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="68256-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68256-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="68256-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68256-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68256-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68256-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="68256-118">Scenario description</span></span>
<span data-ttu-id="68256-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="68256-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68256-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="68256-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68256-121">Добавление Intacct из галереи hello</span><span class="sxs-lookup"><span data-stu-id="68256-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="68256-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="68256-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="68256-123">Добавление Intacct из галереи hello</span><span class="sxs-lookup"><span data-stu-id="68256-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="68256-124">tooconfigure hello интеграции Intacct в Azure AD, вы должны tooadd Intacct из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="68256-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="68256-125">**tooadd Intacct из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68256-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="68256-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="68256-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68256-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="68256-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="68256-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="68256-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="68256-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="68256-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="68256-133">Введите в поле поиска hello **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="68256-133">In hello search box, type **Intacct**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="68256-135">В панели результатов hello выберите **Intacct**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="68256-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68256-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="68256-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68256-138">В этом разделе описана настройка и проверка единого входа Azure AD в Intacct с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68256-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="68256-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Intacct является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68256-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="68256-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Intacct должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="68256-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="68256-141">В Intacct, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="68256-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="68256-142">tooconfigure и теста Azure AD единого входа с Intacct, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="68256-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="68256-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="68256-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="68256-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="68256-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68256-145">**[Создание тестового пользователя, прошедшего Intacct](#creating-an-intacct-test-user)**  -toohave аналог Саймон Britta в Intacct, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="68256-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="68256-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="68256-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68256-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68256-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68256-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="68256-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68256-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Intacct.</span><span class="sxs-lookup"><span data-stu-id="68256-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="68256-150">**tooconfigure Azure AD единого входа с Intacct, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68256-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="68256-151">В hello в hello портала Azure **Intacct** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="68256-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="68256-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="68256-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="68256-155">На hello **URL-адреса и домена Intacct** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="68256-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="68256-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="68256-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="68256-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="68256-158">This value is not real.</span></span> <span data-ttu-id="68256-159">Измените значение этого параметра hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="68256-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="68256-160">Обратитесь к [Intacct поддержки](https://us.intacct.com/support) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="68256-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="68256-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="68256-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="68256-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="68256-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="68256-165">На hello **конфигурации Intacct** щелкните **Настройка Intacct** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="68256-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="68256-166">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="68256-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="68256-168">В другом окне браузера Войдите на сайте компании tooyour Intacct с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="68256-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="68256-169">Нажмите кнопку hello **компании** , а затем щелкните **сведения о компании**.</span><span class="sxs-lookup"><span data-stu-id="68256-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="68256-170">![Организация](./media/active-directory-saas-intacct-tutorial/ic790037.png "Организация")</span><span class="sxs-lookup"><span data-stu-id="68256-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="68256-171">Нажмите кнопку hello **безопасности** , а затем щелкните **изменить**.</span><span class="sxs-lookup"><span data-stu-id="68256-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="68256-172">![Безопасность](./media/active-directory-saas-intacct-tutorial/ic790038.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="68256-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="68256-173">В hello **единого входа (SSO)** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="68256-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="68256-174">![Единый вход](./media/active-directory-saas-intacct-tutorial/ic790039.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="68256-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="68256-175">а.</span><span class="sxs-lookup"><span data-stu-id="68256-175">a.</span></span> <span data-ttu-id="68256-176">Установите флажок **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="68256-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="68256-177">b.</span><span class="sxs-lookup"><span data-stu-id="68256-177">b.</span></span> <span data-ttu-id="68256-178">Выберите для параметра **Identity provider type** (Тип поставщика удостоверений) значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="68256-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="68256-179">c.</span><span class="sxs-lookup"><span data-stu-id="68256-179">c.</span></span> <span data-ttu-id="68256-180">В **URL-адрес издателя** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="68256-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="68256-181">d.</span><span class="sxs-lookup"><span data-stu-id="68256-181">d.</span></span> <span data-ttu-id="68256-182">В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="68256-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="68256-183">д.</span><span class="sxs-lookup"><span data-stu-id="68256-183">e.</span></span> <span data-ttu-id="68256-184">Откройте ваш **base-64** закодированный сертификат в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат** поле.</span><span class="sxs-lookup"><span data-stu-id="68256-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="68256-185">f.</span><span class="sxs-lookup"><span data-stu-id="68256-185">f.</span></span> <span data-ttu-id="68256-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="68256-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="68256-187">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="68256-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="68256-188">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="68256-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="68256-189">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68256-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68256-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="68256-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="68256-191">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="68256-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="68256-193">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68256-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="68256-194">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="68256-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68256-196">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="68256-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68256-198">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="68256-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68256-200">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="68256-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68256-202">а.</span><span class="sxs-lookup"><span data-stu-id="68256-202">a.</span></span> <span data-ttu-id="68256-203">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68256-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68256-204">b.</span><span class="sxs-lookup"><span data-stu-id="68256-204">b.</span></span> <span data-ttu-id="68256-205">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="68256-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68256-206">c.</span><span class="sxs-lookup"><span data-stu-id="68256-206">c.</span></span> <span data-ttu-id="68256-207">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="68256-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="68256-208">d.</span><span class="sxs-lookup"><span data-stu-id="68256-208">d.</span></span> <span data-ttu-id="68256-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="68256-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="68256-210">Создание тестового пользователя Intacct</span><span class="sxs-lookup"><span data-stu-id="68256-210">Creating an Intacct test user</span></span>

<span data-ttu-id="68256-211">tooset пользователей Azure AD, они смогут войти в tooIntacct, их необходимо подготовить в Intacct.</span><span class="sxs-lookup"><span data-stu-id="68256-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="68256-212">Эта подготовка для Intacct выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="68256-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="68256-213">**tooprovision учетных записей пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68256-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="68256-214">Войдите в tooyour **Intacct** клиента.</span><span class="sxs-lookup"><span data-stu-id="68256-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="68256-215">Нажмите кнопку hello **компании** , а затем щелкните **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="68256-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="68256-216">![Пользователи](./media/active-directory-saas-intacct-tutorial/ic790041.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="68256-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="68256-217">Нажмите кнопку hello **добавить** вкладки.</span><span class="sxs-lookup"><span data-stu-id="68256-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="68256-218">![Добавление](./media/active-directory-saas-intacct-tutorial/ic790042.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="68256-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="68256-219">В hello **сведения о пользователе** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="68256-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="68256-220">![Сведения о пользователе](./media/active-directory-saas-intacct-tutorial/ic790043.png "Сведения о пользователе")</span><span class="sxs-lookup"><span data-stu-id="68256-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="68256-221">а.</span><span class="sxs-lookup"><span data-stu-id="68256-221">a.</span></span> <span data-ttu-id="68256-222">Введите hello **идентификатор пользователя**, hello **Фамилия**, **имя**, hello **адрес электронной почты**, hello **заголовка**, и hello **Phone** учетной записи Azure AD, которые должны tooprovision hello **сведения о пользователе** раздела.</span><span class="sxs-lookup"><span data-stu-id="68256-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="68256-223">b.</span><span class="sxs-lookup"><span data-stu-id="68256-223">b.</span></span> <span data-ttu-id="68256-224">Выберите hello **права доступа администратора** нужных tooprovision учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68256-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="68256-225">c.</span><span class="sxs-lookup"><span data-stu-id="68256-225">c.</span></span> <span data-ttu-id="68256-226">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="68256-226">Click **Save**.</span></span> <span data-ttu-id="68256-227">Hello владельцем учетной записи Azure AD получает сообщение электронной почты и следует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="68256-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="68256-228">tooprovision учетных записей пользователей Azure AD, можно использовать другие инструменты создания учетных записей Intacct или API-интерфейсы, предоставляемые Intacct.</span><span class="sxs-lookup"><span data-stu-id="68256-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="68256-229">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="68256-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="68256-230">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooIntacct доступа.</span><span class="sxs-lookup"><span data-stu-id="68256-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="68256-232">**tooassign tooIntacct Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="68256-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="68256-233">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="68256-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="68256-235">В списке приложений hello выберите **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="68256-235">In hello applications list, select **Intacct**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="68256-237">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="68256-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="68256-239">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="68256-239">Click **Add** button.</span></span> <span data-ttu-id="68256-240">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="68256-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="68256-242">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="68256-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="68256-243">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="68256-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68256-244">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="68256-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68256-245">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="68256-245">Testing single sign-on</span></span>

<span data-ttu-id="68256-246">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="68256-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="68256-247">Если щелкнуть плитку Intacct hello в hello панели доступа, вы должны автоматически входить в tooyour Intacct приложения.</span><span class="sxs-lookup"><span data-stu-id="68256-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68256-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="68256-248">Additional resources</span></span>

* [<span data-ttu-id="68256-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68256-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68256-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68256-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

