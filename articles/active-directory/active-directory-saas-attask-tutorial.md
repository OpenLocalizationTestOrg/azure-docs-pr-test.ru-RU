---
title: "Учебник: Интеграция Azure Active Directory с @Task| Документы Microsoft"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="7a2bb-103">Учебник. Интеграция Azure Active Directory с @Task</span><span class="sxs-lookup"><span data-stu-id="7a2bb-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="7a2bb-104">Hello цель этого учебника — tooshow вы как toointegrate @Task с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a2bb-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="7a2bb-105">Интеграция @Task с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="7a2bb-106">Можно управлять в Azure AD, у которого есть доступtoo@Task</span><span class="sxs-lookup"><span data-stu-id="7a2bb-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="7a2bb-107">Позволяет пользователям получить tooautomatically вошедшего too@Task (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a2bb-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="7a2bb-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="7a2bb-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="7a2bb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a2bb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a2bb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a2bb-110">Prerequisites</span></span>
<span data-ttu-id="7a2bb-111">Интеграция Azure AD tooconfigure с @Task, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="7a2bb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7a2bb-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7a2bb-113">подписка на @Task с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a2bb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="7a2bb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7a2bb-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7a2bb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a2bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="7a2bb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7a2bb-118">Scenario Description</span></span>
<span data-ttu-id="7a2bb-119">Hello цель этого учебника — tooenable tootest Azure AD единого входа в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="7a2bb-120">Hello сценарий, описанный в этом учебнике состоит из трех основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="7a2bb-121">Добавление @Task из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7a2bb-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="7a2bb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a2bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="7a2bb-123">Добавление @Task из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7a2bb-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="7a2bb-124">Интеграция hello tooconfigure @Task в Azure AD необходимо tooadd @Task из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7a2bb-125">**tooadd @Task из галереи hello выполнения hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="7a2bb-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a2bb-126">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="7a2bb-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="7a2bb-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Приложения][2] 
4. <span data-ttu-id="7a2bb-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Приложения][3] 
5. <span data-ttu-id="7a2bb-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Приложения][4] 
6. <span data-ttu-id="7a2bb-135">Введите в поле поиска hello  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="7a2bb-135">In hello search box, type **@Task**.</span></span>
   
    ![Приложения][5] 
7. <span data-ttu-id="7a2bb-137">В области результатов hello выберите  **@Task** и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Приложения][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a2bb-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a2bb-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a2bb-140">Hello цель этого раздела — tooshow вы как tooconfigure и тестирования Azure AD single входа с @Task основании тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="7a2bb-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a2bb-141">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в @Task tooan пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="7a2bb-142">Другими словами, связи между пользователя Azure AD и связанных пользователей hello в @Task должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="7a2bb-143">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в @Task.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="7a2bb-144">tooconfigure и Azure AD тестирования единого входа с @Task, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7a2bb-145">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7a2bb-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a2bb-147">**[Создание @Tasktest пользователя](#creating-a-halogen-software-test-user)**  -toohave a аналог Саймон Britta в @Taskthat является представлением ей связанного toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7a2bb-148">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a2bb-149">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a2bb-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a2bb-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="7a2bb-151">Цель этого раздела Hello является tooenable Azure AD единого входа в hello классический портал Azure и tooconfigure единый вход в ваш @Task приложения.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="7a2bb-152">**tooconfigure Azure AD единого входа с @Task, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="7a2bb-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a2bb-153">В классический портал Azure, на hello hello  **@Task**  странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**  диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][6] 
2. <span data-ttu-id="7a2bb-155">На hello **как бы вы как toosign пользователей на too@Task**  выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Единый вход в Azure AD][7] 
3. <span data-ttu-id="7a2bb-157">На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Настройка параметров приложения][8] 
   
     <span data-ttu-id="7a2bb-159">а.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-159">a.</span></span> <span data-ttu-id="7a2bb-160">В hello **на URL-адрес входа** textbox hello введите URL-адрес, используемые вашей пользователей на toosign tooyour @Task приложения (например:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="7a2bb-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="7a2bb-161">b.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-161">b.</span></span> <span data-ttu-id="7a2bb-162">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-162">Click **Next**.</span></span>
4. <span data-ttu-id="7a2bb-163">На hello **настроить единый вход в @Task**  щелкните **загрузить метаданные**, сохраните файл метаданных hello на локальном компьютере и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Что такое Azure AD Connect?][9] 
5. <span data-ttu-id="7a2bb-165">Tooyour входа @Task сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="7a2bb-166">Go слишком**единого входа на конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="7a2bb-167">На hello **Single Sign-On** диалоговое окно, выполните следующие шаги hello</span><span class="sxs-lookup"><span data-stu-id="7a2bb-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Настройка единого входа][23]
   
    <span data-ttu-id="7a2bb-169">а.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-169">a.</span></span> <span data-ttu-id="7a2bb-170">Для параметра **Тип** выберите значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="7a2bb-171">b.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-171">b.</span></span> <span data-ttu-id="7a2bb-172">Выберите **идентификатор поставщика службы**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="7a2bb-173">c.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-173">c.</span></span> <span data-ttu-id="7a2bb-174">На hello классического портала Azure скопируйте hello **URL-адрес удаленного входа**и вставьте его в hello **URL-адрес входа портала** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="7a2bb-175">d.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-175">d.</span></span> <span data-ttu-id="7a2bb-176">На hello классического портала Azure скопируйте hello **URL-адрес службы единого выхода**, а затем вставьте его в hello **URL-адрес выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="7a2bb-177">д.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-177">e.</span></span> <span data-ttu-id="7a2bb-178">На hello классического портала Azure скопируйте hello **URL-адрес изменения пароля**и вставьте его в hello **URL-адрес изменения пароля** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="7a2bb-179">f.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-179">f.</span></span> <span data-ttu-id="7a2bb-180">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-180">Click **Save**.</span></span>
