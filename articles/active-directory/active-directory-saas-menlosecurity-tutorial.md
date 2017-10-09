---
title: "Руководство по интеграции Azure Active Directory с Menlo Security | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Menlo безопасности."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="5b712-103">Руководство по интеграции Azure Active Directory с Menlo Security</span><span class="sxs-lookup"><span data-stu-id="5b712-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="5b712-104">В этом учебнике вы узнаете, как toointegrate Menlo безопасности в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b712-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b712-105">Интеграция безопасности Menlo с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5b712-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b712-106">Можно управлять в Azure AD, имеющего доступ tooMenlo безопасности</span><span class="sxs-lookup"><span data-stu-id="5b712-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="5b712-107">Можно включить на пользователей tooautomatically get вошедшего tooMenlo безопасности (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b712-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b712-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5b712-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b712-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b712-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="5b712-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b712-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b712-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5b712-111">Prerequisites</span></span>

<span data-ttu-id="5b712-112">tooconfigure интеграция Azure AD с Menlo безопасности необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5b712-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="5b712-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5b712-113">An Azure AD subscription</span></span>
- <span data-ttu-id="5b712-114">подписка Menlo Security с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5b712-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b712-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5b712-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b712-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5b712-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b712-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5b712-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b712-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b712-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b712-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5b712-119">Scenario description</span></span>
<span data-ttu-id="5b712-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5b712-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b712-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5b712-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b712-122">Добавление Menlo безопасности из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="5b712-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="5b712-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b712-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="5b712-124">Добавление Menlo безопасности из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="5b712-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="5b712-125">tooconfigure hello интеграции Menlo безопасности в Azure AD, вы должны tooadd Menlo безопасности из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5b712-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b712-126">**tooadd Menlo безопасности из коллекции hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5b712-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b712-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5b712-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b712-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5b712-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b712-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5b712-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5b712-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5b712-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5b712-134">Введите в поле поиска hello **Menlo безопасности**.</span><span class="sxs-lookup"><span data-stu-id="5b712-134">In hello search box, type **Menlo Security**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="5b712-136">В панели результатов hello выберите **безопасности Menlo**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5b712-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b712-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b712-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b712-139">В этом разделе описана настройка и проверка единого входа Azure AD в Menlo Security с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b712-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5b712-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Menlo безопасности является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b712-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="5b712-141">Другими словами связи между пользователя Azure AD и hello связанных пользователей в системе безопасности Menlo должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5b712-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="5b712-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** Menlo безопасности.</span><span class="sxs-lookup"><span data-stu-id="5b712-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="5b712-143">tooconfigure и теста Azure AD единого входа с Menlo безопасности, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="5b712-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b712-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5b712-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b712-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5b712-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b712-146">**[Создание тестового пользователя безопасности Menlo](#creating-a-menlo-security-test-user)**  -toohave аналог Саймон Britta в Menlo безопасности, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5b712-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b712-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5b712-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b712-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5b712-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b712-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b712-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b712-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Menlo безопасности.</span><span class="sxs-lookup"><span data-stu-id="5b712-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="5b712-151">**tooconfigure Azure AD единого входа с безопасностью Menlo выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5b712-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b712-152">В hello в hello портала Azure **безопасности Menlo** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5b712-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5b712-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5b712-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="5b712-156">На hello **Menlo безопасности домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5b712-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="5b712-158">а.</span><span class="sxs-lookup"><span data-stu-id="5b712-158">a.</span></span> <span data-ttu-id="5b712-159">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="5b712-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="5b712-160">b.</span><span class="sxs-lookup"><span data-stu-id="5b712-160">b.</span></span> <span data-ttu-id="5b712-161">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="5b712-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b712-162">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="5b712-162">These values are not hello real.</span></span> <span data-ttu-id="5b712-163">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="5b712-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5b712-164">Обратитесь к [Menlo безопасности клиента поддержки](https://www.menlosecurity.com/menlo-contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="5b712-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="5b712-165">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="5b712-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="5b712-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5b712-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b712-169">На hello **конфигурация безопасности Menlo** щелкните **Настройка безопасности Menlo** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="5b712-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5b712-170">Копировать hello **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="5b712-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="5b712-172">tooconfigure единого входа на **безопасности Menlo** стороны, toohello входа **Menlo безопасности** веб-сайта от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="5b712-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="5b712-173">В разделе **параметры** go слишком**проверки подлинности** и выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5b712-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="5b712-175">а.</span><span class="sxs-lookup"><span data-stu-id="5b712-175">a.</span></span> <span data-ttu-id="5b712-176">Деления hello флажок **включить проверку подлинности пользователя с помощью SAML**.</span><span class="sxs-lookup"><span data-stu-id="5b712-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="5b712-177">b.</span><span class="sxs-lookup"><span data-stu-id="5b712-177">b.</span></span> <span data-ttu-id="5b712-178">Выберите **разрешить внешний доступ** слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="5b712-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="5b712-179">c.</span><span class="sxs-lookup"><span data-stu-id="5b712-179">c.</span></span> <span data-ttu-id="5b712-180">В разделе **SAML Provider** (Поставщик SAML) выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b712-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="5b712-181">d.</span><span class="sxs-lookup"><span data-stu-id="5b712-181">d.</span></span> <span data-ttu-id="5b712-182">**Конечная точка SAML 2.0** : hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5b712-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5b712-183">д.</span><span class="sxs-lookup"><span data-stu-id="5b712-183">e.</span></span> <span data-ttu-id="5b712-184">**Идентификатор службы (издатель)** : hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5b712-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5b712-185">f.</span><span class="sxs-lookup"><span data-stu-id="5b712-185">f.</span></span> <span data-ttu-id="5b712-186">**Сертификат X.509** : Привет открыть **сертификата (Base64)** загружаются из hello портала Azure в Блокнот и вставьте его в этом поле.</span><span class="sxs-lookup"><span data-stu-id="5b712-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="5b712-187">ж.</span><span class="sxs-lookup"><span data-stu-id="5b712-187">g.</span></span> <span data-ttu-id="5b712-188">Нажмите кнопку **Сохранить** toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="5b712-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="5b712-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5b712-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b712-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5b712-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b712-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b712-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b712-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b712-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b712-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5b712-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5b712-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5b712-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b712-196">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5b712-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b712-198">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5b712-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b712-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="5b712-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b712-202">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5b712-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b712-204">а.</span><span class="sxs-lookup"><span data-stu-id="5b712-204">a.</span></span> <span data-ttu-id="5b712-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b712-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b712-206">b.</span><span class="sxs-lookup"><span data-stu-id="5b712-206">b.</span></span> <span data-ttu-id="5b712-207">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b712-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b712-208">c.</span><span class="sxs-lookup"><span data-stu-id="5b712-208">c.</span></span> <span data-ttu-id="5b712-209">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5b712-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b712-210">d.</span><span class="sxs-lookup"><span data-stu-id="5b712-210">d.</span></span> <span data-ttu-id="5b712-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5b712-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="5b712-212">Создание тестового пользователя Menlo Security</span><span class="sxs-lookup"><span data-stu-id="5b712-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="5b712-213">В этом разделе описано, как создать пользователя Britta Simon в приложении Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="5b712-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="5b712-214">Работать с [Menlo безопасности клиента поддержки](https://www.menlosecurity.com/menlo-contact) tooadd пользователей hello hello Menlo безопасности платформы.</span><span class="sxs-lookup"><span data-stu-id="5b712-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="5b712-215">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="5b712-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b712-216">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5b712-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b712-217">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooMenlo безопасности.</span><span class="sxs-lookup"><span data-stu-id="5b712-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5b712-219">**tooassign tooMenlo Britta Simon безопасности, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="5b712-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b712-220">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5b712-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5b712-222">В списке приложений hello выберите **Menlo безопасности**.</span><span class="sxs-lookup"><span data-stu-id="5b712-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="5b712-224">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5b712-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5b712-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5b712-226">Click **Add** button.</span></span> <span data-ttu-id="5b712-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5b712-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5b712-229">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5b712-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b712-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5b712-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b712-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5b712-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b712-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5b712-232">Testing single sign-on</span></span>

<span data-ttu-id="5b712-233">В этом разделе описано, как проверить конфигурацию единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b712-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="5b712-234">Откройте окно браузера в «InPrivate» или «Анонимный» режим tootrigger новыми параметрами проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5b712-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="5b712-235">В Internet Explorer нажмите клавиши CTRL+SHIFT+P.</span><span class="sxs-lookup"><span data-stu-id="5b712-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="5b712-236">В Chrome нажмите клавиши CTRL+SHIFT+N.</span><span class="sxs-lookup"><span data-stu-id="5b712-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="5b712-237">В hello закрытого просмотра окне обзора tooa защищенный ресурс и выполнения входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b712-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="5b712-238">После успешного входа в сеансе изоляции будет взят toohello запрошенного узла.</span><span class="sxs-lookup"><span data-stu-id="5b712-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b712-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5b712-239">Additional resources</span></span>

* [<span data-ttu-id="5b712-240">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b712-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b712-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b712-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

