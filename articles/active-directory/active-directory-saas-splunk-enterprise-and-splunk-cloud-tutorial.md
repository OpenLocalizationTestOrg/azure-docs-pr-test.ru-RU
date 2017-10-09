---
title: "Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и корпоративный Splunk и Splunk облака."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="2af99-103">Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="2af99-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="2af99-104">В этом учебнике вы узнаете, как toointegrate Splunk предприятия и Splunk в облаке в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2af99-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2af99-105">Интеграция с Azure AD Splunk предприятия и в облаке Splunk предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="2af99-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2af99-106">Можно управлять в Azure AD, который имеет доступ tooSplunk предприятия и Splunk в облаке</span><span class="sxs-lookup"><span data-stu-id="2af99-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="2af99-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooSplunk предприятия и в облаке Splunk единого входа (SSO)</span><span class="sxs-lookup"><span data-stu-id="2af99-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="2af99-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="2af99-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="2af99-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2af99-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2af99-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2af99-110">Prerequisites</span></span>

<span data-ttu-id="2af99-111">tooconfigure интеграция Azure AD с Splunk предприятия и Splunk в облаке необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2af99-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="2af99-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2af99-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2af99-113">подписка Splunk Enterprise или Splunk Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="2af99-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="2af99-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="2af99-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="2af99-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="2af99-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2af99-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="2af99-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2af99-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2af99-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2af99-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2af99-118">Scenario description</span></span>
<span data-ttu-id="2af99-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2af99-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="2af99-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="2af99-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2af99-121">Добавление Splunk предприятия и в облаке Splunk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2af99-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="2af99-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2af99-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="2af99-123">Добавление Splunk предприятия и в облаке Splunk из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="2af99-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="2af99-124">tooconfigure hello интеграции Splunk предприятия и Splunk в облаке в Azure AD, необходимо tooadd Splunk предприятия и Splunk облако из списка tooyour hello коллекции из управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2af99-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2af99-125">**tooadd Splunk предприятия и в облаке Splunk из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2af99-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2af99-126">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2af99-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="2af99-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="2af99-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="2af99-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="2af99-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Приложения][2]

4. <span data-ttu-id="2af99-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="2af99-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Приложения][3]

5. <span data-ttu-id="2af99-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="2af99-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Приложения][4]

6. <span data-ttu-id="2af99-135">Введите в поле поиска hello **Splunk Enterprise или облака Splunk**.</span><span class="sxs-lookup"><span data-stu-id="2af99-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="2af99-137">В области результатов hello выберите **Splunk предприятия и в облаке Splunk**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2af99-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2af99-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2af99-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2af99-140">В этом разделе описывается настройка и проверка единого входа Azure AD в Splunk Enterprise и Splunk Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2af99-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2af99-141">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Splunk предприятия и в облаке Splunk является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2af99-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="2af99-142">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Splunk предприятия и в облаке Splunk должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="2af99-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="2af99-143">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Splunk предприятия и Splunk в облаке.</span><span class="sxs-lookup"><span data-stu-id="2af99-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="2af99-144">tooconfigure и теста Azure AD единого входа с Splunk предприятия и Splunk в облаке, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2af99-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2af99-145">**[Настройка Azure AD единого входа](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="2af99-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2af99-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="2af99-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2af99-147">**[Создание тестового пользователя Splunk предприятия и в облаке Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave аналог Саймон Britta Splunk предприятия и Splunk облако, которое является представлением ей связанного toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2af99-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2af99-148">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="2af99-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2af99-149">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2af99-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2af99-150">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="2af99-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2af99-151">В этом разделе Включить единый вход Azure AD в классическом портале hello и Настройка единого входа в приложении предприятия Splunk и Splunk в облаке.</span><span class="sxs-lookup"><span data-stu-id="2af99-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="2af99-152">**tooconfigure Azure AD единого входа с Splunk предприятия и Splunk в облаке, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2af99-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="2af99-153">Классическом портале hello на hello **Splunk предприятия и в облаке Splunk** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="2af99-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Настройка единого входа][6] 

2. <span data-ttu-id="2af99-155">На hello **как toosign пользователей на tooSplunk предприятия и облако Splunk** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2af99-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="2af99-157">На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2af99-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="2af99-159">В hello **на URL-адрес входа** текстовом поле введите URL-адрес hello используется вашим пользователям на toosign tooyour Splunk предприятия и Splunk облачного приложения, используя следующий шаблон hello:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="2af99-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="2af99-160">В hello **идентификатор** текстовом поле введите URL-адрес hello Splunk сервера.</span><span class="sxs-lookup"><span data-stu-id="2af99-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="2af99-161">В hello **URL-адрес ответа** текстовом поле введите URL-адрес hello с hello следующий шаблон:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="2af99-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="2af99-162">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2af99-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="2af99-163">На hello **настроить единый вход в Splunk предприятия и в облаке Splunk** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2af99-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="2af99-165">Нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="2af99-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="2af99-166">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2af99-166">Click **Next**.</span></span>

5. <span data-ttu-id="2af99-167">tooget единого входа, настроенному для вашего приложения, обратитесь к Splunk Enterprise и группа поддержки Splunk облака и укажите их hello следующее:</span><span class="sxs-lookup"><span data-stu-id="2af99-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="2af99-168">загружаются Hello **federaton метаданных**</span><span class="sxs-lookup"><span data-stu-id="2af99-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="2af99-169">Hello классического портала выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2af99-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Единый вход в Azure AD][10]

