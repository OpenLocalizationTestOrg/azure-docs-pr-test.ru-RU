---
title: "Руководство по интеграции Azure Active Directory с Soonr Workplace | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Soonr рабочей области."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="7bd39-103">Учебник. Интеграция Azure Active Directory с Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="7bd39-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="7bd39-104">Hello цель этого учебника — tooshow вы как toointegrate Soonr рабочему месту с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7bd39-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="7bd39-105">Интеграция с Azure AD Soonr рабочему месту предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7bd39-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7bd39-106">Можно управлять в Azure AD, имеющего tooSoonr доступа к рабочему месту</span><span class="sxs-lookup"><span data-stu-id="7bd39-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="7bd39-107">Можно включить на пользователей tooautomatically get вошедшего tooSoonr рабочему месту (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd39-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7bd39-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="7bd39-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="7bd39-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7bd39-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bd39-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7bd39-110">Prerequisites</span></span>

<span data-ttu-id="7bd39-111">tooconfigure интеграция Azure AD в рабочей области Soonr требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7bd39-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="7bd39-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7bd39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7bd39-113">подписка Soonr Workplace с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7bd39-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="7bd39-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7bd39-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="7bd39-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7bd39-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7bd39-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="7bd39-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7bd39-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7bd39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7bd39-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7bd39-118">Scenario description</span></span>
<span data-ttu-id="7bd39-119">Hello цель этого учебника — tooenable tootest Azure AD единого входа в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7bd39-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="7bd39-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7bd39-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7bd39-121">Добавление рабочей области Soonr из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7bd39-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="7bd39-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd39-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="7bd39-123">Добавление рабочей области Soonr из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7bd39-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="7bd39-124">tooconfigure hello интеграции Soonr рабочая область в Azure AD, вы должны tooadd Soonr рабочей области из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7bd39-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7bd39-125">**tooadd Soonr рабочей области из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7bd39-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7bd39-126">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7bd39-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="7bd39-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="7bd39-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="7bd39-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Приложения][2]

4. <span data-ttu-id="7bd39-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="7bd39-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Приложения][3]

5. <span data-ttu-id="7bd39-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![Приложения][4]

