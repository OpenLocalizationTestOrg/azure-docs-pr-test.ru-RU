---
title: "Руководство. Интеграция Azure Active Directory с HappyFox | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 1190652d7d1144c7eddea339cb3f9175912407fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="b9ca8-103">Руководство. Интеграция Azure Active Directory с HappyFox</span><span class="sxs-lookup"><span data-stu-id="b9ca8-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="b9ca8-104">В этом учебнике вы узнаете, как toointegrate HappyFox с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9ca8-104">In this tutorial, you learn how toointegrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9ca8-105">Интеграция с Azure AD HappyFox предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b9ca8-105">Integrating HappyFox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9ca8-106">Можно управлять в Azure AD, имеющего доступ tooHappyFox</span><span class="sxs-lookup"><span data-stu-id="b9ca8-106">You can control in Azure AD who has access tooHappyFox</span></span>
- <span data-ttu-id="b9ca8-107">Можно включить на пользователей tooautomatically get вошедшего tooHappyFox (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca8-107">You can enable your users tooautomatically get signed-on tooHappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9ca8-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b9ca8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9ca8-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9ca8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b9ca8-110">Prerequisites</span></span>

<span data-ttu-id="b9ca8-111">tooconfigure интеграция Azure AD с HappyFox требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b9ca8-111">tooconfigure Azure AD integration with HappyFox, you need hello following items:</span></span>

- <span data-ttu-id="b9ca8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b9ca8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9ca8-113">подписка HappyFox с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9ca8-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9ca8-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b9ca8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9ca8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9ca8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9ca8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9ca8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b9ca8-118">Scenario description</span></span>
<span data-ttu-id="b9ca8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9ca8-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b9ca8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9ca8-121">Добавление HappyFox из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b9ca8-121">Adding HappyFox from hello gallery</span></span>
2. <span data-ttu-id="b9ca8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-hello-gallery"></a><span data-ttu-id="b9ca8-123">Добавление HappyFox из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b9ca8-123">Adding HappyFox from hello gallery</span></span>
<span data-ttu-id="b9ca8-124">tooconfigure hello интеграции HappyFox в Azure AD, вы должны tooadd HappyFox из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-124">tooconfigure hello integration of HappyFox into Azure AD, you need tooadd HappyFox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9ca8-125">**tooadd HappyFox из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9ca8-125">**tooadd HappyFox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ca8-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9ca8-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9ca8-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b9ca8-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b9ca8-133">Введите в поле поиска hello **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-133">In hello search box, type **HappyFox**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="b9ca8-135">В панели результатов hello выберите **HappyFox**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-135">In hello results panel, select **HappyFox**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9ca8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9ca8-138">В этом разделе описана настройка и проверка единого входа Azure AD в HappyFox с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b9ca8-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в HappyFox является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HappyFox is tooa user in Azure AD.</span></span> <span data-ttu-id="b9ca8-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в HappyFox должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-140">In other words, a link relationship between an Azure AD user and hello related user in HappyFox needs toobe established.</span></span>

<span data-ttu-id="b9ca8-141">В HappyFox, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-141">In HappyFox, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9ca8-142">tooconfigure и теста Azure AD единого входа с HappyFox, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b9ca8-142">tooconfigure and test Azure AD single sign-on with HappyFox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9ca8-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9ca8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9ca8-145">**[Создание тестового пользователя HappyFox](#creating-a-happyfox-test-user)**  -toohave аналог Саймон Britta в HappyFox, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - toohave a counterpart of Britta Simon in HappyFox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9ca8-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9ca8-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9ca8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9ca8-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении HappyFox.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="b9ca8-150">**tooconfigure Azure AD единого входа с HappyFox, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9ca8-150">**tooconfigure Azure AD single sign-on with HappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ca8-151">В hello в hello портала Azure **HappyFox** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-151">In hello Azure portal, on hello **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b9ca8-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="b9ca8-155">На hello **URL-адреса и домена HappyFox** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9ca8-155">On hello **HappyFox Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="b9ca8-157">а.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-157">a.</span></span> <span data-ttu-id="b9ca8-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="b9ca8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="b9ca8-159">b.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-159">b.</span></span> <span data-ttu-id="b9ca8-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="b9ca8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9ca8-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-161">These values are not real.</span></span> <span data-ttu-id="b9ca8-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b9ca8-163">Обратитесь к [группа поддержки клиента HappyFox](https://support.happyfox.com/home) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) tooget these values.</span></span> 
 
4. <span data-ttu-id="b9ca8-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="b9ca8-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b9ca8-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9ca8-168">На hello **конфигурации HappyFox** щелкните **Настройка HappyFox** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-168">On hello **HappyFox Configuration** section, click **Configure HappyFox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b9ca8-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="b9ca8-171">Войдите на портал персонала HappyFox tooyour и перейдите слишком**управление**, щелкните на **интеграции** вкладки.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-171">Sign on tooyour HappyFox staff portal and navigate too**Manage**, Click on **Integrations** tab.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="b9ca8-173">Во вкладке интеграций hello нажмите **Настройка** под **интеграции SAML** tooopen hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-173">In hello Integrations tab, Click **Configure** under **SAML Integration** tooopen hello Single Sign On Settings.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="b9ca8-175">Вставьте hello внутри раздела конфигурации SAML, **SAML единого входа URL-адрес службы** , скопированный из портала Azure в **URL-адрес единого входа для целевого** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-175">Inside SAML configuration section, paste hello **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="b9ca8-177">Откройте сертификат hello загружен с портала Azure в Блокноте и вставьте его содержимое в **подписи поставщика удостоверений** раздела.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-177">Open hello certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="b9ca8-179">Нажмите кнопку **Save Settings** (Сохранить параметры).</span><span class="sxs-lookup"><span data-stu-id="b9ca8-179">Click **Save Settings** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="b9ca8-181">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b9ca8-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9ca8-182">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9ca8-183">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9ca8-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9ca8-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca8-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9ca8-185">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b9ca8-187">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9ca8-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ca8-188">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9ca8-190">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9ca8-192">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b9ca8-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9ca8-194">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9ca8-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9ca8-196">а.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-196">a.</span></span> <span data-ttu-id="b9ca8-197">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9ca8-198">b.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-198">b.</span></span> <span data-ttu-id="b9ca8-199">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9ca8-200">c.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-200">c.</span></span> <span data-ttu-id="b9ca8-201">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9ca8-202">d.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-202">d.</span></span> <span data-ttu-id="b9ca8-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="b9ca8-204">Создание тестового пользователя HappyFox</span><span class="sxs-lookup"><span data-stu-id="b9ca8-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="b9ca8-205">Приложение поддерживает только в подготовки пользователей время и после проверки подлинности пользователей автоматически создаются в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-205">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9ca8-206">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b9ca8-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9ca8-207">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHappyFox доступа.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHappyFox.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b9ca8-209">**tooassign tooHappyFox Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9ca8-209">**tooassign Britta Simon tooHappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ca8-210">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b9ca8-212">В списке приложений hello выберите **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-212">In hello applications list, select **HappyFox**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="b9ca8-214">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b9ca8-216">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-216">Click **Add** button.</span></span> <span data-ttu-id="b9ca8-217">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b9ca8-219">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9ca8-220">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9ca8-221">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9ca8-222">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b9ca8-222">Testing single sign-on</span></span>

<span data-ttu-id="b9ca8-223">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="b9ca8-224">При нажатии кнопки hello HappyFox плитки в панели доступа hello, должно появиться страница входа HappyFox приложения.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-224">When you click hello HappyFox tile in hello Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="b9ca8-225">Вы увидите hello **«SAML»** кнопку на страницу входа hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-225">You should see hello **‘SAML’** button on hello sign-in page.</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="b9ca8-227">Нажмите кнопку hello **«SAML»** toolog кнопки в tooHappyFox с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9ca8-227">Click hello **‘SAML’** button toolog in tooHappyFox using your Azure AD account.</span></span>

<span data-ttu-id="b9ca8-228">Дополнительные сведения о панели доступа hello см. в разделе [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca8-228">For more information about hello Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9ca8-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b9ca8-229">Additional resources</span></span>

* [<span data-ttu-id="b9ca8-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9ca8-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9ca8-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9ca8-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

