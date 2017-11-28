---
title: "Руководство по интеграции Azure Active Directory с Qualtrics | Документация Майкрософт"
description: "Узнайте, как использовать Qualtrics вместе с Azure Active Directory для реализации единого входа, автоматической подготовки пользователей и выполнения других задач."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="c20c0-103">Учебник. Интеграция Azure Active Directory с Qualtrics</span><span class="sxs-lookup"><span data-stu-id="c20c0-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="c20c0-104">Цель данного учебника — показать интеграцию Azure и Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="c20c0-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="c20c0-105">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="c20c0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c20c0-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="c20c0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c20c0-107">Подписка Qualtrics с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c20c0-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="c20c0-108">После завершения этого руководства пользователи Azure AD, назначенные Qualtrics, будут иметь возможность единого входа в приложение на веб-сайте компании Qualtrics (вход, инициированный поставщиком услуг) или с помощью инструкций из статьи [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c20c0-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c20c0-109">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="c20c0-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="c20c0-110">Включение интеграции приложений для Qualtrics</span><span class="sxs-lookup"><span data-stu-id="c20c0-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="c20c0-111">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="c20c0-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="c20c0-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="c20c0-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="c20c0-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="c20c0-113">Assigning users</span></span>

<span data-ttu-id="c20c0-114">![Сценарий](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="c20c0-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="c20c0-115">Включение интеграции приложений для Qualtrics</span><span class="sxs-lookup"><span data-stu-id="c20c0-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="c20c0-116">В этом разделе показано, как включить интеграцию приложений для Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="c20c0-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="c20c0-117">**Чтобы включить интеграцию приложений для Qualtrics, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c20c0-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="c20c0-118">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c20c0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="c20c0-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c20c0-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c20c0-120">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="c20c0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c20c0-121">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="c20c0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="c20c0-122">![Приложения](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="c20c0-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c20c0-123">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="c20c0-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="c20c0-124">![Добавление приложения](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="c20c0-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c20c0-125">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="c20c0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="c20c0-126">![Добавление приложения из коллекции](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="c20c0-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c20c0-127">В **поле поиска** введите **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="c20c0-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="c20c0-128">![Коллекция приложений](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="c20c0-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="c20c0-129">В области результатов выберите **Qualtrics** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="c20c0-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="c20c0-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="c20c0-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c20c0-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="c20c0-131">Configure single sign-on</span></span>

<span data-ttu-id="c20c0-132">В этом разделе показано, как разрешить пользователям проходить аутентификацию в Qualtrics со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="c20c0-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="c20c0-133">**Чтобы настроить единый вход, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c20c0-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="c20c0-134">На классическом портале Azure на странице интеграции с приложением **Qualtrics** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c20c0-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c20c0-135">![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c20c0-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="c20c0-136">На странице **Как пользователи должны входить в Qualtrics?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c20c0-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="c20c0-137">![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c20c0-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="c20c0-138">На странице **Настроить URL-адрес приложения** в текстовом поле **URL-адрес входа в Qualtrics** введите свой URL-адрес (например, *https://ssotest2ut1.qualtrics.com*) и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c20c0-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="c20c0-139">![Настройка URL-адреса приложения](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="c20c0-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="c20c0-140">На странице **Настройка единого входа в Qualtrics** щелкните **Скачать метаданные**, а затем сохраните файл метаданных на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c20c0-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="c20c0-141">![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c20c0-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="c20c0-142">Отправьте файл метаданных в группу поддержки Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="c20c0-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c20c0-143">Настройка единого входа должна выполняться группой поддержки Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="c20c0-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="c20c0-144">Сразу же после завершения настройки вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="c20c0-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="c20c0-145">На классическом портале Azure выберите подтверждение конфигурации единого входа, а затем нажмите кнопку **Завершить**, чтобы закрыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c20c0-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c20c0-146">![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c20c0-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="c20c0-147">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="c20c0-147">Configure user provisioning</span></span>

<span data-ttu-id="c20c0-148">Действие для настройки подготовки пользователей в Qualtrics отсутствует.</span><span class="sxs-lookup"><span data-stu-id="c20c0-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="c20c0-149">Когда назначенный пользователь пытается войти в Qualtrics с помощью панели доступа, Qualtrics проверяет, существует ли данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="c20c0-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="c20c0-150">Если учетная запись пользователя отсутствует, Qualtrics автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="c20c0-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="c20c0-151">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="c20c0-151">Assign users</span></span>
<span data-ttu-id="c20c0-152">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="c20c0-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="c20c0-153">**Чтобы назначить пользователей Qualtrics, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c20c0-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="c20c0-154">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="c20c0-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c20c0-155">На странице интеграции с приложением **Qualtrics** щелкните **Назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c20c0-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="c20c0-156">![Назначение пользователей](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="c20c0-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="c20c0-157">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="c20c0-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="c20c0-158">![Да](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="c20c0-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c20c0-159">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="c20c0-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="c20c0-160">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c20c0-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

