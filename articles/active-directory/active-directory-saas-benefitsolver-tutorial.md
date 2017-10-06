---
title: "Руководство по интеграции Azure Active Directory с Benefitsolver | Документация Майкрософт"
description: "Узнайте, как toouse Benefitsolver с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="4c6f0-103">Руководство. Интеграция Azure Active Directory с Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="4c6f0-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="4c6f0-104">Цель этого учебника Hello — tooshow hello интеграцию Azure и Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="4c6f0-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4c6f0-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="4c6f0-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="4c6f0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="4c6f0-107">подписка на Benefitsolver с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="4c6f0-108">После завершения этого учебника, пользователи hello Azure AD, назначенные tooBenefitsolver будут может toosingle входа в приложение hello hello [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c6f0-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="4c6f0-109">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="4c6f0-110">Включение интеграции приложений hello для Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="4c6f0-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="4c6f0-111">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="4c6f0-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="4c6f0-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="4c6f0-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="4c6f0-113">Assigning users</span></span>

<span data-ttu-id="4c6f0-114">![Сценарий](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="4c6f0-115">Включение интеграции приложений hello для Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="4c6f0-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="4c6f0-116">Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="4c6f0-117">интеграции приложения hello tooenable для Benefitsolver, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="4c6f0-118">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="4c6f0-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="4c6f0-120">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="4c6f0-121">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="4c6f0-122">![Приложения](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="4c6f0-123">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="4c6f0-124">![Добавление приложения](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="4c6f0-125">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="4c6f0-126">![Добавление приложения из коллекции](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="4c6f0-127">В hello **поле поиска**, тип **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="4c6f0-128">![Коллекция приложений](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="4c6f0-129">В области результатов hello выберите **Benefitsolver**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="4c6f0-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="4c6f0-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="4c6f0-131">Configure single sign-on</span></span>

<span data-ttu-id="4c6f0-132">Цель этого раздела Hello — toooutline как tooBenefitsolver tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="4c6f0-133">Приложение Benefitsolver ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена saml** конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="4c6f0-134">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="4c6f0-135">![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="4c6f0-136">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="4c6f0-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c6f0-137">В классический портал Azure, на hello hello **Benefitsolver** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4c6f0-138">![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="4c6f0-139">На hello **предпочитаемый как toosign пользователей на tooBenefitsolver** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="4c6f0-140">![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="4c6f0-141">На hello **Настройка параметров приложения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4c6f0-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="4c6f0-142">![Настройка параметров приложения](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Настройка параметров приложения")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="4c6f0-143">В hello **на URL-адрес входа** введите **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="4c6f0-144">В hello **URL-адрес ответа** введите **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="4c6f0-145">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-145">Click **Next**.</span></span>
4. <span data-ttu-id="4c6f0-146">На hello **настроить единый вход в Benefitsolver** страницы, toodownload метаданные, нажмите кнопку **загрузить метаданные**, а затем сохраните файл метаданных hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="4c6f0-147">![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="4c6f0-148">Отправьте hello загружены метаданные файла tooyour Benefitsolver поддержки.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="4c6f0-149">Сотрудники службы поддержки Benefitsolver имеет toodo hello фактическую настройку единого входа.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="4c6f0-150">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="4c6f0-151">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4c6f0-152">![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="4c6f0-153">В меню в верхней части hello hello выберите **атрибуты** tooopen hello **атрибутов токена SAML** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="4c6f0-154">![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="4c6f0-155">сопоставления атрибутов hello необходимые tooadd, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="4c6f0-156">![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="4c6f0-157">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="4c6f0-157">Attribute Name</span></span> | <span data-ttu-id="4c6f0-158">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="4c6f0-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="4c6f0-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="4c6f0-159">ClientID</span></span> |<span data-ttu-id="4c6f0-160">Для команды поддержки Benefitsolver это значение требуется tooget.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="4c6f0-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="4c6f0-161">ClientKey</span></span> |<span data-ttu-id="4c6f0-162">Для команды поддержки Benefitsolver это значение требуется tooget.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="4c6f0-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="4c6f0-163">LogoutURL</span></span> |<span data-ttu-id="4c6f0-164">Для команды поддержки Benefitsolver это значение требуется tooget.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="4c6f0-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="4c6f0-165">EmployeeID</span></span> |<span data-ttu-id="4c6f0-166">Для команды поддержки Benefitsolver это значение требуется tooget.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="4c6f0-167">Для каждой строки данных в таблице hello выше, щелкните **добавить атрибут пользователя**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="4c6f0-168">В hello **имя атрибута** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="4c6f0-169">В hello **значение атрибута** текстовое поле, значение атрибута выберите hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="4c6f0-170">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-170">Click **Complete**.</span></span>
9. <span data-ttu-id="4c6f0-171">Нажмите кнопку **Применить изменения**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="4c6f0-172">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="4c6f0-172">Configure user provisioning</span></span>
<span data-ttu-id="4c6f0-173">В порядке tooenable toolog пользователей Azure AD в Benefitsolver их необходимо подготовить в Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="4c6f0-174">В случае Benefitsolver hello данные о сотрудниках — в приложении, который заполняется с использованием файла переписи населения из информационной системы Персонала системы (обычно ночное время).</span><span class="sxs-lookup"><span data-stu-id="4c6f0-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="4c6f0-175">Можно использовать любые другие Benefitsolver пользователя средства создания учетных записей или интерфейсы API, предоставляемые Benefitsolver tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="4c6f0-176">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="4c6f0-176">Assigning users</span></span>
<span data-ttu-id="4c6f0-177">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="4c6f0-178">tooBenefitsolver tooassign пользователей, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4c6f0-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="4c6f0-179">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4c6f0-180">На hello ** Benefitsolver ** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="4c6f0-181">![Назначение пользователей](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="4c6f0-182">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="4c6f0-183">![Да](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="4c6f0-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4c6f0-184">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f0-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="4c6f0-185">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c6f0-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

