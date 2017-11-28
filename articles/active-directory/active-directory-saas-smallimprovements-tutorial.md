---
title: "Руководство по интеграции Azure Active Directory со Small Improvements | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и усовершенствований."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="32f21-103">Учебник. Интеграция Azure Active Directory со Small Improvements</span><span class="sxs-lookup"><span data-stu-id="32f21-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="32f21-104">В этом учебнике вы узнаете, как toointegrate усовершенствований в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32f21-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32f21-105">Интеграция с Azure AD усовершенствований предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="32f21-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32f21-106">Можно управлять в Azure AD, имеющего доступ tooSmall усовершенствования</span><span class="sxs-lookup"><span data-stu-id="32f21-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="32f21-107">Можно включить на пользователей tooautomatically get вошедшего tooSmall усовершенствования (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f21-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32f21-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="32f21-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32f21-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32f21-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32f21-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="32f21-110">Prerequisites</span></span>

<span data-ttu-id="32f21-111">tooconfigure интеграция Azure AD с усовершенствований необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="32f21-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="32f21-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="32f21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32f21-113">подписка Small Improvements с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="32f21-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32f21-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="32f21-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32f21-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="32f21-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32f21-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="32f21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32f21-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32f21-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32f21-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="32f21-118">Scenario description</span></span>
<span data-ttu-id="32f21-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="32f21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32f21-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="32f21-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32f21-121">Добавление усовершенствований из галереи hello</span><span class="sxs-lookup"><span data-stu-id="32f21-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="32f21-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="32f21-123">Добавление усовершенствований из галереи hello</span><span class="sxs-lookup"><span data-stu-id="32f21-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="32f21-124">tooconfigure hello интеграции усовершенствований в Azure AD, вы должны tooadd усовершенствований из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="32f21-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32f21-125">**tooadd усовершенствований из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="32f21-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f21-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="32f21-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32f21-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="32f21-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32f21-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="32f21-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="32f21-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="32f21-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="32f21-133">Введите в поле поиска hello **усовершенствований**.</span><span class="sxs-lookup"><span data-stu-id="32f21-133">In hello search box, type **Small Improvements**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="32f21-135">В панели результатов hello выберите **усовершенствований**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="32f21-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32f21-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32f21-138">В этом разделе описана настройка и проверка единого входа Azure AD в Small Improvements с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32f21-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32f21-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в небольших улучшений является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32f21-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="32f21-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в небольших улучшений должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="32f21-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="32f21-141">В небольших улучшений, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="32f21-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="32f21-142">tooconfigure и теста Azure AD единого входа с усовершенствований, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="32f21-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32f21-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="32f21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32f21-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="32f21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32f21-145">**[Создание тестового пользователя усовершенствований](#creating-a-small-improvements-test-user)**  -toohave аналог Саймон Britta небольших улучшений, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="32f21-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="32f21-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="32f21-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32f21-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="32f21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32f21-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32f21-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении усовершенствований.</span><span class="sxs-lookup"><span data-stu-id="32f21-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="32f21-150">**tooconfigure Azure AD единого входа с усовершенствований, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="32f21-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f21-151">В hello в hello портала Azure **усовершенствований** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="32f21-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="32f21-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="32f21-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="32f21-155">На hello **небольших улучшений доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="32f21-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="32f21-157">а.</span><span class="sxs-lookup"><span data-stu-id="32f21-157">a.</span></span> <span data-ttu-id="32f21-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="32f21-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="32f21-159">b.</span><span class="sxs-lookup"><span data-stu-id="32f21-159">b.</span></span> <span data-ttu-id="32f21-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="32f21-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32f21-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="32f21-161">These values are not real.</span></span> <span data-ttu-id="32f21-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="32f21-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32f21-163">Обратитесь к [клиента небольшие улучшения поддержки](mailto:support@small-improvements.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="32f21-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="32f21-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="32f21-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="32f21-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="32f21-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32f21-168">На hello **небольшие улучшения конфигурации** щелкните **Настройка усовершенствований** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="32f21-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="32f21-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="32f21-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="32f21-171">В другом окне браузера Войдите на сайт компании усовершенствований tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="32f21-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="32f21-172">На странице приветствия главной панели мониторинга нажмите **администрирования** кнопку левой hello.</span><span class="sxs-lookup"><span data-stu-id="32f21-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="32f21-174">Нажмите кнопку hello **единого входа SAML** кнопку **интеграции** раздела.</span><span class="sxs-lookup"><span data-stu-id="32f21-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="32f21-176">На странице настройки единого входа hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="32f21-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="32f21-178">а.</span><span class="sxs-lookup"><span data-stu-id="32f21-178">a.</span></span> <span data-ttu-id="32f21-179">В hello **конечной точки HTTP** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="32f21-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="32f21-180">b.</span><span class="sxs-lookup"><span data-stu-id="32f21-180">b.</span></span> <span data-ttu-id="32f21-181">Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **x509 сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="32f21-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="32f21-182">c.</span><span class="sxs-lookup"><span data-stu-id="32f21-182">c.</span></span> <span data-ttu-id="32f21-183">Если вы хотите toohave единого входа и имя входа формы вариант проверки подлинности для пользователей, проверьте hello **включить доступ через имя входа и пароль слишком** параметр.</span><span class="sxs-lookup"><span data-stu-id="32f21-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="32f21-184">d.</span><span class="sxs-lookup"><span data-stu-id="32f21-184">d.</span></span> <span data-ttu-id="32f21-185">Введите соответствующее значение tooName hello hello-кнопка Единого входа в hello **SAML Prompt** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="32f21-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="32f21-186">д.</span><span class="sxs-lookup"><span data-stu-id="32f21-186">e.</span></span> <span data-ttu-id="32f21-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="32f21-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="32f21-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="32f21-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="32f21-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="32f21-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="32f21-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32f21-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32f21-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f21-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="32f21-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="32f21-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="32f21-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="32f21-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f21-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="32f21-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32f21-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="32f21-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32f21-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="32f21-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32f21-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="32f21-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32f21-203">а.</span><span class="sxs-lookup"><span data-stu-id="32f21-203">a.</span></span> <span data-ttu-id="32f21-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32f21-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32f21-205">b.</span><span class="sxs-lookup"><span data-stu-id="32f21-205">b.</span></span> <span data-ttu-id="32f21-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32f21-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32f21-207">c.</span><span class="sxs-lookup"><span data-stu-id="32f21-207">c.</span></span> <span data-ttu-id="32f21-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="32f21-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32f21-209">d.</span><span class="sxs-lookup"><span data-stu-id="32f21-209">d.</span></span> <span data-ttu-id="32f21-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="32f21-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="32f21-211">Создание тестового пользователя Small Improvements</span><span class="sxs-lookup"><span data-stu-id="32f21-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="32f21-212">Пользователи toolog tooenable Azure AD в tooSmall улучшения, их необходимо подготовить в усовершенствований.</span><span class="sxs-lookup"><span data-stu-id="32f21-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="32f21-213">В случае hello небольших улучшений Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="32f21-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="32f21-214">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="32f21-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f21-215">Корпоративный сайт усовершенствований tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="32f21-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="32f21-216">На домашней странице hello переходите toohello меню hello слева, нажмите кнопку **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="32f21-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="32f21-217">Нажмите кнопку hello **каталог пользователя** кнопку из раздела управления пользователями.</span><span class="sxs-lookup"><span data-stu-id="32f21-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="32f21-219">Щелкните **Add users** (Добавить пользователей).</span><span class="sxs-lookup"><span data-stu-id="32f21-219">Click **Add users**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="32f21-221">На hello **Добавление пользователей** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="32f21-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="32f21-223">а.</span><span class="sxs-lookup"><span data-stu-id="32f21-223">a.</span></span> <span data-ttu-id="32f21-224">Введите hello **имя** пользователя как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="32f21-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="32f21-225">b.</span><span class="sxs-lookup"><span data-stu-id="32f21-225">b.</span></span> <span data-ttu-id="32f21-226">Введите hello **Фамилия** пользователя как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="32f21-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="32f21-227">c.</span><span class="sxs-lookup"><span data-stu-id="32f21-227">c.</span></span> <span data-ttu-id="32f21-228">Введите hello **электронной почты** пользователя как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="32f21-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="32f21-229">d.</span><span class="sxs-lookup"><span data-stu-id="32f21-229">d.</span></span> <span data-ttu-id="32f21-230">Вы также можете личное сообщение hello tooenter в hello **отправить уведомление по электронной почте** поле.</span><span class="sxs-lookup"><span data-stu-id="32f21-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="32f21-231">При необходимости toosend hello уведомлений, снимите этот флажок.</span><span class="sxs-lookup"><span data-stu-id="32f21-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="32f21-232">д.</span><span class="sxs-lookup"><span data-stu-id="32f21-232">e.</span></span> <span data-ttu-id="32f21-233">Щелкните **Создать пользователей**.</span><span class="sxs-lookup"><span data-stu-id="32f21-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32f21-234">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="32f21-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32f21-235">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSmall улучшения.</span><span class="sxs-lookup"><span data-stu-id="32f21-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="32f21-237">**tooassign Britta Simon tooSmall улучшения, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="32f21-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="32f21-238">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="32f21-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="32f21-240">В списке приложений hello выберите **усовершенствований**.</span><span class="sxs-lookup"><span data-stu-id="32f21-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="32f21-242">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="32f21-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="32f21-244">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="32f21-244">Click **Add** button.</span></span> <span data-ttu-id="32f21-245">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="32f21-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="32f21-247">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="32f21-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32f21-248">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="32f21-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32f21-249">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="32f21-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32f21-250">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="32f21-250">Testing single sign-on</span></span>

<span data-ttu-id="32f21-251">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="32f21-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="32f21-252">При нажатии кнопки приветствия усовершенствований плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на небольшой усовершенствования приложения.</span><span class="sxs-lookup"><span data-stu-id="32f21-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32f21-253">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="32f21-253">Additional resources</span></span>

* [<span data-ttu-id="32f21-254">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32f21-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32f21-255">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32f21-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