7. <span data-ttu-id="2af99-171">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="2af99-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Единый вход в Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2af99-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2af99-173">Create an Azure AD test user</span></span>
<span data-ttu-id="2af99-174">В этом разделе создайте тестового пользователя вызывается Саймон Britta классическом портале hello.</span><span class="sxs-lookup"><span data-stu-id="2af99-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="2af99-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2af99-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2af99-177">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2af99-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="2af99-179">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="2af99-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="2af99-180">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2af99-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2af99-182">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2af99-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="2af99-184">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2af99-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="2af99-186">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="2af99-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="2af99-187">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2af99-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="2af99-188">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2af99-188">Click **Next**.</span></span>

6.  <span data-ttu-id="2af99-189">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2af99-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="2af99-191">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2af99-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="2af99-192">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2af99-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="2af99-193">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2af99-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="2af99-194">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2af99-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="2af99-195">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2af99-195">Click **Next**.</span></span>

7. <span data-ttu-id="2af99-196">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="2af99-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="2af99-198">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2af99-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="2af99-200">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="2af99-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="2af99-201">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="2af99-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="2af99-202">Создание тестового пользователя Splunk Enterprise и Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="2af99-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="2af99-203">В этом разделе описано, как создать пользователя Britta Simon в Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="2af99-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="2af99-204">Обратитесь Splunk предприятия и в облаке Splunk поддержки команды tooadd hello пользователей hello Splunk предприятия и Splunk облачной платформы.</span><span class="sxs-lookup"><span data-stu-id="2af99-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2af99-205">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="2af99-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2af99-206">В этом разделе включите Саймон Britta toouse SSOy Azure предоставление своего предприятия tooSplunk доступа и Splunk в облаке.</span><span class="sxs-lookup"><span data-stu-id="2af99-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="2af99-208">**tooassign Britta Simon tooSplunk предприятия и облака Splunk выполняют hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="2af99-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="2af99-209">Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="2af99-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2af99-211">В списке приложений hello выберите **Splunk предприятия и в облаке Splunk**.</span><span class="sxs-lookup"><span data-stu-id="2af99-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="2af99-213">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2af99-213">In hello menu on hello top, click **Users**.</span></span>

    ![Назначение пользователя][203]

4. <span data-ttu-id="2af99-215">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2af99-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="2af99-216">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="2af99-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="2af99-218">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2af99-218">Test single sign-on</span></span>

<span data-ttu-id="2af99-219">В этом разделе тестирования вашей SSOonfiguration Azure AD, с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="2af99-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="2af99-220">При нажатии кнопки hello Splunk предприятия и облака Splunk плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Splunk предприятия и Splunk облачных приложений.</span><span class="sxs-lookup"><span data-stu-id="2af99-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2af99-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2af99-221">Additional resources</span></span>

* [<span data-ttu-id="2af99-222">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2af99-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2af99-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2af99-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
