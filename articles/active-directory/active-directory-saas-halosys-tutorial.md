---
title: "Руководство по интеграции Azure Active Directory с Halosys | Документация Майкрософт"
description: "Узнайте, как toouse Halosys с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="d7de8-103">Руководство по интеграции Azure Active Directory с Halosys</span><span class="sxs-lookup"><span data-stu-id="d7de8-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="d7de8-104">В этом учебнике вы узнаете, как toointegrate Halosys с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7de8-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7de8-105">Интеграция с Azure AD Halosys предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d7de8-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d7de8-106">Можно управлять в Azure AD, имеющего доступ tooHalosys</span><span class="sxs-lookup"><span data-stu-id="d7de8-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="d7de8-107">Можно включить на пользователей tooautomatically get вошедшего tooHalosys (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7de8-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7de8-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="d7de8-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="d7de8-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7de8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7de8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d7de8-110">Prerequisites</span></span>

<span data-ttu-id="d7de8-111">tooconfigure интеграция Azure AD с Halosys требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d7de8-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="d7de8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d7de8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7de8-113">подписка Halosys с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d7de8-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="d7de8-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d7de8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d7de8-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d7de8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7de8-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="d7de8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d7de8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7de8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d7de8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d7de8-118">Scenario description</span></span>
<span data-ttu-id="d7de8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d7de8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="d7de8-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d7de8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7de8-121">Добавление Halosys из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d7de8-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="d7de8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7de8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="d7de8-123">Добавление Halosys из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d7de8-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="d7de8-124">tooconfigure hello интеграции Halosys в Azure AD, вы должны tooadd Halosys из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d7de8-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d7de8-125">**tooadd Halosys из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d7de8-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7de8-126">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="d7de8-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="d7de8-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="d7de8-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="d7de8-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Приложения][2]

4. <span data-ttu-id="d7de8-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="d7de8-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Приложения][3]

5. <span data-ttu-id="d7de8-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Приложения][4]

6. <span data-ttu-id="d7de8-135">Введите в поле поиска hello **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-135">In hello search box, type **Halosys**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="d7de8-137">В области результатов hello выберите **Halosys**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d7de8-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7de8-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7de8-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7de8-140">В этом разделе описана настройка и проверка единого входа Azure AD в Halosys с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7de8-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7de8-141">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Halosys является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7de8-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="d7de8-142">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Halosys должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d7de8-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="d7de8-143">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Halosys.</span><span class="sxs-lookup"><span data-stu-id="d7de8-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="d7de8-144">tooconfigure и теста Azure AD единого входа с Halosys, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d7de8-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d7de8-145">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d7de8-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d7de8-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d7de8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7de8-147">**[Создание тестового пользователя Halosys](#creating-a-halosys-test-user)**  -toohave аналог Саймон Britta в Halosys, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="d7de8-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d7de8-148">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d7de8-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7de8-149">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d7de8-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7de8-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7de8-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7de8-151">В этом разделе включения Azure AD единого входа в классическом портале hello и настройки единого входа в приложении Halosys.</span><span class="sxs-lookup"><span data-stu-id="d7de8-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="d7de8-152">**tooconfigure Azure AD единого входа с Halosys, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d7de8-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7de8-153">Классическом портале hello на hello **Halosys** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d7de8-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Настройка единого входа][6] 

2. <span data-ttu-id="d7de8-155">На hello **предпочитаемый как toosign пользователей на tooHalosys** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="d7de8-157">На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d7de8-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="d7de8-159">а.</span><span class="sxs-lookup"><span data-stu-id="d7de8-159">a.</span></span> <span data-ttu-id="d7de8-160">В hello **на URL-адрес входа** текстовом поле введите URL-адрес hello, используемого приложением Halosys tooyour toosign на пользователей, используя следующий шаблон hello: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="d7de8-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="d7de8-161">b.In hello **URL-адрес идентификатора** текстовом поле введите URL-адрес hello в hello следующий шаблон: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="d7de8-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="d7de8-162">На hello **настроить единый вход в Halosys** щелкните **загрузить метаданные**, а затем сохраните файл hello на вашем компьютере:</span><span class="sxs-lookup"><span data-stu-id="d7de8-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="d7de8-164">tooget единого входа, настроенному для вашего приложения, обратитесь в службу поддержки Halosys и предоставить им hello следующее:</span><span class="sxs-lookup"><span data-stu-id="d7de8-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="d7de8-165">• hello загружены **файл метаданных**</span><span class="sxs-lookup"><span data-stu-id="d7de8-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="d7de8-166">• hello **URL-адрес единого входа SAML**</span><span class="sxs-lookup"><span data-stu-id="d7de8-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="d7de8-167">Hello классического портала выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Единый вход в Azure AD][10]

