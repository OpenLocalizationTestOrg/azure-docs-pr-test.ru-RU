---
title: "Учебник. Интеграция Azure Active Directory с LogicMonitor | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="5e1c0-103">Руководство. Интеграция Azure Active Directory с LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="5e1c0-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="5e1c0-104">В этом учебнике вы узнаете, как toointegrate LogicMonitor с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e1c0-104">In this tutorial, you learn how toointegrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e1c0-105">Интеграция LogicMonitor с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-105">Integrating LogicMonitor with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5e1c0-106">Можно управлять в Azure AD, имеющего доступ tooLogicMonitor</span><span class="sxs-lookup"><span data-stu-id="5e1c0-106">You can control in Azure AD who has access tooLogicMonitor</span></span>
- <span data-ttu-id="5e1c0-107">Можно включить на пользователей tooautomatically get вошедшего tooLogicMonitor (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1c0-107">You can enable your users tooautomatically get signed-on tooLogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5e1c0-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5e1c0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5e1c0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5e1c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e1c0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5e1c0-110">Prerequisites</span></span>

<span data-ttu-id="5e1c0-111">tooconfigure интеграция Azure AD с LogicMonitor требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-111">tooconfigure Azure AD integration with LogicMonitor, you need hello following items:</span></span>

- <span data-ttu-id="5e1c0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5e1c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5e1c0-113">подписка LogicMonitor с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e1c0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e1c0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e1c0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e1c0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e1c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e1c0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5e1c0-118">Scenario description</span></span>
<span data-ttu-id="5e1c0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e1c0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e1c0-121">Добавление LogicMonitor из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5e1c0-121">Adding LogicMonitor from hello gallery</span></span>
2. <span data-ttu-id="5e1c0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-hello-gallery"></a><span data-ttu-id="5e1c0-123">Добавление LogicMonitor из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5e1c0-123">Adding LogicMonitor from hello gallery</span></span>
<span data-ttu-id="5e1c0-124">tooconfigure hello интеграции LogicMonitor в Azure AD, вы должны tooadd LogicMonitor из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-124">tooconfigure hello integration of LogicMonitor into Azure AD, you need tooadd LogicMonitor from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5e1c0-125">**tooadd LogicMonitor из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5e1c0-125">**tooadd LogicMonitor from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e1c0-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5e1c0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5e1c0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5e1c0-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5e1c0-133">Введите в поле поиска hello **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-133">In hello search box, type **LogicMonitor**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="5e1c0-135">В панели результатов hello выберите **LogicMonitor**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-135">In hello results panel, select **LogicMonitor**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5e1c0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5e1c0-138">В этом разделе описана настройка и проверка единого входа Azure AD в LogicMonitor с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5e1c0-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в LogicMonitor является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LogicMonitor is tooa user in Azure AD.</span></span> <span data-ttu-id="5e1c0-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в LogicMonitor должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-140">In other words, a link relationship between an Azure AD user and hello related user in LogicMonitor needs toobe established.</span></span>

<span data-ttu-id="5e1c0-141">В LogicMonitor, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-141">In LogicMonitor, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5e1c0-142">tooconfigure и теста Azure AD единого входа с LogicMonitor, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-142">tooconfigure and test Azure AD single sign-on with LogicMonitor, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5e1c0-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5e1c0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e1c0-145">**[Создание тестового пользователя LogicMonitor](#creating-a-logicmonitor-test-user)**  -toohave аналог Саймон Britta в LogicMonitor, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - toohave a counterpart of Britta Simon in LogicMonitor that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e1c0-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e1c0-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5e1c0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5e1c0-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="5e1c0-150">**Azure AD tooconfigure единого входа с LogicMonitor, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5e1c0-150">**tooconfigure Azure AD single sign-on with LogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e1c0-151">В hello в hello портала Azure **LogicMonitor** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-151">In hello Azure portal, on hello **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5e1c0-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="5e1c0-155">На hello **URL-адреса и домена LogicMonitor** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-155">On hello **LogicMonitor Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="5e1c0-157">а.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-157">a.</span></span> <span data-ttu-id="5e1c0-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="5e1c0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="5e1c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-159">b.</span></span> <span data-ttu-id="5e1c0-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="5e1c0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5e1c0-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-161">These values are not real.</span></span> <span data-ttu-id="5e1c0-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5e1c0-163">Обратитесь к [группа поддержки клиент LogicMonitor](https://www.logicmonitor.com/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="5e1c0-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="5e1c0-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5e1c0-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e1c0-168">Войдите в tooyour **LogicMonitor** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-168">Log in tooyour **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="5e1c0-169">В меню в верхней части hello hello выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-169">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="5e1c0-170">![Параметры](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="5e1c0-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="5e1c0-171">В hello bat навигации в левой части hello, щелкните **единого входа**</span><span class="sxs-lookup"><span data-stu-id="5e1c0-171">In hello navigation bat on hello left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="5e1c0-172">![Единый вход](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="5e1c0-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="5e1c0-173">В hello **параметры единого входа (SSO)** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-173">In hello **Single Sign-on (SSO) settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="5e1c0-174">![Параметры единого входа](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="5e1c0-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="5e1c0-175">а.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-175">a.</span></span> <span data-ttu-id="5e1c0-176">Выберите пункт **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="5e1c0-177">b.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-177">b.</span></span> <span data-ttu-id="5e1c0-178">Выберите для параметра **Default Role Assignment** (Назначение ролей по умолчанию) значение **readonly** (только для чтения).</span><span class="sxs-lookup"><span data-stu-id="5e1c0-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="5e1c0-179">c.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-179">c.</span></span> <span data-ttu-id="5e1c0-180">Откройте в блокноте файл hello загружены метаданные, а затем вставьте содержимое файла hello в hello **метаданные поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-180">Open hello downloaded metadata file in notepad, and then paste content of hello file into hello **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="5e1c0-181">d.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-181">d.</span></span> <span data-ttu-id="5e1c0-182">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5e1c0-183">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5e1c0-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5e1c0-184">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5e1c0-185">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5e1c0-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5e1c0-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e1c0-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="5e1c0-187">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5e1c0-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5e1c0-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e1c0-190">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5e1c0-192">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5e1c0-194">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="5e1c0-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5e1c0-196">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5e1c0-198">а.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-198">a.</span></span> <span data-ttu-id="5e1c0-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e1c0-200">b.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-200">b.</span></span> <span data-ttu-id="5e1c0-201">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5e1c0-202">c.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-202">c.</span></span> <span data-ttu-id="5e1c0-203">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5e1c0-204">d.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-204">d.</span></span> <span data-ttu-id="5e1c0-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="5e1c0-206">Создание тестового пользователя LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="5e1c0-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="5e1c0-207">Для AAD пользователей toobe может toosign в они должны быть подготовленных toohello приложении LogicMonitor с использованием своих имен пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-207">For AAD users toobe able toosign in, they must be provisioned toohello LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="5e1c0-208">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5e1c0-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e1c0-209">Войдите в систему tooyour сайт LogicMonitor компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-209">Log in tooyour LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="5e1c0-210">В меню в верхней части hello hello выберите **параметры**и нажмите кнопку **ролей и пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-210">In hello menu on hello top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="5e1c0-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users") (Роли и пользователи)</span><span class="sxs-lookup"><span data-stu-id="5e1c0-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="5e1c0-212">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-212">Click **Add**.</span></span>

4. <span data-ttu-id="5e1c0-213">В hello **добавить учетную запись** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e1c0-213">In hello **Add an account** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="5e1c0-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account") (Добавление учетной записи)</span><span class="sxs-lookup"><span data-stu-id="5e1c0-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="5e1c0-215">а.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-215">a.</span></span> <span data-ttu-id="5e1c0-216">Тип hello **имя пользователя**, **электронной почты**, **пароль**, и **повторить ввод пароля** значения нужного пользователя Azure Active Directory hello текстовые поля, связанные с tooprovision в hello.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-216">Type hello **Username**, **Email**, **Password**, and **Retype password** values of hello Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="5e1c0-217">b.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-217">b.</span></span> <span data-ttu-id="5e1c0-218">Выберите **ролей**, **разрешений на просмотр**и hello **состояние**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-218">Select **Roles**, **View Permissions**, and hello **Status**.</span></span>
   
   <span data-ttu-id="5e1c0-219">c.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-219">c.</span></span> <span data-ttu-id="5e1c0-220">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="5e1c0-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="5e1c0-221">Можно использовать любые другие LogicMonitor пользователя средства создания учетных записей или API, предоставленные LogicMonitor tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5e1c0-222">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5e1c0-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5e1c0-223">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLogicMonitor доступа.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLogicMonitor.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5e1c0-225">**tooassign tooLogicMonitor Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5e1c0-225">**tooassign Britta Simon tooLogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e1c0-226">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5e1c0-228">В списке приложений hello выберите **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-228">In hello applications list, select **LogicMonitor**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="5e1c0-230">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5e1c0-232">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-232">Click **Add** button.</span></span> <span data-ttu-id="5e1c0-233">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5e1c0-235">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5e1c0-236">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e1c0-237">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5e1c0-238">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5e1c0-238">Testing single sign-on</span></span>

<span data-ttu-id="5e1c0-239">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="5e1c0-240">Если щелкнуть плитку LogicMonitor hello в hello панели доступа, вы должны получить tooyour автоматически подписью в приложении LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="5e1c0-240">When you click hello LogicMonitor tile in hello Access Panel, you should get automatically signed-on tooyour LogicMonitor application.</span></span>
<span data-ttu-id="5e1c0-241">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e1c0-241">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5e1c0-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5e1c0-242">Additional resources</span></span>

* [<span data-ttu-id="5e1c0-243">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e1c0-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e1c0-244">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5e1c0-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

