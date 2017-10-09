---
title: "Руководство по интеграции Azure Active Directory с Optimizely | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="bbe9e-103">Учебник. Интеграция Azure Active Directory с Optimizely</span><span class="sxs-lookup"><span data-stu-id="bbe9e-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="bbe9e-104">В этом учебнике вы узнаете, как toointegrate Optimizely с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbe9e-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbe9e-105">Интеграция с Azure AD Optimizely предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bbe9e-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bbe9e-106">Можно управлять в Azure AD, имеющего доступ tooOptimizely</span><span class="sxs-lookup"><span data-stu-id="bbe9e-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="bbe9e-107">Можно включить на пользователей tooautomatically get вошедшего tooOptimizely (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbe9e-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbe9e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bbe9e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bbe9e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbe9e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbe9e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bbe9e-110">Prerequisites</span></span>

<span data-ttu-id="bbe9e-111">tooconfigure интеграция Azure AD с Optimizely требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="bbe9e-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="bbe9e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bbe9e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbe9e-113">подписка Optimizely с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbe9e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbe9e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="bbe9e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbe9e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbe9e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbe9e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbe9e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bbe9e-118">Scenario description</span></span>
<span data-ttu-id="bbe9e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbe9e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="bbe9e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbe9e-121">Добавление Optimizely из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bbe9e-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="bbe9e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbe9e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="bbe9e-123">Добавление Optimizely из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bbe9e-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="bbe9e-124">tooconfigure hello интеграции Optimizely в Azure AD, вы должны tooadd Optimizely из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bbe9e-125">**tooadd Optimizely из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bbe9e-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbe9e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bbe9e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bbe9e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bbe9e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bbe9e-133">Введите в поле поиска hello **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-133">In hello search box, type **Optimizely**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="bbe9e-135">В панели результатов hello выберите **Optimizely**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bbe9e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbe9e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bbe9e-138">В этом разделе описана настройка и проверка единого входа Azure AD в Optimizely с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bbe9e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Optimizely является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="bbe9e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Optimizely должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="bbe9e-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Optimizely.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="bbe9e-142">tooconfigure и теста Azure AD единого входа с Optimizely, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bbe9e-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bbe9e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bbe9e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbe9e-145">**[Создание тестового пользователя, прошедшего Optimizely](#creating-an-optimizely-test-user)**  -toohave аналог Саймон Britta в Optimizely, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbe9e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbe9e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bbe9e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbe9e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bbe9e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Optimizely.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="bbe9e-150">**tooconfigure Azure AD единого входа с Optimizely, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bbe9e-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbe9e-151">В hello в hello портала Azure **Optimizely** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bbe9e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="bbe9e-155">На hello **URL-адреса и домена Optimizely** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bbe9e-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="bbe9e-157">а.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-157">a.</span></span> <span data-ttu-id="bbe9e-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="bbe9e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="bbe9e-159">b.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-159">b.</span></span> <span data-ttu-id="bbe9e-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="bbe9e-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bbe9e-161">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-161">These values are not hello real.</span></span> <span data-ttu-id="bbe9e-162">Значение hello будут обновлены hello фактический URL-адрес входа и идентификатор, который описан далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="bbe9e-163">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="bbe9e-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bbe9e-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bbe9e-167">На hello **конфигурации Optimizely** щелкните **Настройка Optimizely** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bbe9e-168">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="bbe9e-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="bbe9e-170">tooconfigure единого входа на **Optimizely** стороны, обратитесь к менеджеру по продажам Optimizely и обеспечения загружаются hello **сертификата (Base64)**, и **SAML единого входа URL-адрес службы** .</span><span class="sxs-lookup"><span data-stu-id="bbe9e-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="bbe9e-171">В сообщении электронной почты tooyour ответ Optimizely предоставляет приветствия на URL-адрес входа (SSO, инициированные SP) и hello значения идентификатора (идентификатор сущности поставщика службы).</span><span class="sxs-lookup"><span data-stu-id="bbe9e-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="bbe9e-172">а.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-172">a.</span></span> <span data-ttu-id="bbe9e-173">Копировать hello **инициируемая SP URL-адрес единого входа** предоставляемого Optimizely и вставить в hello **на URL-адрес входа** текстовое поле в **URL-адреса и домена Optimizely** раздела на портале Azure</span><span class="sxs-lookup"><span data-stu-id="bbe9e-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="bbe9e-174">b.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-174">b.</span></span> <span data-ttu-id="bbe9e-175">Копировать hello **идентификатор сущности поставщика службы** предоставляемого Optimizely и вставить в hello **идентификатор** текстовое поле в **URL-адреса и домена Optimizely** раздела на портале Azure</span><span class="sxs-lookup"><span data-stu-id="bbe9e-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="bbe9e-176">В другом окне браузера, tooyour входа Optimizely приложения.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="bbe9e-177">Нажмите кнопку, можно ввести имя учетной записи в предложении top hello правом углу и затем **параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Единый вход в Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="bbe9e-179">Во вкладке "учетная запись" hello, установите флажок "hello" **Включить единый вход** в области единого входа в hello **Обзор** раздела.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Единый вход в Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="bbe9e-181">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="bbe9e-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="bbe9e-182">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="bbe9e-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bbe9e-183">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bbe9e-184">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbe9e-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bbe9e-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbe9e-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="bbe9e-186">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bbe9e-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bbe9e-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbe9e-189">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbe9e-191">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbe9e-193">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="bbe9e-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbe9e-195">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bbe9e-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbe9e-197">а.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-197">a.</span></span> <span data-ttu-id="bbe9e-198">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbe9e-199">b.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-199">b.</span></span> <span data-ttu-id="bbe9e-200">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="bbe9e-201">c.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-201">c.</span></span> <span data-ttu-id="bbe9e-202">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bbe9e-203">d.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-203">d.</span></span> <span data-ttu-id="bbe9e-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="bbe9e-205">Создание тестового пользователя Optimizely</span><span class="sxs-lookup"><span data-stu-id="bbe9e-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="bbe9e-206">В этом разделе описано, как создать пользователя Britta Simon в приложении Optimizely.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="bbe9e-207">На домашней странице приветствия установите **участники совместной работы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="bbe9e-208">tooadd новый проект toohello участника совместной работы, нажмите кнопку **нового участника совместной работы**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="bbe9e-210">Введите адрес электронной почты hello и назначить ему роль.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="bbe9e-211">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-211">Click **Invite**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="bbe9e-213">Он получит приглашение по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-213">They receive an email invite.</span></span> <span data-ttu-id="bbe9e-214">С помощью адреса электронной почты hello, они имеют toolog tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bbe9e-215">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bbe9e-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bbe9e-216">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooOptimizely доступа.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bbe9e-218">**tooassign tooOptimizely Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bbe9e-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbe9e-219">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bbe9e-221">В списке приложений hello выберите **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-221">In hello applications list, select **Optimizely**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="bbe9e-223">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bbe9e-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-225">Click **Add** button.</span></span> <span data-ttu-id="bbe9e-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bbe9e-228">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bbe9e-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbe9e-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bbe9e-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bbe9e-231">Testing single sign-on</span></span>

<span data-ttu-id="bbe9e-232">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bbe9e-233">При нажатии кнопки hello Optimizely плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Optimizely приложения.</span><span class="sxs-lookup"><span data-stu-id="bbe9e-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bbe9e-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bbe9e-234">Additional resources</span></span>

* [<span data-ttu-id="bbe9e-235">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbe9e-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbe9e-236">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbe9e-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

