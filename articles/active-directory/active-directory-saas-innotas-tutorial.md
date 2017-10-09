---
title: "Учебник. Интеграция Azure Active Directory с Innotas | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Innotas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 31d787a351fe9362e35afee28a292c927f43702d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="8fef5-103">Руководство. Интеграция Azure Active Directory с Innotas</span><span class="sxs-lookup"><span data-stu-id="8fef5-103">Tutorial: Azure Active Directory integration with Innotas</span></span>

<span data-ttu-id="8fef5-104">В этом учебнике вы узнаете, как toointegrate Innotas с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8fef5-104">In this tutorial, you learn how toointegrate Innotas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8fef5-105">Интеграция Innotas с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8fef5-105">Integrating Innotas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8fef5-106">Можно управлять в Azure AD, имеющего доступ tooInnotas</span><span class="sxs-lookup"><span data-stu-id="8fef5-106">You can control in Azure AD who has access tooInnotas</span></span>
- <span data-ttu-id="8fef5-107">Можно включить на пользователей tooautomatically get вошедшего tooInnotas (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fef5-107">You can enable your users tooautomatically get signed-on tooInnotas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8fef5-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8fef5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8fef5-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8fef5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fef5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8fef5-110">Prerequisites</span></span>

<span data-ttu-id="8fef5-111">tooconfigure интеграция Azure AD с Innotas требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8fef5-111">tooconfigure Azure AD integration with Innotas, you need hello following items:</span></span>

- <span data-ttu-id="8fef5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8fef5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8fef5-113">подписка Innotas с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8fef5-113">An Innotas single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8fef5-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8fef5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8fef5-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8fef5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8fef5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8fef5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8fef5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8fef5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8fef5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8fef5-118">Scenario description</span></span>

<span data-ttu-id="8fef5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8fef5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8fef5-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8fef5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8fef5-121">Добавление Innotas из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8fef5-121">Adding Innotas from hello gallery</span></span>
2. <span data-ttu-id="8fef5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fef5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innotas-from-hello-gallery"></a><span data-ttu-id="8fef5-123">Добавление Innotas из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8fef5-123">Adding Innotas from hello gallery</span></span>
<span data-ttu-id="8fef5-124">tooconfigure hello интеграции Innotas в Azure AD, вы должны tooadd Innotas из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8fef5-124">tooconfigure hello integration of Innotas into Azure AD, you need tooadd Innotas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8fef5-125">**tooadd Innotas из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8fef5-125">**tooadd Innotas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fef5-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8fef5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8fef5-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8fef5-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8fef5-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8fef5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8fef5-133">Введите в поле поиска hello **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-133">In hello search box, type **Innotas**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_search.png)

5. <span data-ttu-id="8fef5-135">В панели результатов hello выберите **Innotas**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8fef5-135">In hello results panel, select **Innotas**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8fef5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fef5-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="8fef5-138">В этом разделе описана настройка и проверка единого входа Azure AD с Innotas с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fef5-138">In this section, you configure and test Azure AD single sign-on with Innotas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8fef5-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Innotas является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fef5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Innotas is tooa user in Azure AD.</span></span> <span data-ttu-id="8fef5-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Innotas должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8fef5-140">In other words, a link relationship between an Azure AD user and hello related user in Innotas needs toobe established.</span></span>

<span data-ttu-id="8fef5-141">В Innotas, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8fef5-141">In Innotas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8fef5-142">tooconfigure и теста Azure AD единого входа с Innotas, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8fef5-142">tooconfigure and test Azure AD single sign-on with Innotas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8fef5-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8fef5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8fef5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8fef5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8fef5-145">**[Создание тестового пользователя, прошедшего Innotas](#creating-an-innotas-test-user)**  -toohave аналог Саймон Britta в Innotas, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8fef5-145">**[Creating an Innotas test user](#creating-an-innotas-test-user)** - toohave a counterpart of Britta Simon in Innotas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8fef5-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8fef5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8fef5-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8fef5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8fef5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fef5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8fef5-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Innotas приложения.</span><span class="sxs-lookup"><span data-stu-id="8fef5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Innotas application.</span></span>

<span data-ttu-id="8fef5-150">**Azure AD tooconfigure единого входа с Innotas, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8fef5-150">**tooconfigure Azure AD single sign-on with Innotas, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fef5-151">В hello в hello портала Azure **Innotas** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-151">In hello Azure portal, on hello **Innotas** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8fef5-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8fef5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_samlbase.png)

3. <span data-ttu-id="8fef5-155">На hello **URL-адреса и домена Innotas** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8fef5-155">On hello **Innotas Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_url.png)

    <span data-ttu-id="8fef5-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.Innotas.com`</span><span class="sxs-lookup"><span data-stu-id="8fef5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Innotas.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8fef5-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="8fef5-158">This value is not real.</span></span> <span data-ttu-id="8fef5-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8fef5-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8fef5-160">Обратитесь к [группа поддержки клиент Innotas](https://www.innotas.com/contact) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="8fef5-160">Contact [Innotas Client support team](https://www.innotas.com/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="8fef5-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8fef5-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_certificate.png) 

5. <span data-ttu-id="8fef5-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8fef5-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-innotas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8fef5-165">tooconfigure единого входа на **Innotas** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки Innotas](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="8fef5-165">tooconfigure single sign-on on **Innotas** side, you need toosend hello downloaded **Metadata XML** too[Innotas support team](https://www.innotas.com/contact).</span></span> <span data-ttu-id="8fef5-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="8fef5-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8fef5-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8fef5-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8fef5-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8fef5-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8fef5-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8fef5-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8fef5-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fef5-170">Creating an Azure AD test user</span></span>

<span data-ttu-id="8fef5-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8fef5-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8fef5-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8fef5-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fef5-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8fef5-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8fef5-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8fef5-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8fef5-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8fef5-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8fef5-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8fef5-182">а.</span><span class="sxs-lookup"><span data-stu-id="8fef5-182">a.</span></span> <span data-ttu-id="8fef5-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8fef5-184">b.</span><span class="sxs-lookup"><span data-stu-id="8fef5-184">b.</span></span> <span data-ttu-id="8fef5-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8fef5-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8fef5-186">c.</span><span class="sxs-lookup"><span data-stu-id="8fef5-186">c.</span></span> <span data-ttu-id="8fef5-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8fef5-188">d.</span><span class="sxs-lookup"><span data-stu-id="8fef5-188">d.</span></span> <span data-ttu-id="8fef5-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-189">Click **Create**.</span></span>
 
### <a name="creating-an-innotas-test-user"></a><span data-ttu-id="8fef5-190">Создание тестового пользователя Innotas</span><span class="sxs-lookup"><span data-stu-id="8fef5-190">Creating an Innotas test user</span></span>

<span data-ttu-id="8fef5-191">Нет элемента действия для вас tooconfigure подготовки пользователей tooInnotas.</span><span class="sxs-lookup"><span data-stu-id="8fef5-191">There is no action item for you tooconfigure user provisioning tooInnotas.</span></span>  
<span data-ttu-id="8fef5-192">Когда назначенный пользователь пытается toolog в tooInnotas, с помощью панели доступа hello, Innotas проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="8fef5-192">When an assigned user tries toolog in tooInnotas using hello access panel, Innotas checks whether hello user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="8fef5-193">Если учетная запись пользователя отсутствует, Innotas автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="8fef5-193">If there is no user account available yet, it is automatically created by Innotas.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8fef5-194">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8fef5-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8fef5-195">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooInnotas доступа.</span><span class="sxs-lookup"><span data-stu-id="8fef5-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInnotas.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8fef5-197">**tooassign tooInnotas Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8fef5-197">**tooassign Britta Simon tooInnotas, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fef5-198">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8fef5-200">В списке приложений hello выберите **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-200">In hello applications list, select **Innotas**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_app.png) 

3. <span data-ttu-id="8fef5-202">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8fef5-204">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-204">Click **Add** button.</span></span> <span data-ttu-id="8fef5-205">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8fef5-207">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8fef5-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8fef5-208">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8fef5-209">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8fef5-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8fef5-210">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8fef5-210">Testing single sign-on</span></span>

<span data-ttu-id="8fef5-211">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8fef5-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8fef5-212">При нажатии кнопки Innotas плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Innotas приложения.</span><span class="sxs-lookup"><span data-stu-id="8fef5-212">When you click hello Innotas tile in hello Access Panel, you should get automatically signed-on tooyour Innotas application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8fef5-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8fef5-213">Additional resources</span></span>

* [<span data-ttu-id="8fef5-214">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fef5-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8fef5-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8fef5-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_203.png