6. <span data-ttu-id="7bd39-135">Введите в поле поиска hello **рабочему месту Soonr**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="7bd39-137">В области результатов hello выберите **рабочему месту Soonr**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7bd39-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7bd39-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd39-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7bd39-140">Цель этого раздела Hello является tooshow как tooconfigure и тестирования Azure AD единого входа в рабочей области Soonr на основе тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="7bd39-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7bd39-141">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочей области Soonr tooan пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bd39-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="7bd39-142">Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочей области Soonr должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7bd39-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="7bd39-143">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** Soonr рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="7bd39-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="7bd39-144">tooconfigure и тестирования Azure AD единого входа в рабочей области Soonr, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7bd39-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7bd39-145">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7bd39-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7bd39-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7bd39-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7bd39-147">**[Создание тестового пользователя рабочему месту Soonr](#creating-a-soonr-workplace-test-user)**  -toohave аналог Саймон Britta в рабочей области Soonr, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="7bd39-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7bd39-148">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7bd39-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7bd39-149">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7bd39-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7bd39-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd39-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7bd39-151">В этом разделе включения Azure AD единого входа в классическом портале hello и настройки единого входа в приложении Soonr рабочей области.</span><span class="sxs-lookup"><span data-stu-id="7bd39-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="7bd39-152">**tooconfigure Azure AD единого входа в рабочей области Soonr, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7bd39-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7bd39-153">В классический портал Azure, на hello hello **рабочему месту Soonr** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**  диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="7bd39-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Настройка единого входа][6] 

2. <span data-ttu-id="7bd39-155">На hello **предпочитаемый как toosign пользователей на рабочем месте tooSoonr** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="7bd39-157">На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:.</span><span class="sxs-lookup"><span data-stu-id="7bd39-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="7bd39-159">а.</span><span class="sxs-lookup"><span data-stu-id="7bd39-159">a.</span></span> <span data-ttu-id="7bd39-160">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="7bd39-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="7bd39-161">b.</span><span class="sxs-lookup"><span data-stu-id="7bd39-161">b.</span></span> <span data-ttu-id="7bd39-162">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7bd39-163">Обратите внимание на то, что это не Вещественное значение hello.</span><span class="sxs-lookup"><span data-stu-id="7bd39-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="7bd39-164">У вас есть tooupdate это значение с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="7bd39-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="7bd39-165">Обратитесь к рабочему месту Soonr поддержки команды tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="7bd39-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="7bd39-166">На hello **настроить единый вход на рабочем месте Soonr** щелкните **загрузить метаданные** и затем сохраните файл hello на вашем компьютере:</span><span class="sxs-lookup"><span data-stu-id="7bd39-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="7bd39-168">tooget единого входа, настроенному для вашего приложения, обратитесь в службу поддержки Soonr рабочей области и предоставить им hello следующие:</span><span class="sxs-lookup"><span data-stu-id="7bd39-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="7bd39-169">• hello загружены **метаданные** файла</span><span class="sxs-lookup"><span data-stu-id="7bd39-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="7bd39-170">• hello **URL-адрес издателя**</span><span class="sxs-lookup"><span data-stu-id="7bd39-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="7bd39-171">• hello **URL-адрес единого входа SAML**</span><span class="sxs-lookup"><span data-stu-id="7bd39-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="7bd39-172">• hello **URL-адрес службы единого выхода**</span><span class="sxs-lookup"><span data-stu-id="7bd39-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="7bd39-173">Это приложение заменяется <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask рабочей области</a> и может указывать <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">это</a> учебника по настройке приложения hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bd39-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="7bd39-174">В hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Единый вход в Azure AD][10]

7. <span data-ttu-id="7bd39-176">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Единый вход в Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7bd39-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd39-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="7bd39-179">Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="7bd39-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Создание пользователя Azure AD][20]

<span data-ttu-id="7bd39-181">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7bd39-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7bd39-182">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="7bd39-184">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="7bd39-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="7bd39-185">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7bd39-187">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="7bd39-189">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7bd39-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="7bd39-191">а.</span><span class="sxs-lookup"><span data-stu-id="7bd39-191">a.</span></span> <span data-ttu-id="7bd39-192">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="7bd39-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="7bd39-193">b.</span><span class="sxs-lookup"><span data-stu-id="7bd39-193">b.</span></span> <span data-ttu-id="7bd39-194">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7bd39-195">c.</span><span class="sxs-lookup"><span data-stu-id="7bd39-195">c.</span></span> <span data-ttu-id="7bd39-196">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-196">Click **Next**.</span></span>

6.  <span data-ttu-id="7bd39-197">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7bd39-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="7bd39-199">а.</span><span class="sxs-lookup"><span data-stu-id="7bd39-199">a.</span></span> <span data-ttu-id="7bd39-200">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="7bd39-201">b.</span><span class="sxs-lookup"><span data-stu-id="7bd39-201">b.</span></span> <span data-ttu-id="7bd39-202">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="7bd39-203">c.</span><span class="sxs-lookup"><span data-stu-id="7bd39-203">c.</span></span> <span data-ttu-id="7bd39-204">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="7bd39-205">d.</span><span class="sxs-lookup"><span data-stu-id="7bd39-205">d.</span></span> <span data-ttu-id="7bd39-206">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="7bd39-207">д.</span><span class="sxs-lookup"><span data-stu-id="7bd39-207">e.</span></span> <span data-ttu-id="7bd39-208">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-208">Click **Next**.</span></span>

7. <span data-ttu-id="7bd39-209">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="7bd39-211">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7bd39-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="7bd39-213">а.</span><span class="sxs-lookup"><span data-stu-id="7bd39-213">a.</span></span> <span data-ttu-id="7bd39-214">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="7bd39-215">b.</span><span class="sxs-lookup"><span data-stu-id="7bd39-215">b.</span></span> <span data-ttu-id="7bd39-216">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="7bd39-217">Создание тестового пользователя Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="7bd39-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="7bd39-218">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon Soonr рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="7bd39-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="7bd39-219">Обратитесь toocreate группы поддержки Soonr рабочее место пользователя на платформе hello.</span><span class="sxs-lookup"><span data-stu-id="7bd39-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="7bd39-220">Может вызывать службу поддержки hello Soonr из <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">здесь</a>.</span><span class="sxs-lookup"><span data-stu-id="7bd39-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7bd39-221">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7bd39-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7bd39-222">Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа путем предоставления ее tooSoonr доступа к рабочему месту.</span><span class="sxs-lookup"><span data-stu-id="7bd39-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7bd39-224">**tooassign tooSoonr Britta Simon рабочему месту, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="7bd39-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7bd39-225">Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="7bd39-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7bd39-227">В списке приложений hello выберите **рабочему месту Soonr**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="7bd39-229">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-229">In hello menu on hello top, click **Users**.</span></span>

    ![Назначение пользователя][203] 

1. <span data-ttu-id="7bd39-231">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="7bd39-232">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="7bd39-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Назначение пользователя][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="7bd39-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7bd39-234">Testing single sign-on</span></span>

<span data-ttu-id="7bd39-235">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="7bd39-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="7bd39-236">При нажатии кнопки hello рабочему месту Soonr плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Soonr рабочей области приложения.</span><span class="sxs-lookup"><span data-stu-id="7bd39-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7bd39-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7bd39-237">Additional resources</span></span>

* [<span data-ttu-id="7bd39-238">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bd39-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7bd39-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7bd39-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
