---
title: "Руководство по интеграции Azure Active Directory с SmarterU | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="4d933-103">Учебник. Интеграция Azure Active Directory со SmarterU</span><span class="sxs-lookup"><span data-stu-id="4d933-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="4d933-104">В этом учебнике вы узнаете, как toointegrate SmarterU с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d933-104">In this tutorial, you learn how toointegrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d933-105">Интеграция SmarterU с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4d933-105">Integrating SmarterU with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4d933-106">Можно управлять в Azure AD, имеющего доступ tooSmarterU</span><span class="sxs-lookup"><span data-stu-id="4d933-106">You can control in Azure AD who has access tooSmarterU</span></span>
- <span data-ttu-id="4d933-107">Можно включить на пользователей tooautomatically get вошедшего tooSmarterU (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d933-107">You can enable your users tooautomatically get signed-on tooSmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d933-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4d933-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4d933-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d933-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d933-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4d933-110">Prerequisites</span></span>

<span data-ttu-id="4d933-111">tooconfigure интеграция Azure AD со SmarterU требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4d933-111">tooconfigure Azure AD integration with SmarterU, you need hello following items:</span></span>

- <span data-ttu-id="4d933-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4d933-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d933-113">подписка SmarterU с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4d933-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d933-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4d933-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d933-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="4d933-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d933-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4d933-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d933-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d933-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d933-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4d933-118">Scenario description</span></span>
<span data-ttu-id="4d933-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4d933-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d933-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="4d933-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d933-121">Добавление SmarterU из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4d933-121">Adding SmarterU from hello gallery</span></span>
2. <span data-ttu-id="4d933-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d933-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-hello-gallery"></a><span data-ttu-id="4d933-123">Добавление SmarterU из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4d933-123">Adding SmarterU from hello gallery</span></span>
<span data-ttu-id="4d933-124">tooconfigure hello интеграции SmarterU в Azure AD, вы должны tooadd SmarterU из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4d933-124">tooconfigure hello integration of SmarterU into Azure AD, you need tooadd SmarterU from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4d933-125">**tooadd SmarterU из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d933-125">**tooadd SmarterU from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d933-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4d933-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d933-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="4d933-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4d933-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4d933-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4d933-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4d933-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4d933-133">Введите в поле поиска hello **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="4d933-133">In hello search box, type **SmarterU**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="4d933-135">В панели результатов hello выберите **SmarterU**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4d933-135">In hello results panel, select **SmarterU**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d933-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d933-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d933-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение SmarterU с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d933-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4d933-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SmarterU является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d933-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SmarterU is tooa user in Azure AD.</span></span> <span data-ttu-id="4d933-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в SmarterU должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="4d933-140">In other words, a link relationship between an Azure AD user and hello related user in SmarterU needs toobe established.</span></span>

<span data-ttu-id="4d933-141">В SmarterU, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="4d933-141">In SmarterU, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4d933-142">tooconfigure и теста Azure AD единого входа с SmarterU, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4d933-142">tooconfigure and test Azure AD single sign-on with SmarterU, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4d933-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="4d933-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4d933-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="4d933-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d933-145">**[Создание тестового пользователя SmarterU](#creating-a-smarteru-test-user)**  -toohave аналог Саймон Britta в SmarterU, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="4d933-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - toohave a counterpart of Britta Simon in SmarterU that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d933-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="4d933-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d933-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4d933-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d933-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d933-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d933-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в SmarterU приложения.</span><span class="sxs-lookup"><span data-stu-id="4d933-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="4d933-150">**tooconfigure Azure AD единого входа со SmarterU, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d933-150">**tooconfigure Azure AD single sign-on with SmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d933-151">В hello в hello портала Azure **SmarterU** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4d933-151">In hello Azure portal, on hello **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4d933-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="4d933-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="4d933-155">На hello **URL-адреса и домена SmarterU** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4d933-155">On hello **SmarterU Domain and URLs** section, perform hello following steps:</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="4d933-157">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="4d933-157">In hello **Identifier** textbox, type hello URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="4d933-158">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4d933-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="4d933-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4d933-160">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4d933-162">В другом окне браузера войти в корпоративный сайт SmarterU tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="4d933-162">In a different web browser window, log in tooyour SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="4d933-163">Щелкните hello панели инструментов в верхней части hello **параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="4d933-163">In hello toolbar on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="4d933-164">![Параметры учетной записи](./media/active-directory-saas-smarteru-tutorial/IC777326.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="4d933-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="4d933-165">На странице настройки учетной записи hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="4d933-165">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="4d933-166">![Внешняя авторизация](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Внешняя авторизация")</span><span class="sxs-lookup"><span data-stu-id="4d933-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="4d933-167">а.</span><span class="sxs-lookup"><span data-stu-id="4d933-167">a.</span></span> <span data-ttu-id="4d933-168">Установите флажок **Включить внешнюю авторизацию**.</span><span class="sxs-lookup"><span data-stu-id="4d933-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="4d933-169">b.</span><span class="sxs-lookup"><span data-stu-id="4d933-169">b.</span></span> <span data-ttu-id="4d933-170">В hello **управления входом в систему главного** раздел, выберите hello **SmarterU** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4d933-170">In hello **Master Login Control** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="4d933-171">c.</span><span class="sxs-lookup"><span data-stu-id="4d933-171">c.</span></span> <span data-ttu-id="4d933-172">В hello **входа пользователя по умолчанию** раздел, выберите hello **SmarterU** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4d933-172">In hello **User Default Login** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="4d933-173">d.</span><span class="sxs-lookup"><span data-stu-id="4d933-173">d.</span></span> <span data-ttu-id="4d933-174">Выберите **Включить Okta**.</span><span class="sxs-lookup"><span data-stu-id="4d933-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="4d933-175">д.</span><span class="sxs-lookup"><span data-stu-id="4d933-175">e.</span></span> <span data-ttu-id="4d933-176">Скопируйте содержимое hello hello скачанный файл метаданных, а затем вставьте его в hello **метаданные Okta** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="4d933-176">Copy hello content of hello downloaded metadata file, and then paste it into hello **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="4d933-177">f.</span><span class="sxs-lookup"><span data-stu-id="4d933-177">f.</span></span> <span data-ttu-id="4d933-178">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4d933-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4d933-179">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="4d933-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4d933-180">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="4d933-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4d933-181">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d933-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d933-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d933-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d933-183">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4d933-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4d933-185">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d933-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d933-186">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4d933-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d933-188">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4d933-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d933-190">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="4d933-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d933-192">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4d933-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d933-194">а.</span><span class="sxs-lookup"><span data-stu-id="4d933-194">a.</span></span> <span data-ttu-id="4d933-195">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d933-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d933-196">b.</span><span class="sxs-lookup"><span data-stu-id="4d933-196">b.</span></span> <span data-ttu-id="4d933-197">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4d933-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d933-198">c.</span><span class="sxs-lookup"><span data-stu-id="4d933-198">c.</span></span> <span data-ttu-id="4d933-199">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="4d933-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4d933-200">d.</span><span class="sxs-lookup"><span data-stu-id="4d933-200">d.</span></span> <span data-ttu-id="4d933-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4d933-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="4d933-202">Создание тестового пользователя SmarterU</span><span class="sxs-lookup"><span data-stu-id="4d933-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="4d933-203">Пользователи toolog tooenable Azure AD в tooSmarterU, их необходимо подготовить в SmarterU.</span><span class="sxs-lookup"><span data-stu-id="4d933-203">tooenable Azure AD users toolog in tooSmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="4d933-204">В случае SmarterU подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="4d933-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="4d933-205">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d933-205">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d933-206">Войдите в tooyour **SmarterU** клиента.</span><span class="sxs-lookup"><span data-stu-id="4d933-206">Log in tooyour **SmarterU** tenant.</span></span>

2. <span data-ttu-id="4d933-207">Go слишком**пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4d933-207">Go too**Users**.</span></span>

3. <span data-ttu-id="4d933-208">В разделе hello пользователя выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4d933-208">In hello user section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4d933-209">![Новый пользователь](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="4d933-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="4d933-210">а.</span><span class="sxs-lookup"><span data-stu-id="4d933-210">a.</span></span> <span data-ttu-id="4d933-211">Щелкните **+ Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="4d933-211">Click **+User**.</span></span>
    
    <span data-ttu-id="4d933-212">b.</span><span class="sxs-lookup"><span data-stu-id="4d933-212">b.</span></span> <span data-ttu-id="4d933-213">Тип hello связанные значения атрибутов учетной записи пользователя hello Azure AD в следующие текстовые поля hello: **основной адрес электронной почты**, **идентификатор сотрудника**, **пароль**,  **Проверка пароля**, **заданное имя**, **Фамилия**.</span><span class="sxs-lookup"><span data-stu-id="4d933-213">Type hello related attribute values of hello Azure AD user account into hello following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="4d933-214">c.</span><span class="sxs-lookup"><span data-stu-id="4d933-214">c.</span></span> <span data-ttu-id="4d933-215">Нажмите **Активный**.</span><span class="sxs-lookup"><span data-stu-id="4d933-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="4d933-216">d.</span><span class="sxs-lookup"><span data-stu-id="4d933-216">d.</span></span> <span data-ttu-id="4d933-217">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4d933-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="4d933-218">Можно использовать любые другие SmarterU пользователя средства создания учетных записей или интерфейсы API, предоставляемые SmarterU tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="4d933-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4d933-219">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="4d933-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4d933-220">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSmarterU доступа.</span><span class="sxs-lookup"><span data-stu-id="4d933-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmarterU.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4d933-222">**tooassign tooSmarterU Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d933-222">**tooassign Britta Simon tooSmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d933-223">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4d933-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4d933-225">В списке приложений hello выберите **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="4d933-225">In hello applications list, select **SmarterU**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="4d933-227">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="4d933-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4d933-229">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4d933-229">Click **Add** button.</span></span> <span data-ttu-id="4d933-230">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4d933-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4d933-232">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="4d933-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4d933-233">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4d933-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d933-234">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4d933-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d933-235">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4d933-235">Testing single sign-on</span></span>

<span data-ttu-id="4d933-236">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="4d933-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="4d933-237">При нажатии кнопки hello SmarterU плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour SmarterU приложения.</span><span class="sxs-lookup"><span data-stu-id="4d933-237">When you click hello SmarterU tile in hello Access Panel, you should get automatically signed-on tooyour SmarterU application.</span></span>
<span data-ttu-id="4d933-238">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d933-238">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="4d933-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4d933-239">Additional resources</span></span>

* [<span data-ttu-id="4d933-240">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d933-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d933-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d933-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

