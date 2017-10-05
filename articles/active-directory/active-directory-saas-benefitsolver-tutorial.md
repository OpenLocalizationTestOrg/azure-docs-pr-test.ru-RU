---
title: "Руководство по интеграции Azure Active Directory с Benefitsolver | Документация Майкрософт"
description: "Узнайте, как использовать Benefitsolver вместе с Azure Active Directory для реализации единого входа, автоматической подготовки пользователей и выполнения других задач."
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
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="d1a7f-103">Руководство. Интеграция Azure Active Directory с Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="d1a7f-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="d1a7f-104">Цель данного учебника — показать интеграцию Azure и Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="d1a7f-105">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="d1a7f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="d1a7f-106">действующая подписка Azure;</span><span class="sxs-lookup"><span data-stu-id="d1a7f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d1a7f-107">подписка на Benefitsolver с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="d1a7f-108">После завершения этого руководства пользователи Azure AD, назначенные Benefitsolver, будут иметь возможность единого входа в приложение с помощью инструкций из статьи [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1a7f-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d1a7f-109">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="d1a7f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="d1a7f-110">Включение интеграции приложений для Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="d1a7f-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="d1a7f-111">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d1a7f-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="d1a7f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d1a7f-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="d1a7f-113">Assigning users</span></span>

<span data-ttu-id="d1a7f-114">![Сценарий](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="d1a7f-115">Включение интеграции приложений для Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="d1a7f-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="d1a7f-116">В этом разделе показано, как включить интеграцию приложений для Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="d1a7f-117">Чтобы включить интеграцию приложений для Benefitsolver, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="d1a7f-118">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d1a7f-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d1a7f-120">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d1a7f-121">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="d1a7f-122">![Приложения](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d1a7f-123">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="d1a7f-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="d1a7f-124">![Добавление приложения](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d1a7f-125">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="d1a7f-126">![Добавление приложения из коллекции](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d1a7f-127">В **поле поиска** введите **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="d1a7f-128">![Коллекция приложений](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="d1a7f-129">В области результатов выберите **Benefitsolver** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="d1a7f-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d1a7f-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="d1a7f-131">Configure single sign-on</span></span>

<span data-ttu-id="d1a7f-132">В этом разделе показано, как разрешить пользователям проходить проверку подлинности в Benefitsolver со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="d1a7f-133">Приложение Benefitsolver ожидает проверочные утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию **атрибутов токена SAML** .</span><span class="sxs-lookup"><span data-stu-id="d1a7f-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="d1a7f-134">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="d1a7f-135">![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="d1a7f-136">**Чтобы настроить единый вход, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d1a7f-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="d1a7f-137">На классическом портале Azure на странице интеграции с приложением **Benefitsolver** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d1a7f-138">![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="d1a7f-139">На странице **Как пользователи должны входить в Benefitsolver?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d1a7f-140">![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="d1a7f-141">На странице **Настройка параметров приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="d1a7f-142">![Настройка параметров приложения](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Настройка параметров приложения")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="d1a7f-143">В текстовом поле **URL-адрес для входа** введите **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="d1a7f-144">В текстовом поле **URL-адрес ответа** введите **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="d1a7f-145">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-145">Click **Next**.</span></span>
4. <span data-ttu-id="d1a7f-146">На странице **Настройка единого входа в Benefitsolver** щелкните **Скачать метаданные**, чтобы скачать метаданные, а затем сохраните файл метаданных на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="d1a7f-147">![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="d1a7f-148">Отправьте загруженный файл метаданных в службу поддержки Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d1a7f-149">Настройка единого входа должна выполняться службой поддержки Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="d1a7f-150">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="d1a7f-151">На классическом портале Azure выберите подтверждение конфигурации единого входа, а затем нажмите кнопку **Завершить**, чтобы закрыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d1a7f-152">![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="d1a7f-153">В меню в верхней части экрана выберите пункт **Атрибуты** to open the **SAML Token Атрибуты** .</span><span class="sxs-lookup"><span data-stu-id="d1a7f-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="d1a7f-154">![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="d1a7f-155">Чтобы добавить обязательные сопоставления атрибутов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="d1a7f-156">![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="d1a7f-157">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="d1a7f-157">Attribute Name</span></span> | <span data-ttu-id="d1a7f-158">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="d1a7f-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="d1a7f-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="d1a7f-159">ClientID</span></span> |<span data-ttu-id="d1a7f-160">Это значение необходимо получить у службы поддержки Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="d1a7f-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="d1a7f-161">ClientKey</span></span> |<span data-ttu-id="d1a7f-162">Это значение необходимо получить у службы поддержки Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="d1a7f-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="d1a7f-163">LogoutURL</span></span> |<span data-ttu-id="d1a7f-164">Это значение необходимо получить у службы поддержки Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="d1a7f-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="d1a7f-165">EmployeeID</span></span> |<span data-ttu-id="d1a7f-166">Это значение необходимо получить у службы поддержки Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="d1a7f-167">Для каждой строки данных в приведенной выше таблице нажмите кнопку **добавить атрибут пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="d1a7f-168">В текстовом поле **Имя атрибута** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="d1a7f-169">В текстовом поле **Значение атрибута** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="d1a7f-170">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-170">Click **Complete**.</span></span>
9. <span data-ttu-id="d1a7f-171">Нажмите кнопку **Применить изменения**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="d1a7f-172">Настройка подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="d1a7f-172">Configure user provisioning</span></span>
<span data-ttu-id="d1a7f-173">Чтобы пользователи Azure AD могли выполнять вход в Benefitsolver, они должны быть подготовлены для Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="d1a7f-174">При использовании Benefitsolver данные о сотрудниках находятся в приложении, которое заполняется с помощью файла переписи из вашей информационной системы персонала (обычно каждую ночь).</span><span class="sxs-lookup"><span data-stu-id="d1a7f-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="d1a7f-175">Вы можете использовать любые другие средства создания учетной записи пользователя Benefitsolver или API, предоставляемые Benefitsolver для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="d1a7f-176">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="d1a7f-176">Assigning users</span></span>
<span data-ttu-id="d1a7f-177">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="d1a7f-178">Чтобы назначить пользователей Benefitsolver, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="d1a7f-179">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d1a7f-180">На ** Benefitsolver ** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d1a7f-181">![Назначение пользователей](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="d1a7f-182">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="d1a7f-183">![Да](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="d1a7f-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d1a7f-184">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="d1a7f-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d1a7f-185">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1a7f-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

