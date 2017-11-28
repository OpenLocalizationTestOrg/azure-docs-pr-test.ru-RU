---
title: "Руководство по интеграции Azure Active Directory с SCC LifeCycle | Документация Майкрософт"
description: "Узнайте, как использовать SCC LifeCycle с Azure Active Directory для реализации единого входа, автоматической подготовки к работе и многого другого."
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
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="0282c-103">Учебник. Интеграция Azure Active Directory с SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="0282c-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="0282c-104">Цель данного учебника — показать интеграцию Azure и SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0282c-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="0282c-105">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="0282c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="0282c-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="0282c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="0282c-107">Подписка SCC LifeCycle с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0282c-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="0282c-108">После завершения этого руководства пользователи Azure AD, назначенные SCC LifeCycle, будут иметь возможность единого входа в приложение на веб-сайте компании SCC LifeCycle (вход, инициированный поставщиком услуг) или с помощью инструкций из статьи [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0282c-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="0282c-109">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="0282c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="0282c-110">Включение интеграции приложений для SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="0282c-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="0282c-111">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="0282c-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="0282c-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="0282c-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="0282c-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="0282c-113">Assigning users</span></span>

<span data-ttu-id="0282c-114">![Сценарий](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="0282c-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="0282c-115">Включение интеграции приложений для SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="0282c-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="0282c-116">В этом разделе показано, как включить интеграцию приложений для SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0282c-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="0282c-117">**Чтобы включить интеграцию приложений для SCC LifeCycle, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="0282c-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="0282c-118">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0282c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="0282c-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="0282c-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="0282c-120">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="0282c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="0282c-121">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="0282c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="0282c-122">![Приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="0282c-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="0282c-123">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="0282c-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="0282c-124">![Добавление приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="0282c-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="0282c-125">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="0282c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="0282c-126">![Добавление приложения из коллекции](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="0282c-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="0282c-127">В **поле поиска** введите **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="0282c-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="0282c-128">![Коллекция приложений](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="0282c-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="0282c-129">В области результатов выберите **SCC LifeCycle** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="0282c-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="0282c-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="0282c-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="0282c-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="0282c-131">Configure single sign-on</span></span>

<span data-ttu-id="0282c-132">В этом разделе показано, как разрешить пользователям проходить аутентификацию в SCC LifeCycle со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="0282c-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="0282c-133">**Чтобы настроить единый вход, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0282c-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="0282c-134">На классическом портале Azure на странице интеграции с приложением **SCC LifeCycle** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0282c-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="0282c-135">![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="0282c-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="0282c-136">На странице **Как пользователи должны входить в SCC LifeCycle?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0282c-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="0282c-137">![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="0282c-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="0282c-138">На странице **Настроить URL-адрес приложения** в текстовом поле **URL-адрес входа** введите URL-адрес, используемый пользователями для входа в приложение SCC LifeCycle, в формате *https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*, после чего и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0282c-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="0282c-139">![Настройка URL-адреса приложения](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="0282c-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="0282c-140">На странице **Настройка единого входа в SCC LifeCycle** щелкните **Скачать метаданные**, а затем сохраните файл метаданных на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="0282c-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="0282c-141">![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="0282c-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="0282c-142">Передайте этот файл метаданных в группу поддержки SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0282c-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="0282c-143">Единый вход должна включить группа поддержки SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0282c-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="0282c-144">На классическом портале Azure выберите подтверждение конфигурации единого входа, а затем нажмите кнопку **Завершить**, чтобы закрыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0282c-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="0282c-145">![Настройка единого входа](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="0282c-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="0282c-146">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="0282c-146">Configure user provisioning</span></span>

<span data-ttu-id="0282c-147">Чтобы пользователи Azure AD могли выполнять вход в SCC LifeCycle, они должны быть подготовлены для SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0282c-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="0282c-148">Действие для настройки подготовки пользователей в SCC LifeCycle отсутствует.</span><span class="sxs-lookup"><span data-stu-id="0282c-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="0282c-149">Когда назначенный пользователь пытается войти в SCC LifeCycle, учетная запись SCC LifeCycle создается автоматически (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="0282c-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="0282c-150">Вы можете использовать любые другие инструменты создания учетной записи пользователя SCC LifeCycle или API, предоставляемые SCC LifeCycle для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="0282c-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="0282c-151">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="0282c-151">Assign users</span></span>
<span data-ttu-id="0282c-152">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="0282c-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="0282c-153">**Чтобы назначить пользователей SCC LifeCycle, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="0282c-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="0282c-154">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="0282c-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="0282c-155">На странице интеграции с приложением **SCC LifeCycle** щелкните **Назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0282c-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="0282c-156">![Назначение пользователей](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="0282c-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="0282c-157">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="0282c-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="0282c-158">![Да](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="0282c-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="0282c-159">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="0282c-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="0282c-160">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0282c-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

