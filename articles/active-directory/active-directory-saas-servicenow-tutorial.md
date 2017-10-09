---
title: "Руководство по интеграции Azure Active Directory с ServiceNow | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ServiceNow и ServiceNow, экспресс-выпуск."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="ceb24-103">Руководство: интеграция Azure Active Directory с ServiceNow</span><span class="sxs-lookup"><span data-stu-id="ceb24-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="ceb24-104">В этом учебнике вы узнаете, как toointegrate ServiceNow и ServiceNow, экспресс-выпуск с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ceb24-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ceb24-105">Интеграция с Azure AD ServiceNow и ServiceNow Express предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ceb24-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="ceb24-106">Можно управлять в Azure AD, имеющего доступ tooServiceNow и ServiceNow, экспресс-выпуск</span><span class="sxs-lookup"><span data-stu-id="ceb24-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="ceb24-107">Можно разрешить пользователям tooautomatically get вошедшего tooServiceNow и ServiceNow Express (Single Sign-On) с их учетными записями Azure AD</span><span class="sxs-lookup"><span data-stu-id="ceb24-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="ceb24-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="ceb24-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="ceb24-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ceb24-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ceb24-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ceb24-110">Prerequisites</span></span>
<span data-ttu-id="ceb24-111">tooconfigure интеграция Azure AD с ServiceNow и ServiceNow Express необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ceb24-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="ceb24-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ceb24-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ceb24-113">Экземпляр или клиент ServiceNow версии Calgary или выше (для ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="ceb24-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="ceb24-114">Экземпляр ServiceNow Express версии Helsinki или выше (для ServiceNow Express).</span><span class="sxs-lookup"><span data-stu-id="ceb24-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="ceb24-115">Hello клиента ServiceNow должен иметь hello [несколько единого входа на подключаемый модуль поставщика](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) включена.</span><span class="sxs-lookup"><span data-stu-id="ceb24-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="ceb24-116">Это можно сделать путем [отправки запроса на обслуживание](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="ceb24-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="ceb24-117">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ceb24-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="ceb24-118">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ceb24-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ceb24-119">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="ceb24-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ceb24-120">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ceb24-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ceb24-121">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ceb24-121">Scenario description</span></span>
<span data-ttu-id="ceb24-122">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ceb24-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ceb24-123">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ceb24-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ceb24-124">Добавление ServiceNow из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ceb24-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="ceb24-125">Настройка и проверка единого входа Azure AD в ServiceNow или ServiceNow Express.</span><span class="sxs-lookup"><span data-stu-id="ceb24-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="ceb24-126">Добавление ServiceNow из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ceb24-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="ceb24-127">tooconfigure hello интеграции ServiceNow или ServiceNow Express в Azure AD, вы должны tooadd ServiceNow из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ceb24-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="ceb24-128">**tooadd ServiceNow из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ceb24-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ceb24-129">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="ceb24-131">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="ceb24-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="ceb24-132">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Приложения][2]
4. <span data-ttu-id="ceb24-134">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="ceb24-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Приложения][3]
5. <span data-ttu-id="ceb24-136">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Приложения][4]
6. <span data-ttu-id="ceb24-138">Введите в поле поиска hello **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="ceb24-140">В области результатов hello выберите **ServiceNow**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ceb24-142">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ceb24-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ceb24-143">В этом разделе описано, как настроить и проверить единый вход Azure AD в ServiceNow или ServiceNow Express с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ceb24-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ceb24-144">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ServiceNow является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ceb24-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="ceb24-145">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ServiceNow должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ceb24-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="ceb24-146">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="ceb24-147">tooconfigure и теста Azure AD единого входа с ServiceNow, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ceb24-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ceb24-148">**[Настройка Azure AD Single Sign-On для ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ceb24-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ceb24-149">**[Настройка Azure AD Single Sign-On для быстрой ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ceb24-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="ceb24-150">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ceb24-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="ceb24-151">**[Создание тестового пользователя ServiceNow](#creating-a-servicenow-test-user)**  -toohave аналог Саймон Britta в ServiceNow, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="ceb24-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="ceb24-152">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ceb24-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="ceb24-153">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ceb24-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="ceb24-154">Если вы хотите tooconfigure ServiceNow пропустите шаг 2.</span><span class="sxs-lookup"><span data-stu-id="ceb24-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="ceb24-155">Аналогичным образом tooconfigure ServiceNow Express опустить шаг 1.</span><span class="sxs-lookup"><span data-stu-id="ceb24-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="ceb24-156">Настройка единого входа Azure AD в ServiceNow</span><span class="sxs-lookup"><span data-stu-id="ceb24-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="ceb24-157">Классического портала Azure AD hello на hello **ServiceNow** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно .</span><span class="sxs-lookup"><span data-stu-id="ceb24-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="ceb24-158">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="ceb24-159">На hello **предпочитаемый как toosign пользователей на tooServiceNow** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="ceb24-160">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="ceb24-161">На hello **Настройка параметров приложения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ceb24-162">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ceb24-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="ceb24-163">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-163">a.</span></span> <span data-ttu-id="ceb24-164">в hello **ServiceNow на URL-адрес входа** текстовое поле, введите URL-адрес, используемую приложением пользователей tooyour toosign на ServiceNow следующий шаблон hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="ceb24-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="ceb24-165">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-165">b.</span></span> <span data-ttu-id="ceb24-166">В hello **идентификатор** текстовое поле, введите URL-адрес, используемую приложением пользователей tooyour toosign на ServiceNow следующий шаблон hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="ceb24-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="ceb24-167">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-167">c.</span></span> <span data-ttu-id="ceb24-168">Щелкните **Далее**</span><span class="sxs-lookup"><span data-stu-id="ceb24-168">Click **Next**</span></span>

4. <span data-ttu-id="ceb24-169">toohave Azure AD, автоматически Настройка ServiceNow для проверки подлинности на основе SAML, введите имя экземпляра, имя пользователя администратора и пароль администратора ServiceNow в hello **автоматически настроить единый вход** форму и нажмите кнопку  *Настройка*.</span><span class="sxs-lookup"><span data-stu-id="ceb24-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="ceb24-170">Обратите внимание, что указано имя пользователя администратора hello должен иметь hello **security_admin** роли, назначенные в ServiceNow для этого toowork.</span><span class="sxs-lookup"><span data-stu-id="ceb24-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="ceb24-171">В противном случае toomanually настроить ServiceNow toouse Azure AD как поставщика удостоверений SAML, нажмите кнопку **вручную настроить приложение hello для единого входа**, нажмите кнопку **Далее** и завершения hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="ceb24-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="ceb24-172">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ceb24-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="ceb24-173">На hello **Настройка единого входа в ServiceNow** щелкните **загрузки сертификата**, сохраните файл сертификата hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ceb24-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="ceb24-174">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="ceb24-175">Вход tooyour ServiceNow приложения от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="ceb24-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="ceb24-176">Активировать hello *интеграция - несколько поставщика единого входа установщика* Здравствуйте, подключаемый модуль, выполнив следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ceb24-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="ceb24-177">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-177">a.</span></span> <span data-ttu-id="ceb24-178">Hello hello левой панели навигации перейдите слишком**определения системы** статьи, а затем нажмите кнопку **подключаемых модулей**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="ceb24-179">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Активация подключаемого модуля")</span><span class="sxs-lookup"><span data-stu-id="ceb24-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="ceb24-180">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-180">b.</span></span> <span data-ttu-id="ceb24-181">Найдите *Integration - Multiple Provider Single Sign-On Installer* (Интеграция — установщик единого входа для нескольких поставщиков).</span><span class="sxs-lookup"><span data-stu-id="ceb24-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="ceb24-182">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Активация подключаемого модуля")</span><span class="sxs-lookup"><span data-stu-id="ceb24-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="ceb24-183">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-183">c.</span></span> <span data-ttu-id="ceb24-184">Выберите hello подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-184">Select hello plugin.</span></span> <span data-ttu-id="ceb24-185">Щелкните правой кнопкой мыши и выберите **Activate/Upgrade** (Активировать или обновить).</span><span class="sxs-lookup"><span data-stu-id="ceb24-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="ceb24-186">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-186">d.</span></span> <span data-ttu-id="ceb24-187">Нажмите кнопку hello **активировать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ceb24-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="ceb24-188">Hello hello левой панели навигации щелкните **свойства**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="ceb24-189">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ceb24-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="ceb24-190">На hello **несколько свойств поставщика единого входа** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ceb24-191">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ceb24-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="ceb24-192">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-192">a.</span></span> <span data-ttu-id="ceb24-193">Для параметра **Enable multiple provider SSO** (Включить единый вход для нескольких поставщиков) выберите значение **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="ceb24-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="ceb24-194">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-194">b.</span></span> <span data-ttu-id="ceb24-195">Как **включить ведение журнала отладки получен hello несколько поставщика единого входа интеграции**выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="ceb24-196">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-196">c.</span></span> <span data-ttu-id="ceb24-197">В **поле hello hello пользователем таблица...**  введите **имя_пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="ceb24-198">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-198">d.</span></span> <span data-ttu-id="ceb24-199">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-199">Click **Save**.</span></span>

