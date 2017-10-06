---
title: "Руководство по интеграции Azure Active Directory с Asana | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="71036-103">Руководство. Интеграция Azure Active Directory с Asana</span><span class="sxs-lookup"><span data-stu-id="71036-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="71036-104">В этом учебнике вы узнаете, как toointegrate Asana с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71036-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71036-105">Интеграция с Azure AD Asana предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="71036-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="71036-106">Можно управлять в Azure AD, имеющего доступ tooAsana</span><span class="sxs-lookup"><span data-stu-id="71036-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="71036-107">Можно включить на пользователей tooautomatically get вошедшего tooAsana (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="71036-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71036-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="71036-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="71036-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71036-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71036-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="71036-110">Prerequisites</span></span>

<span data-ttu-id="71036-111">tooconfigure интеграция Azure AD с Asana требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="71036-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="71036-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="71036-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71036-113">подписка Asana с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="71036-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71036-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="71036-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71036-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="71036-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71036-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="71036-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71036-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71036-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71036-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="71036-118">Scenario description</span></span>
<span data-ttu-id="71036-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="71036-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71036-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="71036-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71036-121">Добавление Asana из галереи hello</span><span class="sxs-lookup"><span data-stu-id="71036-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="71036-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="71036-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="71036-123">Добавление Asana из галереи hello</span><span class="sxs-lookup"><span data-stu-id="71036-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="71036-124">tooconfigure hello интеграции Asana в Azure AD, вы должны tooadd Asana из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="71036-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="71036-125">**tooadd Asana из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="71036-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="71036-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="71036-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="71036-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="71036-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="71036-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="71036-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="71036-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="71036-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="71036-133">Введите в поле поиска hello **Asana**выберите **Asana** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="71036-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="71036-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="71036-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="71036-136">В этом разделе описана настройка и проверка единого входа Azure AD в Asana с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71036-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="71036-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Asana является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71036-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="71036-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Asana должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="71036-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="71036-139">В Asana, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="71036-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="71036-140">tooconfigure и теста Azure AD единого входа с Asana, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="71036-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="71036-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="71036-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="71036-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="71036-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71036-143">**[Создание тестового пользователя, прошедшего Asana](#create-an-asana-test-user) ** -toohave аналог Саймон Britta в Asana, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="71036-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="71036-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="71036-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71036-145">**[Тестирование единого входа](#test-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="71036-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="71036-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="71036-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="71036-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Asana.</span><span class="sxs-lookup"><span data-stu-id="71036-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="71036-148">**tooconfigure Azure AD единого входа с Asana, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="71036-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="71036-149">В hello в hello портала Azure **Asana** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="71036-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="71036-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="71036-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="71036-153">На hello **URL-адреса и домена Asana** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="71036-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="71036-155">а.</span><span class="sxs-lookup"><span data-stu-id="71036-155">a.</span></span> <span data-ttu-id="71036-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="71036-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="71036-157">b.</span><span class="sxs-lookup"><span data-stu-id="71036-157">b.</span></span> <span data-ttu-id="71036-158">В hello **идентификатор** текстовое поле, значение типа:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="71036-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="71036-159">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="71036-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="71036-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="71036-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="71036-163">На hello **конфигурации Asana** щелкните **Настройка Asana** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="71036-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="71036-164">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="71036-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="71036-166">В другом окне браузера, tooyour входа Asana приложения.</span><span class="sxs-lookup"><span data-stu-id="71036-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="71036-167">tooconfigure единого входа в Asana параметров рабочей области доступа hello, щелкнув имя рабочей области hello в hello правом верхнем углу экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="71036-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="71036-168">Щелкните элемент **\<your workspace name\> Settings** (Параметры <имя_рабочей_области>).</span><span class="sxs-lookup"><span data-stu-id="71036-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Параметры единого входа Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="71036-170">На hello **параметры организации** окно, нажмите кнопку **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="71036-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="71036-171">Нажмите кнопку **членов необходимо войти в систему через SAML** Настройка единого входа tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="71036-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="71036-172">Hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="71036-172">hello perform hello following steps:</span></span>
   
    ![Настройка параметров единого входа организации](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="71036-174">а.</span><span class="sxs-lookup"><span data-stu-id="71036-174">a.</span></span> <span data-ttu-id="71036-175">В hello **входа в URL-адрес страницы** текстовое поле, вставить hello **SAML единого входа URL-адрес службы**.</span><span class="sxs-lookup"><span data-stu-id="71036-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="71036-176">b.</span><span class="sxs-lookup"><span data-stu-id="71036-176">b.</span></span> <span data-ttu-id="71036-177">Щелкните правой кнопкой мыши сертификат hello загружен с портала Azure, а затем откройте файл сертификата hello, с помощью блокнота или предпочтительный текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="71036-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="71036-178">Копирования содержимого hello между hello begin и hello конец заголовка сертификата и вставьте его в hello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="71036-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="71036-179">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="71036-179">Click **Save**.</span></span> <span data-ttu-id="71036-180">Go слишком[Asana руководство по настройке единого входа](https://asana.com/guide/help/premium/authentication#gl-saml) Если вам нужна дополнительная помощь.</span><span class="sxs-lookup"><span data-stu-id="71036-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="71036-181">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="71036-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="71036-182">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="71036-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="71036-183">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71036-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="71036-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="71036-184">Create an Azure AD test user</span></span>

<span data-ttu-id="71036-185">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="71036-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="71036-187">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="71036-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="71036-188">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="71036-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71036-190">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="71036-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71036-192">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="71036-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71036-194">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="71036-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71036-196">а.</span><span class="sxs-lookup"><span data-stu-id="71036-196">a.</span></span> <span data-ttu-id="71036-197">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71036-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71036-198">b.</span><span class="sxs-lookup"><span data-stu-id="71036-198">b.</span></span> <span data-ttu-id="71036-199">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="71036-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71036-200">c.</span><span class="sxs-lookup"><span data-stu-id="71036-200">c.</span></span> <span data-ttu-id="71036-201">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="71036-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="71036-202">d.</span><span class="sxs-lookup"><span data-stu-id="71036-202">d.</span></span> <span data-ttu-id="71036-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="71036-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="71036-204">Создание тестового пользователя Asana</span><span class="sxs-lookup"><span data-stu-id="71036-204">Create an Asana test user</span></span>

<span data-ttu-id="71036-205">В этом разделе описано, как создать пользователя Britta Simon в приложении Asana.</span><span class="sxs-lookup"><span data-stu-id="71036-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="71036-206">На **Asana**, go toohello **команды** раздел на левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="71036-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="71036-207">Нажмите кнопку hello, а также кнопки входа.</span><span class="sxs-lookup"><span data-stu-id="71036-207">Click hello plus sign button.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="71036-209">Введите по электронной почте hello britta.simon@contoso.com в hello текстовое поле, а затем выберите **пригласить**.</span><span class="sxs-lookup"><span data-stu-id="71036-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="71036-210">Щелкните **Send Invite**(Отправить приглашение).</span><span class="sxs-lookup"><span data-stu-id="71036-210">Click **Send Invite**.</span></span> <span data-ttu-id="71036-211">Hello новый пользователь получит сообщение электронной почты в свою учетную запись электронной почты.</span><span class="sxs-lookup"><span data-stu-id="71036-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="71036-212">Она может потребоваться toocreate и проверить подлинность учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="71036-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="71036-213">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="71036-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="71036-214">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAsana доступа.</span><span class="sxs-lookup"><span data-stu-id="71036-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![Назначение пользователям ролей hello][200]

<span data-ttu-id="71036-216">**tooassign tooAsana Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="71036-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="71036-217">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="71036-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="71036-219">В списке приложений hello выберите **Asana**.</span><span class="sxs-lookup"><span data-stu-id="71036-219">In hello applications list, select **Asana**.</span></span>

    ![ссылка Asana Hello в списке приложений hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="71036-221">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="71036-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="71036-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="71036-223">Click **Add** button.</span></span> <span data-ttu-id="71036-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="71036-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="71036-226">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="71036-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="71036-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="71036-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71036-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="71036-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="71036-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="71036-229">Test single sign-on</span></span>

<span data-ttu-id="71036-230">Цель этого раздела Hello является tootest к Azure AD единого входа.</span><span class="sxs-lookup"><span data-stu-id="71036-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="71036-231">Переход на страницу входа tooAsana.</span><span class="sxs-lookup"><span data-stu-id="71036-231">Go tooAsana login page.</span></span> <span data-ttu-id="71036-232">В текстовом поле адрес электронной почты hello вставить адрес электронной почты hello britta.simon@contoso.com. Оставьте текстовое поле пароля hello в пустым и нажмите кнопку **входа в**.</span><span class="sxs-lookup"><span data-stu-id="71036-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="71036-233">Будет перенаправленный tooAzure AD страницы входа.</span><span class="sxs-lookup"><span data-stu-id="71036-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="71036-234">Введите учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71036-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="71036-235">Теперь вы должны войти в Asana.</span><span class="sxs-lookup"><span data-stu-id="71036-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71036-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="71036-236">Additional resources</span></span>

* [<span data-ttu-id="71036-237">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71036-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71036-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="71036-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
