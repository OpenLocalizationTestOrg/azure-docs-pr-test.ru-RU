---
title: "Руководство по интеграции Azure Active Directory с SCC LifeCycle | Документация Майкрософт"
description: "Узнайте, как toouse SCC LifeCycle с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="05c5f-103">Учебник. Интеграция Azure Active Directory с SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="05c5f-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="05c5f-104">Цель этого учебника Hello — tooshow hello интеграцию Azure и SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="05c5f-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="05c5f-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="05c5f-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="05c5f-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="05c5f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="05c5f-107">Подписка SCC LifeCycle с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="05c5f-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="05c5f-108">После завершения этого учебника, Здравствуйте, пользователи Azure AD, назначенные tooSCC жизненного цикла будет может toosingle входа в приложение hello на корпоративном сайте SCC LifeCycle (инициированный поставщиком вход службы) или с помощью hello [введение Панель доступа toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05c5f-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="05c5f-109">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="05c5f-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="05c5f-110">Включение hello интеграции приложений для SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="05c5f-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="05c5f-111">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="05c5f-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="05c5f-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="05c5f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="05c5f-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="05c5f-113">Assigning users</span></span>

<span data-ttu-id="05c5f-114">![Сценарий](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="05c5f-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="05c5f-115">Включить hello интеграции приложений для SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="05c5f-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="05c5f-116">Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="05c5f-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="05c5f-117">**Интеграция приложения hello tooenable для SCC LifeCycle, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="05c5f-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="05c5f-118">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05c5f-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="05c5f-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="05c5f-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="05c5f-120">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="05c5f-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="05c5f-121">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="05c5f-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="05c5f-122">![Приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="05c5f-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="05c5f-123">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="05c5f-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="05c5f-124">![Добавление приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="05c5f-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="05c5f-125">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="05c5f-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="05c5f-126">![Добавление приложения из коллекции](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="05c5f-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="05c5f-127">В hello **поле поиска**, тип **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="05c5f-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="05c5f-128">![Коллекция приложений](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="05c5f-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="05c5f-129">В области результатов hello выберите **SCC LifeCycle**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="05c5f-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="05c5f-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="05c5f-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="05c5f-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="05c5f-131">Configure single sign-on</span></span>

<span data-ttu-id="05c5f-132">Цель этого раздела Hello — toooutline, каким образом пользователи tooenable tooauthenticate tooSCC жизненного цикла с помощью учетной записи в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="05c5f-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="05c5f-133">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="05c5f-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="05c5f-134">В классический портал Azure, на hello hello **SCC LifeCycle** странице интеграции приложения щелкните **настроить единый вход** tooopen hello ** Настройка единого входа ** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="05c5f-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="05c5f-135">![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="05c5f-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="05c5f-136">На hello **предпочитаемый как toosign пользователей на tooSCC жизненного цикла** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="05c5f-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="05c5f-137">![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="05c5f-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="05c5f-138">На hello **настроить URL-адрес приложения** страницы в hello **на URL-адрес входа** текстовое поле, введите URL-адрес hello используется ваш toosign пользователей на tooyour SCC LifeCycle приложения, используя следующий шаблон hello»*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*», а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="05c5f-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="05c5f-139">![Настройка URL-адреса приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="05c5f-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="05c5f-140">На hello **настройки единого входа в SCC LifeCycle** щелкните **загрузить метаданные**, а затем сохраните файл метаданных на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="05c5f-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="05c5f-141">![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="05c5f-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="05c5f-142">Пересылка этого tooSCC файл метаданных группе поддержки жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="05c5f-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="05c5f-143">Единый вход имеет toobe включаемые hello группа поддержки SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="05c5f-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="05c5f-144">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="05c5f-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="05c5f-145">![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="05c5f-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="05c5f-146">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="05c5f-146">Configure user provisioning</span></span>

<span data-ttu-id="05c5f-147">В порядке tooenable toolog пользователей Azure AD в SCC LifeCycle их необходимо подготовить в SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="05c5f-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="05c5f-148">Нет элемента действия для вас tooconfigure подготовки пользователей tooSCC жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="05c5f-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="05c5f-149">Когда назначенный пользователь пытается toolog в SCC LifeCycle учетная запись SCC LifeCycle создается автоматически при необходимости.</span><span class="sxs-lookup"><span data-stu-id="05c5f-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="05c5f-150">Можно использовать любые другие SCC LifeCycle пользователя средства создания учетных записей или интерфейсы API, предоставляемые SCC LifeCycle tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="05c5f-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="05c5f-151">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="05c5f-151">Assign users</span></span>
<span data-ttu-id="05c5f-152">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="05c5f-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="05c5f-153">**Пользователи tooassign tooSCC жизненного цикла, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="05c5f-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="05c5f-154">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="05c5f-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="05c5f-155">На hello ** SCC LifeCycle ** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="05c5f-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="05c5f-156">![Назначение пользователей](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="05c5f-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="05c5f-157">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="05c5f-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="05c5f-158">![Да](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="05c5f-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="05c5f-159">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="05c5f-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="05c5f-160">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05c5f-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