10. <span data-ttu-id="ceb24-200">Hello hello левой панели навигации щелкните **x509 сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="ceb24-201">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="ceb24-202">На hello **сертификаты X.509** диалоговое окно, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="ceb24-203">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="ceb24-204">На hello **сертификаты X.509** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="ceb24-205">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="ceb24-206">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-206">a.</span></span> <span data-ttu-id="ceb24-207">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-207">Click **New**.</span></span>
    
     <span data-ttu-id="ceb24-208">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-208">b.</span></span> <span data-ttu-id="ceb24-209">В hello **имя** текстовом поле введите имя для конфигурации (например: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="ceb24-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="ceb24-210">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-210">c.</span></span> <span data-ttu-id="ceb24-211">Установите флажок **Активно**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-211">Select **Active**.</span></span>
    
     <span data-ttu-id="ceb24-212">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-212">d.</span></span> <span data-ttu-id="ceb24-213">В поле **Format** (Формат) выберите **PEM**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="ceb24-214">д.</span><span class="sxs-lookup"><span data-stu-id="ceb24-214">e.</span></span> <span data-ttu-id="ceb24-215">В поле **Type** (Тип) выберите **Trust Store Cert** (Сертификат хранилища доверия).</span><span class="sxs-lookup"><span data-stu-id="ceb24-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="ceb24-216">f.</span><span class="sxs-lookup"><span data-stu-id="ceb24-216">f.</span></span> <span data-ttu-id="ceb24-217">Откройте сертификат в кодировке Base64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат PEM** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="ceb24-218">ж.</span><span class="sxs-lookup"><span data-stu-id="ceb24-218">g.</span></span> <span data-ttu-id="ceb24-219">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-219">Click **Update**.</span></span>

