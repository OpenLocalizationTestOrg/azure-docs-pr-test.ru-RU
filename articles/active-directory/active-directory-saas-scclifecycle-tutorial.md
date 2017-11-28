---
title: "Руководство по интеграции Azure Active Directory с SCC LifeCycle | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SCC LifeCycle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 63623c5bd2d951612040f0121615a406bf83e890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="0eb46-103">Учебник. Интеграция Azure Active Directory с SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="0eb46-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>

<span data-ttu-id="0eb46-104">В этом учебнике вы узнаете, как toointegrate SCC LifeCycle с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0eb46-104">In this tutorial, you learn how toointegrate SCC LifeCycle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0eb46-105">Интеграция SCC LifeCycle с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0eb46-105">Integrating SCC LifeCycle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0eb46-106">Можно управлять в Azure AD, имеющего доступ tooSCC жизненного цикла</span><span class="sxs-lookup"><span data-stu-id="0eb46-106">You can control in Azure AD who has access tooSCC LifeCycle</span></span>
- <span data-ttu-id="0eb46-107">Можно включить на пользователей tooautomatically get вошедшего tooSCC жизненного цикла (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb46-107">You can enable your users tooautomatically get signed-on tooSCC LifeCycle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0eb46-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0eb46-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0eb46-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0eb46-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0eb46-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0eb46-110">Prerequisites</span></span>

<span data-ttu-id="0eb46-111">tooconfigure интеграция Azure AD с SCC LifeCycle, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0eb46-111">tooconfigure Azure AD integration with SCC LifeCycle, you need hello following items:</span></span>

- <span data-ttu-id="0eb46-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0eb46-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0eb46-113">подписка SCC LifeCycle с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0eb46-113">An SCC LifeCycle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0eb46-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0eb46-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0eb46-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0eb46-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0eb46-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0eb46-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0eb46-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0eb46-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0eb46-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0eb46-118">Scenario description</span></span>
<span data-ttu-id="0eb46-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0eb46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0eb46-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0eb46-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0eb46-121">Добавление SCC LifeCycle из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0eb46-121">Adding SCC LifeCycle from hello gallery</span></span>
2. <span data-ttu-id="0eb46-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb46-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scc-lifecycle-from-hello-gallery"></a><span data-ttu-id="0eb46-123">Добавление SCC LifeCycle из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0eb46-123">Adding SCC LifeCycle from hello gallery</span></span>
<span data-ttu-id="0eb46-124">tooconfigure hello интеграцией SCC LifeCycle с Azure AD, вы должны tooadd SCC LifeCycle из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0eb46-124">tooconfigure hello integration of SCC LifeCycle into Azure AD, you need tooadd SCC LifeCycle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0eb46-125">**tooadd SCC LifeCycle из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0eb46-125">**tooadd SCC LifeCycle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0eb46-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0eb46-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0eb46-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0eb46-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0eb46-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0eb46-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0eb46-133">Введите в поле поиска hello **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-133">In hello search box, type **SCC LifeCycle**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_search.png)

5. <span data-ttu-id="0eb46-135">В панели результатов hello выберите **SCC LifeCycle**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0eb46-135">In hello results panel, select **SCC LifeCycle**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0eb46-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb46-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="0eb46-138">В этом разделе описана настройка и проверка единого входа Azure AD в SCC LifeCycle с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0eb46-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0eb46-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SCC LifeCycle является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0eb46-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SCC LifeCycle is tooa user in Azure AD.</span></span> <span data-ttu-id="0eb46-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в SCC LifeCycle должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0eb46-140">In other words, a link relationship between an Azure AD user and hello related user in SCC LifeCycle needs toobe established.</span></span>

<span data-ttu-id="0eb46-141">В SCC LifeCycle, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="0eb46-141">In SCC LifeCycle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0eb46-142">tooconfigure и теста Azure AD единого входа с SCC LifeCycle, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0eb46-142">tooconfigure and test Azure AD single sign-on with SCC LifeCycle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0eb46-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0eb46-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0eb46-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0eb46-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0eb46-145">**[Создание тестового пользователя, прошедшего SCC LifeCycle](#creating-an-scc-lifecycle-test-user)**  -toohave аналог Саймон Britta в SCC LifeCycle, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="0eb46-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - toohave a counterpart of Britta Simon in SCC LifeCycle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0eb46-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0eb46-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0eb46-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0eb46-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0eb46-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb46-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0eb46-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0eb46-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SCC LifeCycle application.</span></span>

<span data-ttu-id="0eb46-150">**tooconfigure Azure AD единого входа с SCC LifeCycle, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0eb46-150">**tooconfigure Azure AD single sign-on with SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="0eb46-151">В hello в hello портала Azure **SCC LifeCycle** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-151">In hello Azure portal, on hello **SCC LifeCycle** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0eb46-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0eb46-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

3. <span data-ttu-id="0eb46-155">На hello **URL-адреса и домена SCC LifeCycle** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0eb46-155">On hello **SCC LifeCycle Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    <span data-ttu-id="0eb46-157">а.</span><span class="sxs-lookup"><span data-stu-id="0eb46-157">a.</span></span> <span data-ttu-id="0eb46-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span><span class="sxs-lookup"><span data-stu-id="0eb46-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span></span>

    <span data-ttu-id="0eb46-159">b.</span><span class="sxs-lookup"><span data-stu-id="0eb46-159">b.</span></span> <span data-ttu-id="0eb46-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="0eb46-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > <span data-ttu-id="0eb46-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0eb46-161">These values are not real.</span></span> <span data-ttu-id="0eb46-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="0eb46-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0eb46-163">Обратитесь к [группа поддержки SCC LifeCycle клиента](mailto:lifecycle.support@scc.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="0eb46-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="0eb46-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0eb46-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

5. <span data-ttu-id="0eb46-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0eb46-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0eb46-168">tooconfigure единого входа на **SCC LifeCycle** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки SCC LifeCycle](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="0eb46-168">tooconfigure single sign-on on **SCC LifeCycle** side, you need toosend hello downloaded **Metadata XML** too[SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span></span> <span data-ttu-id="0eb46-169">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="0eb46-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

     >[!NOTE]
   ><span data-ttu-id="0eb46-170">Единый вход имеет toobe включаемые hello группа поддержки SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0eb46-170">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

> [!TIP]
> <span data-ttu-id="0eb46-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="0eb46-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0eb46-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0eb46-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0eb46-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0eb46-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0eb46-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb46-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="0eb46-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0eb46-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0eb46-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0eb46-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0eb46-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0eb46-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0eb46-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0eb46-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="0eb46-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0eb46-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0eb46-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0eb46-186">а.</span><span class="sxs-lookup"><span data-stu-id="0eb46-186">a.</span></span> <span data-ttu-id="0eb46-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0eb46-188">b.</span><span class="sxs-lookup"><span data-stu-id="0eb46-188">b.</span></span> <span data-ttu-id="0eb46-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0eb46-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0eb46-190">c.</span><span class="sxs-lookup"><span data-stu-id="0eb46-190">c.</span></span> <span data-ttu-id="0eb46-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0eb46-192">d.</span><span class="sxs-lookup"><span data-stu-id="0eb46-192">d.</span></span> <span data-ttu-id="0eb46-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-193">Click **Create**.</span></span>
 
### <a name="creating-an-scc-lifecycle-test-user"></a><span data-ttu-id="0eb46-194">Создание тестового пользователя SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="0eb46-194">Creating an SCC LifeCycle test user</span></span>

<span data-ttu-id="0eb46-195">В порядке tooenable toolog пользователей Azure AD в SCC LifeCycle их необходимо подготовить в SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0eb46-195">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="0eb46-196">Нет элемента действия для вас tooconfigure подготовки пользователей tooSCC жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="0eb46-196">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="0eb46-197">Когда назначенный пользователь пытается toolog в SCC LifeCycle учетная запись SCC LifeCycle создается автоматически при необходимости.</span><span class="sxs-lookup"><span data-stu-id="0eb46-197">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

> [!NOTE]
    > <span data-ttu-id="0eb46-198">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="0eb46-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0eb46-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0eb46-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0eb46-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSCC жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="0eb46-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSCC LifeCycle.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0eb46-202">**tooassign tooSCC Britta Simon жизненного цикла, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="0eb46-202">**tooassign Britta Simon tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="0eb46-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **всех приложений.**</span><span class="sxs-lookup"><span data-stu-id="0eb46-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications.**</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0eb46-205">В списке приложений hello выберите **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-205">In hello applications list, select **SCC LifeCycle**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

3. <span data-ttu-id="0eb46-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0eb46-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-209">Click **Add** button.</span></span> <span data-ttu-id="0eb46-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0eb46-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0eb46-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0eb46-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0eb46-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0eb46-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0eb46-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0eb46-215">Testing single sign-on</span></span>

<span data-ttu-id="0eb46-216">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0eb46-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0eb46-217">При нажатии кнопки hello SCC LifeCycle плитки в панели доступа hello, вы должны получить автоматически вошедшего tooSCC жизненного цикла приложения.</span><span class="sxs-lookup"><span data-stu-id="0eb46-217">When you click hello SCC LifeCycle tile in hello Access Panel, you should get automatically signed-on tooSCC LifeCycle application.</span></span>
<span data-ttu-id="0eb46-218">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0eb46-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0eb46-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0eb46-219">Additional resources</span></span>

* [<span data-ttu-id="0eb46-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0eb46-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0eb46-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0eb46-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_203.png