8. <span data-ttu-id="7a2bb-181">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Что такое Azure AD Connect?][10]
9. <span data-ttu-id="7a2bb-183">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Что такое Azure AD Connect?][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a2bb-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a2bb-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a2bb-186">Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Создание пользователя Azure AD][20]

<span data-ttu-id="7a2bb-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7a2bb-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a2bb-189">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="7a2bb-191">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="7a2bb-192">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="7a2bb-194">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="7a2bb-196">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="7a2bb-198">а.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-198">a.</span></span> <span data-ttu-id="7a2bb-199">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="7a2bb-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="7a2bb-200">b.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-200">b.</span></span> <span data-ttu-id="7a2bb-201">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="7a2bb-202">c.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-202">c.</span></span> <span data-ttu-id="7a2bb-203">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-203">Click **Next**.</span></span>
6. <span data-ttu-id="7a2bb-204">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="7a2bb-206">а.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-206">a.</span></span> <span data-ttu-id="7a2bb-207">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="7a2bb-208">b.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-208">b.</span></span> <span data-ttu-id="7a2bb-209">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="7a2bb-210">c.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-210">c.</span></span> <span data-ttu-id="7a2bb-211">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="7a2bb-212">d.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-212">d.</span></span> <span data-ttu-id="7a2bb-213">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="7a2bb-214">д.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-214">e.</span></span> <span data-ttu-id="7a2bb-215">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-215">Click **Next**.</span></span>

7. <span data-ttu-id="7a2bb-216">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="7a2bb-218">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7a2bb-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="7a2bb-220">а.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-220">a.</span></span> <span data-ttu-id="7a2bb-221">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="7a2bb-222">b.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-222">b.</span></span> <span data-ttu-id="7a2bb-223">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="7a2bb-224">Создание тестового пользователя @Task</span><span class="sxs-lookup"><span data-stu-id="7a2bb-224">Creating an @Task test user</span></span>
<span data-ttu-id="7a2bb-225">Hello цель этого раздела — toocreate пользователя с именем Саймон Britta @Task.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="7a2bb-226">**toocreate пользователя с именем Саймон Britta @Task, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="7a2bb-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a2bb-227">Войдите на tooyour @Task сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="7a2bb-228">В меню в верхней части hello hello выберите **людей**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="7a2bb-229">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="7a2bb-230">В диалоговом окне Новый пользователь hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя @Task][21] 
   
    <span data-ttu-id="7a2bb-232">а.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-232">a.</span></span> <span data-ttu-id="7a2bb-233">В hello **имя** текстовое поле, введите «Britta».</span><span class="sxs-lookup"><span data-stu-id="7a2bb-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="7a2bb-234">b.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-234">b.</span></span> <span data-ttu-id="7a2bb-235">В hello **Фамилия** текстовое поле, введите «Simon».</span><span class="sxs-lookup"><span data-stu-id="7a2bb-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="7a2bb-236">c.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-236">c.</span></span> <span data-ttu-id="7a2bb-237">В hello **адрес электронной почты** текстовом поле введите адрес электронной почты Britta Simon в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="7a2bb-238">d.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-238">d.</span></span> <span data-ttu-id="7a2bb-239">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7a2bb-240">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7a2bb-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="7a2bb-241">Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа, предоставляя свой доступ too@Task.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7a2bb-243">**tooassign Britta Simon too@Task, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="7a2bb-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a2bb-244">Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Назначение пользователя][201] 
2. <span data-ttu-id="7a2bb-246">В списке приложений hello выберите  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="7a2bb-246">In hello applications list, select **@Task**.</span></span>
   
    ![Назначение пользователя][202] 
3. <span data-ttu-id="7a2bb-248">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Назначение пользователя][203] 
4. <span data-ttu-id="7a2bb-250">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7a2bb-251">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="7a2bb-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7a2bb-253">Testing Single Sign-On</span></span>
<span data-ttu-id="7a2bb-254">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="7a2bb-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="7a2bb-255">При нажатии кнопки hello @Task плитки в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour @Task приложения.</span><span class="sxs-lookup"><span data-stu-id="7a2bb-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a2bb-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7a2bb-256">Additional Resources</span></span>
* [<span data-ttu-id="7a2bb-257">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a2bb-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a2bb-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a2bb-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