13. <span data-ttu-id="ceb24-220">Hello hello левой панели навигации щелкните **Поставщики удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="ceb24-221">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="ceb24-222">На hello **Поставщики удостоверений** диалоговое окно, нажмите кнопку **New**:</span><span class="sxs-lookup"><span data-stu-id="ceb24-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="ceb24-223">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="ceb24-224">На hello **Поставщики удостоверений** диалоговое окно, нажмите кнопку **SAML2 обновление 1?**:</span><span class="sxs-lookup"><span data-stu-id="ceb24-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="ceb24-225">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="ceb24-226">В диалоговом окне Свойства обновление 1 SAML2 hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="ceb24-227">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="ceb24-228">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-228">a.</span></span> <span data-ttu-id="ceb24-229">в hello **имя** текстовом поле введите имя для конфигурации (например: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="ceb24-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="ceb24-230">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-230">b.</span></span> <span data-ttu-id="ceb24-231">В hello **поле пользователя** введите **электронной почты** или **имя_пользователя**, в зависимости от того, какое поле используется toouniquely идентификации пользователей в вашем развертывании ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="ceb24-232">Можно либо идентификатора пользователя hello Azure AD (имя участника-пользователя) tooemit настройки Azure AD или hello адрес электронной почты как hello уникальный идентификатор в токене SAML hello с переходом toohello **ServiceNow > атрибуты > Single Sign-On** раздела Здравствуйте классический портал Azure и сопоставление hello требуемого поля toohello **nameidentifier** атрибута.</span><span class="sxs-lookup"><span data-stu-id="ceb24-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="ceb24-233">значение Hello, сохраненные для выбранного атрибута hello в Azure AD (например имя участника-пользователя) должно соответствовать hello значение, хранящееся в ServiceNow для hello введенные поля (например имя_пользователя)</span><span class="sxs-lookup"><span data-stu-id="ceb24-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="ceb24-234">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-234">c.</span></span> <span data-ttu-id="ceb24-235">В классическом портале Azure AD hello, скопируйте hello **идентификатор поставщика удостоверений** значение, а затем вставьте его в hello **URL-адрес поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="ceb24-236">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-236">d.</span></span> <span data-ttu-id="ceb24-237">В классическом портале Azure AD hello, скопируйте hello **URL-адрес запроса проверки подлинности** значение, а затем вставьте его в hello **AuthnRequest поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="ceb24-238">д.</span><span class="sxs-lookup"><span data-stu-id="ceb24-238">e.</span></span> <span data-ttu-id="ceb24-239">В классическом портале Azure AD hello, скопируйте hello **URL-адрес службы единого выхода** значение, а затем вставьте его в hello **SingleLogoutRequest поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="ceb24-240">f.</span><span class="sxs-lookup"><span data-stu-id="ceb24-240">f.</span></span> <span data-ttu-id="ceb24-241">В hello **домашней страницы ServiceNow** текстовом поле введите URL-адрес hello вашей домашней страницы экземпляра ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ceb24-242">Домашняя страница экземпляра ServiceNow Hello составляется из вашего **URL-адрес клиента ServieNow** и **/navpage.do** (например:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="ceb24-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="ceb24-243">ж.</span><span class="sxs-lookup"><span data-stu-id="ceb24-243">g.</span></span> <span data-ttu-id="ceb24-244">В hello **идентификатор сущности или издателя** текстовом поле введите hello URL-адрес клиента ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="ceb24-245">h.</span><span class="sxs-lookup"><span data-stu-id="ceb24-245">h.</span></span> <span data-ttu-id="ceb24-246">В hello **аудитории URL-адрес** в текстовое поле введите hello URL-адрес клиента ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="ceb24-247">i.</span><span class="sxs-lookup"><span data-stu-id="ceb24-247">i.</span></span> <span data-ttu-id="ceb24-248">В hello **привязки протокола для SingleLogoutRequest поставщика Удостоверений hello** введите **urn: oasis: имена: tc: SAML:2.0:bindings:HTTP-перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="ceb24-249">j.</span><span class="sxs-lookup"><span data-stu-id="ceb24-249">j.</span></span> <span data-ttu-id="ceb24-250">В hello политики идентификатора имени текстового поля, введите **urn: oasis: имена: tc: SAML:1.1:nameid-формат: Неизвестная**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="ceb24-251">k.</span><span class="sxs-lookup"><span data-stu-id="ceb24-251">k.</span></span> <span data-ttu-id="ceb24-252">Снимите флажок **Create an AuthnContextClass**(Создать класс контекста проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="ceb24-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="ceb24-253">l.</span><span class="sxs-lookup"><span data-stu-id="ceb24-253">l.</span></span> <span data-ttu-id="ceb24-254">В hello **метод AuthnContextClassRef**, тип `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="ceb24-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="ceb24-255">Это действие требуется только для организаций на основе облака.</span><span class="sxs-lookup"><span data-stu-id="ceb24-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="ceb24-256">Если используется локальная аутентификация AD FS или MFA, это значение указывать не нужно.</span><span class="sxs-lookup"><span data-stu-id="ceb24-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="ceb24-257">m.</span><span class="sxs-lookup"><span data-stu-id="ceb24-257">m.</span></span> <span data-ttu-id="ceb24-258">В текстовое поле **Clock Skew** (Разница в показаниях часов) введите **60**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="ceb24-259">n.</span><span class="sxs-lookup"><span data-stu-id="ceb24-259">n.</span></span> <span data-ttu-id="ceb24-260">В поле **Single Sign On Script** (Сценарий единого входа) выберите **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="ceb24-261">o.</span><span class="sxs-lookup"><span data-stu-id="ceb24-261">o.</span></span> <span data-ttu-id="ceb24-262">Как **x509 сертификат**выберите hello сертификат, созданный на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="ceb24-263">p.</span><span class="sxs-lookup"><span data-stu-id="ceb24-263">p.</span></span> <span data-ttu-id="ceb24-264">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="ceb24-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="ceb24-265">На классический портал hello Azure AD, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="ceb24-266">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="ceb24-267">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="ceb24-268">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="ceb24-269">Настройка единого входа в Azure AD для ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="ceb24-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="ceb24-270">Классического портала Azure AD hello на hello **ServiceNow** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно .</span><span class="sxs-lookup"><span data-stu-id="ceb24-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="ceb24-271">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="ceb24-272">На hello **предпочитаемый как toosign пользователей на tooServiceNow** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="ceb24-273">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="ceb24-274">На hello **Настройка параметров приложения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ceb24-275">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ceb24-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="ceb24-276">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-276">a.</span></span> <span data-ttu-id="ceb24-277">в hello **ServiceNow на URL-адрес входа** текстовое поле, введите URL-адрес, используемую приложением пользователей tooyour toosign на ServiceNow следующий шаблон hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="ceb24-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="ceb24-278">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-278">b.</span></span> <span data-ttu-id="ceb24-279">В hello **URL-адрес издателя** текстовое поле, введите URL-адрес, используемую приложением пользователей tooyour toosign на ServiceNow следующий шаблон hello `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="ceb24-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="ceb24-280">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-280">c.</span></span> <span data-ttu-id="ceb24-281">Щелкните **Далее**</span><span class="sxs-lookup"><span data-stu-id="ceb24-281">Click **Next**</span></span>

4. <span data-ttu-id="ceb24-282">Нажмите кнопку **вручную настроить приложение hello для единого входа**, нажмите кнопку **Далее** и завершения hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="ceb24-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="ceb24-283">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ceb24-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="ceb24-284">На hello **Настройка единого входа в ServiceNow** щелкните **загрузки сертификата**, сохраните файл сертификата hello на локальном компьютере и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="ceb24-285">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="ceb24-286">Вход tooyour ServiceNow Express приложения от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="ceb24-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="ceb24-287">Hello hello левой панели навигации щелкните **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="ceb24-288">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ceb24-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="ceb24-289">На hello **Single Sign-On** диалоговое окно, щелкните значок конфигурации hello в верхнем hello вправо и задайте hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="ceb24-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="ceb24-290">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ceb24-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="ceb24-291">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-291">a.</span></span> <span data-ttu-id="ceb24-292">Переключить **Включение нескольких поставщика единого входа** toohello справа.</span><span class="sxs-lookup"><span data-stu-id="ceb24-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="ceb24-293">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-293">b.</span></span> <span data-ttu-id="ceb24-294">Переключить **Включение ведения журнала для hello поставщик нескольких интеграции единого входа для отладки** toohello справа.</span><span class="sxs-lookup"><span data-stu-id="ceb24-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="ceb24-295">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-295">c.</span></span> <span data-ttu-id="ceb24-296">В **поле hello hello пользователем таблица...**  введите **имя_пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="ceb24-297">На hello **Single Sign-On** диалоговое окно, нажмите кнопку **Добавление нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="ceb24-298">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="ceb24-299">На hello **сертификаты X.509** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="ceb24-300">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="ceb24-301">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-301">a.</span></span> <span data-ttu-id="ceb24-302">В hello **имя** текстовом поле введите имя для конфигурации (например: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="ceb24-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="ceb24-303">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-303">b.</span></span> <span data-ttu-id="ceb24-304">Установите флажок **Активно**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-304">Select **Active**.</span></span>
    
    <span data-ttu-id="ceb24-305">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-305">c.</span></span> <span data-ttu-id="ceb24-306">В поле **Format** (Формат) выберите **PEM**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="ceb24-307">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-307">d.</span></span> <span data-ttu-id="ceb24-308">В поле **Type** (Тип) выберите **Trust Store Cert** (Сертификат хранилища доверия).</span><span class="sxs-lookup"><span data-stu-id="ceb24-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="ceb24-309">д.</span><span class="sxs-lookup"><span data-stu-id="ceb24-309">e.</span></span> <span data-ttu-id="ceb24-310">Создайте файл в кодировке Base 64 из скачанного сертификата.</span><span class="sxs-lookup"><span data-stu-id="ceb24-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ceb24-311">Дополнительные сведения см. в разделе [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="ceb24-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="ceb24-312">f.</span><span class="sxs-lookup"><span data-stu-id="ceb24-312">f.</span></span> <span data-ttu-id="ceb24-313">Откройте сертификат в кодировке Base64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат PEM** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="ceb24-314">ж.</span><span class="sxs-lookup"><span data-stu-id="ceb24-314">g.</span></span> <span data-ttu-id="ceb24-315">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-315">Click **Update**.</span></span>
11. <span data-ttu-id="ceb24-316">На hello **Single Sign-On** диалоговое окно, нажмите кнопку **добавить нового поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="ceb24-317">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="ceb24-318">На hello **Добавление поставщика удостоверений** диалогового окна в разделе **Настройка поставщика удостоверений**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="ceb24-319">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="ceb24-320">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-320">a.</span></span> <span data-ttu-id="ceb24-321">в hello **имя** текстовом поле введите имя для конфигурации (например: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="ceb24-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="ceb24-322">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-322">b.</span></span> <span data-ttu-id="ceb24-323">В классическом портале Azure AD hello, скопируйте hello **идентификатор поставщика удостоверений** значение, а затем вставьте его в hello **URL-адрес поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="ceb24-324">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-324">c.</span></span> <span data-ttu-id="ceb24-325">В классическом портале Azure AD hello, скопируйте hello **URL-адрес запроса проверки подлинности** значение, а затем вставьте его в hello **AuthnRequest поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="ceb24-326">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-326">d.</span></span> <span data-ttu-id="ceb24-327">В классическом портале Azure AD hello, скопируйте hello **URL-адрес службы единого выхода** значение, а затем вставьте его в hello **SingleLogoutRequest поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ceb24-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="ceb24-328">д.</span><span class="sxs-lookup"><span data-stu-id="ceb24-328">e.</span></span> <span data-ttu-id="ceb24-329">Как **сертификат поставщика удостоверений**выберите hello сертификат, созданный на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="ceb24-330">Нажмите кнопку **Дополнительные параметры**, а затем в разделе **дополнительные свойства поставщика удостоверений**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="ceb24-331">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="ceb24-332">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-332">a.</span></span> <span data-ttu-id="ceb24-333">В hello **привязки протокола для SingleLogoutRequest поставщика Удостоверений hello** введите **urn: oasis: имена: tc: SAML:2.0:bindings:HTTP-перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="ceb24-334">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-334">b.</span></span> <span data-ttu-id="ceb24-335">В hello **политики идентификатора имени** введите **urn: oasis: имена: tc: SAML:1.1:nameid-формат: Неизвестная**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="ceb24-336">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-336">c.</span></span> <span data-ttu-id="ceb24-337">В hello **метод AuthnContextClassRef**, тип **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="ceb24-338">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-338">d.</span></span> <span data-ttu-id="ceb24-339">Снимите флажок **Create an AuthnContextClass**(Создать класс контекста проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="ceb24-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="ceb24-340">В разделе **дополнительные свойства поставщика службы**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="ceb24-341">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="ceb24-342">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-342">a.</span></span> <span data-ttu-id="ceb24-343">В hello **домашней страницы ServiceNow** текстовом поле введите URL-адрес hello вашей домашней страницы экземпляра ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="ceb24-344">Домашняя страница экземпляра ServiceNow Hello составляется из вашего **URL-адрес клиента ServieNow** и **/navpage.do** (например: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="ceb24-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="ceb24-345">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-345">b.</span></span> <span data-ttu-id="ceb24-346">В hello **идентификатор сущности или издателя** текстовом поле введите hello URL-адрес клиента ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="ceb24-347">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-347">c.</span></span> <span data-ttu-id="ceb24-348">В hello **URI аудитории** текстовом поле введите hello URL-адрес клиента ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="ceb24-349">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-349">d.</span></span> <span data-ttu-id="ceb24-350">В текстовое поле **Clock Skew** (Разница в показаниях часов) введите **60**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="ceb24-351">д.</span><span class="sxs-lookup"><span data-stu-id="ceb24-351">e.</span></span> <span data-ttu-id="ceb24-352">В hello **поле пользователя** введите **электронной почты** или **имя_пользователя**, в зависимости от того, какое поле используется toouniquely идентификации пользователей в вашем развертывании ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="ceb24-353">Можно либо идентификатора пользователя hello Azure AD (имя участника-пользователя) tooemit настройки Azure AD или hello адрес электронной почты как hello уникальный идентификатор в токене SAML hello с переходом toohello **ServiceNow > атрибуты > Single Sign-On** раздела Здравствуйте классический портал Azure и сопоставление hello требуемого поля toohello **nameidentifier** атрибута.</span><span class="sxs-lookup"><span data-stu-id="ceb24-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="ceb24-354">значение Hello, сохраненные для выбранного атрибута hello в Azure AD (например имя участника-пользователя) должно соответствовать hello значение, хранящееся в ServiceNow для hello введенные поля (например имя_пользователя)</span><span class="sxs-lookup"><span data-stu-id="ceb24-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="ceb24-355">f.</span><span class="sxs-lookup"><span data-stu-id="ceb24-355">f.</span></span> <span data-ttu-id="ceb24-356">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-356">Click **Save**.</span></span> 

3. <span data-ttu-id="ceb24-357">На классический портал hello Azure AD, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="ceb24-358">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="ceb24-359">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="ceb24-360">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ceb24-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="ceb24-361">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="ceb24-361">Configuring user provisioning</span></span>
<span data-ttu-id="ceb24-362">Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="ceb24-363">tooconfigure подготовки пользователей, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="ceb24-364">Hello Azure Management классического портала на hello **ServiceNow** странице интеграции приложения щелкните **Настройка подготовки пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="ceb24-365">![Подготовка учетных записей пользователей](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Подготовка учетных записей пользователей")</span><span class="sxs-lookup"><span data-stu-id="ceb24-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="ceb24-366">На hello **введите ваш ServiceNow учетные данные tooenable автоматическую подготовку пользователей** укажите следующие параметры конфигурации hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="ceb24-367">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-367">a.</span></span> <span data-ttu-id="ceb24-368">В hello **имя экземпляра ServiceNow** текстовое поле, имя экземпляра ServiceNow типа hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="ceb24-369">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-369">b.</span></span> <span data-ttu-id="ceb24-370">В hello **имя пользователя администратора ServiceNow** в текстовое поле имя типа hello hello учетной записи администратора ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="ceb24-371">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-371">c.</span></span> <span data-ttu-id="ceb24-372">В hello **пароль администратора ServiceNow** текстового поля, типа hello пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ceb24-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="ceb24-373">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-373">d.</span></span> <span data-ttu-id="ceb24-374">Нажмите кнопку **проверки** tooverify конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ceb24-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="ceb24-375">д.</span><span class="sxs-lookup"><span data-stu-id="ceb24-375">e.</span></span> <span data-ttu-id="ceb24-376">Нажмите кнопку hello **Далее** hello tooopen кнопку **дальнейшие действия** страницы.</span><span class="sxs-lookup"><span data-stu-id="ceb24-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="ceb24-377">f.</span><span class="sxs-lookup"><span data-stu-id="ceb24-377">f.</span></span> <span data-ttu-id="ceb24-378">Tooprovision приложения toothis всех пользователей, выберите «**автоматически подготовить все учетные записи пользователей в приложении toothis directory hello**».</span><span class="sxs-lookup"><span data-stu-id="ceb24-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="ceb24-379">![Дальнейшие действия](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Дальнейшие действия")</span><span class="sxs-lookup"><span data-stu-id="ceb24-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="ceb24-380">ж.</span><span class="sxs-lookup"><span data-stu-id="ceb24-380">g.</span></span> <span data-ttu-id="ceb24-381">На hello **дальнейшие действия** щелкните **завершить** toosave конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ceb24-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ceb24-382">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ceb24-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="ceb24-383">В этом разделе создайте тестового пользователя вызывается Саймон Britta классическом портале hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="ceb24-385">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ceb24-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ceb24-386">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="ceb24-388">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="ceb24-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="ceb24-389">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ceb24-391">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="ceb24-393">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="ceb24-395">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-395">a.</span></span> <span data-ttu-id="ceb24-396">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="ceb24-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="ceb24-397">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-397">b.</span></span> <span data-ttu-id="ceb24-398">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="ceb24-399">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-399">c.</span></span> <span data-ttu-id="ceb24-400">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-400">Click **Next**.</span></span>

6. <span data-ttu-id="ceb24-401">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="ceb24-403">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-403">a.</span></span> <span data-ttu-id="ceb24-404">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="ceb24-405">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-405">b.</span></span> <span data-ttu-id="ceb24-406">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="ceb24-407">c.</span><span class="sxs-lookup"><span data-stu-id="ceb24-407">c.</span></span> <span data-ttu-id="ceb24-408">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="ceb24-409">d.</span><span class="sxs-lookup"><span data-stu-id="ceb24-409">d.</span></span> <span data-ttu-id="ceb24-410">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="ceb24-411">д.</span><span class="sxs-lookup"><span data-stu-id="ceb24-411">e.</span></span> <span data-ttu-id="ceb24-412">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-412">Click **Next**.</span></span>

7. <span data-ttu-id="ceb24-413">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="ceb24-415">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ceb24-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="ceb24-417">а.</span><span class="sxs-lookup"><span data-stu-id="ceb24-417">a.</span></span> <span data-ttu-id="ceb24-418">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="ceb24-419">b.</span><span class="sxs-lookup"><span data-stu-id="ceb24-419">b.</span></span> <span data-ttu-id="ceb24-420">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="ceb24-421">Создание тестового пользователя ServiceNow</span><span class="sxs-lookup"><span data-stu-id="ceb24-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="ceb24-422">В этом разделе описано, как создать пользователя Britta Simon в ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="ceb24-423">В этом разделе описано, как создать пользователя Britta Simon в ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="ceb24-424">Если вы не знаете, как tooadd в ServiceNow или ServiceNow Express учетная запись пользователя, обратитесь в службу технической поддержки ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ceb24-425">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ceb24-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="ceb24-426">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooServiceNow доступа.</span><span class="sxs-lookup"><span data-stu-id="ceb24-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ceb24-428">**tooassign tooServiceNow Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ceb24-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="ceb24-429">Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="ceb24-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Назначение пользователя][201] 

2. <span data-ttu-id="ceb24-431">В списке приложений hello выберите **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="ceb24-433">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Назначение пользователя][203] 

4. <span data-ttu-id="ceb24-435">В списке Привет всем пользователям, выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="ceb24-436">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="ceb24-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="ceb24-438">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ceb24-438">Testing single sign-on</span></span>
<span data-ttu-id="ceb24-439">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="ceb24-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ceb24-440">При нажатии кнопки hello ServiceNow плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="ceb24-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ceb24-441">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ceb24-441">Additional resources</span></span>
* [<span data-ttu-id="ceb24-442">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ceb24-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ceb24-443">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ceb24-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
