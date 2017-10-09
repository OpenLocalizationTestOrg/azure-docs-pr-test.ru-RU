---
title: "Руководство. Интеграция Azure Active Directory с приложением Bynder | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="14192-103">Руководство. Интеграция Azure Active Directory с Bynder</span><span class="sxs-lookup"><span data-stu-id="14192-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="14192-104">Hello цель этого учебника — tooshow вы как toointegrate Bynder с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14192-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14192-105">Интеграция с Azure AD Bynder предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="14192-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="14192-106">Можно управлять в Azure AD, имеющего доступ tooBynder</span><span class="sxs-lookup"><span data-stu-id="14192-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="14192-107">Можно включить на пользователей tooautomatically get tooBynder вошедшего единого входа (SSO) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="14192-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="14192-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="14192-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="14192-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="14192-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14192-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="14192-110">Prerequisites</span></span>
<span data-ttu-id="14192-111">tooconfigure интеграция Azure AD с Bynder требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="14192-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="14192-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="14192-112">An Azure AD subscription</span></span>
* <span data-ttu-id="14192-113">подписка на Bynder с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="14192-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="14192-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="14192-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="14192-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="14192-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="14192-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="14192-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="14192-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14192-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14192-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="14192-118">Scenario description</span></span>
<span data-ttu-id="14192-119">Hello цель этого учебника — tooenable вы tootest Microsoft Azure AD, единого входа в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="14192-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="14192-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="14192-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14192-121">Добавление Bynder из галереи hello</span><span class="sxs-lookup"><span data-stu-id="14192-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="14192-122">Настройка и проверка единого входа Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14192-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="14192-123">Добавление Bynder из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="14192-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="14192-124">tooconfigure hello интеграции Bynder в Azure AD, вы должны tooadd Bynder из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="14192-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="14192-125">**tooadd Bynder из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="14192-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="14192-126">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14192-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="14192-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="14192-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="14192-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="14192-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Приложения][2]
4. <span data-ttu-id="14192-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="14192-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Приложения][3]
5. <span data-ttu-id="14192-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="14192-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Приложения][4]
6. <span data-ttu-id="14192-135">Введите в поле поиска hello **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="14192-135">In hello search box, type **Bynder**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="14192-137">В панели результатов hello выберите **Bynder**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="14192-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![При выборе приложение hello в галерее hello](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="14192-139">Настройка и проверка единого входа Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="14192-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="14192-140">Цель этого раздела Hello является tooshow как tooconfigure и тестирования единого входа Microsoft Azure AD, с Bynder на основе тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="14192-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="14192-141">Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в Bynder tooan пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14192-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="14192-142">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Bynder должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="14192-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="14192-143">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Bynder.</span><span class="sxs-lookup"><span data-stu-id="14192-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="14192-144">tooconfigure и тестирования единого входа Microsoft Azure AD, с Bynder, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="14192-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="14192-145">**[Настройка Microsoft Azure AD единого входа](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="14192-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="14192-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="14192-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="14192-147">**[Создание тестового пользователя Bynder](#creating-a-bynder-test-user)**  -toohave аналог Саймон Britta в Bynder, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="14192-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="14192-148">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable toouse Britta Simon Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="14192-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="14192-149">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="14192-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="14192-150">Настройка единого входа Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="14192-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="14192-151">В этом разделе включить Microsoft Azure AD, единого входа в классическом портале hello и настройки единого входа в вашем приложении Bynder.</span><span class="sxs-lookup"><span data-stu-id="14192-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="14192-152">**tooconfigure Microsoft Azure AD и единого входа с Bynder, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="14192-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="14192-153">Классическом портале hello на hello **Bynder** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="14192-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][6] 
2. <span data-ttu-id="14192-155">На hello **предпочитаемый как toosign пользователей на tooBynder** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14192-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="14192-157">На hello **Настройка параметров приложения** странице диалогового окна, при желании tooconfigure приложения hello в **режиме, инициированный IDP**, выполните следующие шаги hello и нажмите кнопку **Далее**:</span><span class="sxs-lookup"><span data-stu-id="14192-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="14192-159">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="14192-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="14192-160">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14192-160">Click **Next**.</span></span>
4. <span data-ttu-id="14192-161">При необходимости приложение hello tooconfigure в **режиме, инициируемая SP** на hello **Настройка параметров приложения** странице диалогового окна, а затем нажмите кнопку hello **«Дополнительные параметры (необязательно) Показать»**, а затем введите hello **на URL-адрес входа** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14192-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="14192-163">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="14192-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="14192-164">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14192-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="14192-165">Hello для hello на URL-адрес входа в этом учебнике значение просто placeholfer.</span><span class="sxs-lookup"><span data-stu-id="14192-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="14192-166">Фактический vlaue tooget hello для вашей среды обратитесь к Bynder.</span><span class="sxs-lookup"><span data-stu-id="14192-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="14192-167">На hello **настроить единый вход в Bynder** выполните следующие шаги hello и нажмите кнопку **Далее**:</span><span class="sxs-lookup"><span data-stu-id="14192-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="14192-169">Нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="14192-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="14192-170">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14192-170">Click **Next**.</span></span>
6. <span data-ttu-id="14192-171">tooget единого входа, настроенному для вашего приложения, обратитесь в службу поддержки Bynder.</span><span class="sxs-lookup"><span data-stu-id="14192-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="14192-172">Присоединение hello скачанный файл метаданных и предоставить Bynder tooset команды копирования единого входа с их стороны.</span><span class="sxs-lookup"><span data-stu-id="14192-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="14192-173">Hello классического портала выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14192-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Единый вход в Azure AD][10]
8. <span data-ttu-id="14192-175">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="14192-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Единый вход в Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="14192-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="14192-177">Create an Azure AD test user</span></span>
<span data-ttu-id="14192-178">Hello цель этого раздела — toocreate тестового пользователя вызывается Саймон Britta классическом портале hello.</span><span class="sxs-lookup"><span data-stu-id="14192-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="14192-180">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="14192-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="14192-181">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14192-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="14192-183">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="14192-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="14192-184">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="14192-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="14192-186">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="14192-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="14192-188">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="14192-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="14192-190">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="14192-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="14192-191">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14192-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="14192-192">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14192-192">Click **Next**.</span></span>
6. <span data-ttu-id="14192-193">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="14192-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="14192-195">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="14192-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="14192-196">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="14192-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="14192-197">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="14192-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="14192-198">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="14192-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="14192-199">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14192-199">Click **Next**.</span></span>
7. <span data-ttu-id="14192-200">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="14192-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="14192-202">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="14192-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="14192-204">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="14192-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="14192-205">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="14192-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="14192-206">Создание тестового пользователя Bynder</span><span class="sxs-lookup"><span data-stu-id="14192-206">Create a Bynder test user</span></span>
<span data-ttu-id="14192-207">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Bynder.</span><span class="sxs-lookup"><span data-stu-id="14192-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="14192-208">Приложение Bynder поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="14192-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="14192-209">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="14192-209">There is no action item for you in this section.</span></span> <span data-ttu-id="14192-210">Если он еще не существует во время попытки tooaccess Bynder создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="14192-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="14192-211">Если вам требуется toocreate пользователя вручную, необходимо группа поддержки Bynder toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="14192-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="14192-212">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="14192-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="14192-213">Hello цель этого раздела — tooenabling toouse Britta Simon единого входа Azure, предоставляя свой tooBynder доступа.</span><span class="sxs-lookup"><span data-stu-id="14192-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Назначение пользователя][200]

<span data-ttu-id="14192-215">**tooassign tooBynder Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="14192-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="14192-216">Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="14192-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Назначение пользователя][201]
2. <span data-ttu-id="14192-218">В списке приложений hello выберите **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="14192-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="14192-220">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="14192-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Назначение пользователя][203]
4. <span data-ttu-id="14192-222">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="14192-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="14192-223">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="14192-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="14192-225">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="14192-225">Test single sign-on</span></span>
<span data-ttu-id="14192-226">Цель этого раздела Hello является tootest конфигурации Microsoft Azure AD, единого входа с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="14192-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="14192-227">При нажатии кнопки hello Bynder плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Bynder приложения.</span><span class="sxs-lookup"><span data-stu-id="14192-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14192-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="14192-228">Additional resources</span></span>
* [<span data-ttu-id="14192-229">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14192-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14192-230">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14192-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