7. <span data-ttu-id="d7de8-169">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Единый вход в Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7de8-171">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7de8-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7de8-172">В этом разделе создайте тестового пользователя вызывается Саймон Britta классическом портале hello.</span><span class="sxs-lookup"><span data-stu-id="d7de8-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Создание пользователя Azure AD][20]

<span data-ttu-id="d7de8-174">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d7de8-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7de8-175">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="d7de8-177">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="d7de8-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="d7de8-178">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7de8-180">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="d7de8-182">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello: ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="d7de8-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="d7de8-183">а.</span><span class="sxs-lookup"><span data-stu-id="d7de8-183">a.</span></span> <span data-ttu-id="d7de8-184">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="d7de8-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="d7de8-185">b.</span><span class="sxs-lookup"><span data-stu-id="d7de8-185">b.</span></span> <span data-ttu-id="d7de8-186">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7de8-187">c.</span><span class="sxs-lookup"><span data-stu-id="d7de8-187">c.</span></span> <span data-ttu-id="d7de8-188">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-188">Click **Next**.</span></span>

6.  <span data-ttu-id="d7de8-189">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello: ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="d7de8-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="d7de8-190">а.</span><span class="sxs-lookup"><span data-stu-id="d7de8-190">a.</span></span> <span data-ttu-id="d7de8-191">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="d7de8-192">b.</span><span class="sxs-lookup"><span data-stu-id="d7de8-192">b.</span></span> <span data-ttu-id="d7de8-193">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="d7de8-194">c.</span><span class="sxs-lookup"><span data-stu-id="d7de8-194">c.</span></span> <span data-ttu-id="d7de8-195">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="d7de8-196">d.</span><span class="sxs-lookup"><span data-stu-id="d7de8-196">d.</span></span> <span data-ttu-id="d7de8-197">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="d7de8-198">д.</span><span class="sxs-lookup"><span data-stu-id="d7de8-198">e.</span></span> <span data-ttu-id="d7de8-199">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-199">Click **Next**.</span></span>

7. <span data-ttu-id="d7de8-200">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="d7de8-202">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d7de8-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="d7de8-204">а.</span><span class="sxs-lookup"><span data-stu-id="d7de8-204">a.</span></span> <span data-ttu-id="d7de8-205">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="d7de8-206">b.</span><span class="sxs-lookup"><span data-stu-id="d7de8-206">b.</span></span> <span data-ttu-id="d7de8-207">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="d7de8-208">Создание тестового пользователя Halosys</span><span class="sxs-lookup"><span data-stu-id="d7de8-208">Creating a Halosys test user</span></span>

<span data-ttu-id="d7de8-209">В этом разделе описано, как создать пользователя Britta Simon в приложении Halosys.</span><span class="sxs-lookup"><span data-stu-id="d7de8-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="d7de8-210">Обратитесь Halosys пользователи поддержки team tooadd hello в платформе Halosys hello.</span><span class="sxs-lookup"><span data-stu-id="d7de8-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d7de8-211">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d7de8-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d7de8-212">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooHalosys доступа.</span><span class="sxs-lookup"><span data-stu-id="d7de8-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d7de8-214">**tooassign tooHalosys Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d7de8-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7de8-215">Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="d7de8-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d7de8-217">В списке приложений hello выберите **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-217">In hello applications list, select **Halosys**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="d7de8-219">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-219">In hello menu on hello top, click **Users**.</span></span>

    ![Назначение пользователя][203]

4. <span data-ttu-id="d7de8-221">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="d7de8-222">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="d7de8-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Назначение пользователя][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="d7de8-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d7de8-224">Testing single sign-on</span></span>

<span data-ttu-id="d7de8-225">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="d7de8-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d7de8-226">При нажатии кнопки Halosys плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Halosys приложения.</span><span class="sxs-lookup"><span data-stu-id="d7de8-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d7de8-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d7de8-227">Additional resources</span></span>

* [<span data-ttu-id="d7de8-228">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7de8-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7de8-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d7de8-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
