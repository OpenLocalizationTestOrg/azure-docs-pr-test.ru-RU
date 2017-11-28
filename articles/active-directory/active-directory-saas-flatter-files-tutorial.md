---
title: "Учебник. Интеграция Azure Active Directory с Flatter Files | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и плоское файлами."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="ec816-103">Руководство. Интеграция Azure Active Directory с Flatter Files</span><span class="sxs-lookup"><span data-stu-id="ec816-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="ec816-104">В этом учебнике вы узнаете, как toointegrate плоское файлы с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec816-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec816-105">Интеграция плоское файлы с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ec816-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ec816-106">Можно управлять в Azure AD, который имеет доступ tooFlatter файлов</span><span class="sxs-lookup"><span data-stu-id="ec816-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="ec816-107">Можно включить вашей tooautomatically пользователи получить файлы вошедшего tooFlatter (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec816-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec816-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ec816-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ec816-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec816-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec816-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ec816-110">Prerequisites</span></span>

<span data-ttu-id="ec816-111">tooconfigure интеграция Azure AD с плоское файлов необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ec816-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="ec816-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ec816-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec816-113">подписка с поддержкой единого входа в Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="ec816-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec816-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ec816-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec816-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ec816-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec816-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ec816-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec816-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec816-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec816-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ec816-118">Scenario description</span></span>
<span data-ttu-id="ec816-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ec816-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec816-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ec816-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec816-121">Добавление файлов плоское из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ec816-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="ec816-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec816-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="ec816-123">Добавление файлов плоское из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ec816-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="ec816-124">tooconfigure hello интеграция плоское файлов в Azure AD, вы должны tooadd плоское файлов из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ec816-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ec816-125">**tooadd плоское файлы из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ec816-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec816-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ec816-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ec816-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ec816-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ec816-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ec816-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ec816-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ec816-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ec816-133">Введите в поле поиска hello **плоское файлы**.</span><span class="sxs-lookup"><span data-stu-id="ec816-133">In hello search box, type **Flatter Files**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="ec816-135">В панели результатов hello выберите **плоское файлы**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ec816-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec816-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec816-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec816-138">В этом разделе описана настройка и проверка единого входа Azure AD в Flatter Files с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec816-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ec816-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в плоское файлах является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec816-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="ec816-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в плоское файлов должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ec816-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="ec816-141">В файлах плоское, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ec816-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ec816-142">tooconfigure и теста Azure AD единого входа с плоское файлы, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="ec816-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ec816-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ec816-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ec816-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ec816-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec816-145">**[Создание тестового пользователя плоское файлы](#creating-a-flatter-files-test-user)**  -toohave аналог Саймон Britta в плоское файлов, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ec816-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec816-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ec816-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec816-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ec816-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec816-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec816-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec816-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении плоское файлы.</span><span class="sxs-lookup"><span data-stu-id="ec816-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="ec816-150">**tooconfigure Azure AD единого входа с плоское файлов выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ec816-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec816-151">В hello в hello портала Azure **плоское файлы** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ec816-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ec816-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ec816-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="ec816-155">На hello **плоское домена файлы и URL-адреса** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="ec816-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="ec816-157">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ec816-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="ec816-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ec816-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ec816-161">На hello **плоское файлы конфигурации** щелкните **Настройка плоское файлы** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ec816-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ec816-162">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ec816-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="ec816-164">Вход tooyour плоское файлы приложения с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ec816-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="ec816-165">Щелкните **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="ec816-165">Click **DASHBOARD**.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="ec816-167">Нажмите кнопку **параметры**, а затем выполните следующие действия на hello hello **компании** вкладки:</span><span class="sxs-lookup"><span data-stu-id="ec816-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="ec816-169">а.</span><span class="sxs-lookup"><span data-stu-id="ec816-169">a.</span></span> <span data-ttu-id="ec816-170">Установите флажок **Use SAML 2.0 For Authentication**(Использовать SAML 2.0 для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="ec816-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="ec816-171">b.</span><span class="sxs-lookup"><span data-stu-id="ec816-171">b.</span></span> <span data-ttu-id="ec816-172">Нажмите кнопку **Configure SAML** (Настроить SAML).</span><span class="sxs-lookup"><span data-stu-id="ec816-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="ec816-173">На hello **конфигурация SAML** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ec816-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="ec816-175">а.</span><span class="sxs-lookup"><span data-stu-id="ec816-175">a.</span></span> <span data-ttu-id="ec816-176">В hello **домена** текстовом поле введите имя домена, зарегистрированного.</span><span class="sxs-lookup"><span data-stu-id="ec816-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="ec816-177">Если у вас нет зарегистрированного домена, обратитесь в службу поддержки Flatter Files по адресу [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="ec816-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="ec816-178">b.</span><span class="sxs-lookup"><span data-stu-id="ec816-178">b.</span></span> <span data-ttu-id="ec816-179">В **URL-адрес поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы** которого вы скопировали форме портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ec816-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="ec816-180">c.</span><span class="sxs-lookup"><span data-stu-id="ec816-180">c.</span></span>  <span data-ttu-id="ec816-181">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ec816-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="ec816-182">d.</span><span class="sxs-lookup"><span data-stu-id="ec816-182">d.</span></span> <span data-ttu-id="ec816-183">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="ec816-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="ec816-184">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ec816-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ec816-185">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ec816-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ec816-186">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec816-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec816-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec816-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec816-188">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ec816-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ec816-190">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ec816-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec816-191">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ec816-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec816-193">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ec816-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec816-195">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ec816-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec816-197">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ec816-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec816-199">а.</span><span class="sxs-lookup"><span data-stu-id="ec816-199">a.</span></span> <span data-ttu-id="ec816-200">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec816-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec816-201">b.</span><span class="sxs-lookup"><span data-stu-id="ec816-201">b.</span></span> <span data-ttu-id="ec816-202">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ec816-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec816-203">c.</span><span class="sxs-lookup"><span data-stu-id="ec816-203">c.</span></span> <span data-ttu-id="ec816-204">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ec816-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ec816-205">d.</span><span class="sxs-lookup"><span data-stu-id="ec816-205">d.</span></span> <span data-ttu-id="ec816-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ec816-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="ec816-207">Создание тестового пользователя Flatter Files</span><span class="sxs-lookup"><span data-stu-id="ec816-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="ec816-208">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в плоское файлы.</span><span class="sxs-lookup"><span data-stu-id="ec816-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="ec816-209">**toocreate пользователя с именем Britta Simon в плоское файлы выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ec816-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec816-210">Войдите на tooyour **плоское файлы** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="ec816-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="ec816-211">Hello hello левой панели навигации нажмите кнопку **параметры**, а затем нажмите кнопку hello **пользователей** вкладку.</span><span class="sxs-lookup"><span data-stu-id="ec816-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Создание пользователя Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="ec816-213">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="ec816-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="ec816-214">На hello **добавить пользователя** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ec816-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Создание пользователя Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="ec816-216">а.</span><span class="sxs-lookup"><span data-stu-id="ec816-216">a.</span></span> <span data-ttu-id="ec816-217">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ec816-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="ec816-218">b.</span><span class="sxs-lookup"><span data-stu-id="ec816-218">b.</span></span> <span data-ttu-id="ec816-219">В hello **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ec816-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="ec816-220">c.</span><span class="sxs-lookup"><span data-stu-id="ec816-220">c.</span></span> <span data-ttu-id="ec816-221">В hello **адрес электронной почты** текстовом поле введите адрес электронной почты Britta hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ec816-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="ec816-222">d.</span><span class="sxs-lookup"><span data-stu-id="ec816-222">d.</span></span> <span data-ttu-id="ec816-223">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="ec816-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ec816-224">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ec816-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ec816-225">В этом разделе включите Саймон Britta toouse Azure единого входа путем предоставления доступа к файлам tooFlatter.</span><span class="sxs-lookup"><span data-stu-id="ec816-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ec816-227">**tooassign Britta Simon tooFlatter файлы, выполняют hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="ec816-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec816-228">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ec816-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ec816-230">В списке приложений hello выберите **плоское файлы**.</span><span class="sxs-lookup"><span data-stu-id="ec816-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="ec816-232">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ec816-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ec816-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ec816-234">Click **Add** button.</span></span> <span data-ttu-id="ec816-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ec816-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ec816-237">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ec816-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ec816-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ec816-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec816-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ec816-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec816-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ec816-240">Testing single sign-on</span></span>

<span data-ttu-id="ec816-241">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ec816-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ec816-242">При нажатии кнопки приветствия плоское файлы плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour плоское файлы приложения.</span><span class="sxs-lookup"><span data-stu-id="ec816-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="ec816-243">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ec816-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec816-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ec816-244">Additional resources</span></span>

* [<span data-ttu-id="ec816-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec816-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec816-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ec816-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

