---
title: "Руководство по интеграции Azure Active Directory с песочницей Salesforce | Документация Майкрософт"
description: "Узнайте, как использовать песочницу Salesforce вместе с Azure Active Directory для реализации единого входа, автоматической подготовки к работе и многого другого."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="c64a2-103">Учебник. Интеграция Azure Active Directory с песочницей Salesforce</span><span class="sxs-lookup"><span data-stu-id="c64a2-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="c64a2-104">Цель данного учебника — показать интеграцию Azure и песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c64a2-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="c64a2-105">Чтобы оставить отзыв и просмотреть отзывы других пользователей, перейдите на [страницу службы поддержки Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="c64a2-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="c64a2-106">Песочницы позволяет создать несколько копий организации в отдельных средах для различных целей, например для разработки, тестирования и обучения, не подвергая риску данные и приложения в рабочей организации Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c64a2-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="c64a2-107">Дополнительные сведения см. в [статье о песочницах](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="c64a2-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="c64a2-108">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="c64a2-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c64a2-109">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="c64a2-109">A valid Azure subscription</span></span>
* <span data-ttu-id="c64a2-110">Песочница на сайте Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="c64a2-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="c64a2-111">Если у вас еще нет действующей песочницы на сайте Salesforce.com, вам необходимо будет обратиться в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c64a2-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="c64a2-112">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="c64a2-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="c64a2-113">Включение интеграции приложений для песочницы Salesforce</span><span class="sxs-lookup"><span data-stu-id="c64a2-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="c64a2-114">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="c64a2-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="c64a2-115">Включение домена</span><span class="sxs-lookup"><span data-stu-id="c64a2-115">Enabling your domain</span></span>
4. <span data-ttu-id="c64a2-116">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="c64a2-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="c64a2-117">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="c64a2-117">Assigning users</span></span>

<span data-ttu-id="c64a2-118">![Сценарий](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="c64a2-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="c64a2-119">Включение интеграции приложений для песочницы Salesforce</span><span class="sxs-lookup"><span data-stu-id="c64a2-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="c64a2-120">В этом разделе показано, как включить интеграцию приложений для песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c64a2-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="c64a2-121">**Чтобы включить интеграцию приложений для песочницы Salesforce, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c64a2-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="c64a2-122">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="c64a2-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c64a2-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c64a2-124">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="c64a2-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c64a2-125">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="c64a2-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="c64a2-126">![Приложения](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="c64a2-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c64a2-127">Чтобы открыть **коллекцию приложений**, щелкните **Добавить приложение**, затем — **Добавить приложение для использования моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="c64a2-128">![Что необходимо сделать? ](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Что необходимо сделать?")</span><span class="sxs-lookup"><span data-stu-id="c64a2-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="c64a2-129">В **поле поиска** введите **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="c64a2-130">![Коллекция приложений](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="c64a2-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="c64a2-131">В области результатов выберите **Salesforce Sandbox** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="c64a2-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="c64a2-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="c64a2-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="c64a2-133">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="c64a2-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="c64a2-134">В этом разделе показано, как разрешить пользователям проходить проверку подлинности в Salesforce со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="c64a2-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="c64a2-135">**Чтобы настроить единый вход, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c64a2-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="c64a2-136">На странице интеграции с приложением **Salesforce Sandbox** классического портала Azure нажмите кнопку **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c64a2-137">![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c64a2-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="c64a2-138">На странице **Как пользователи должны входить в Salesforce Sandbox?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="c64a2-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="c64a2-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="c64a2-140">На странице **Настроить URL-адрес приложения** в текстовом поле **URL-адрес для входа** введите свой URL-адрес, используя следующий шаблон `http://company.my.salesforce.com`, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="c64a2-141">![Настройка URL-адреса приложения](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="c64a2-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="c64a2-142">Если вы уже настроили единый вход для другого экземпляра Salesforce Sandbox в каталоге, необходимо также настроить параметр **Идентификатор**, задав для него то же значение, что и для параметра **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="c64a2-143">Поле **Идентификатор** можно найти, установив флажок **Показать дополнительные настройки** на странице **Настроить URL-адрес приложения** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c64a2-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="c64a2-144">На странице **Настройка единого входа в Salesforce Sandbox** нажмите кнопку **Скачать сертификат**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c64a2-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="c64a2-145">![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c64a2-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="c64a2-146">В другом окне веб-браузера войдите в свою песочницу Salesforce в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c64a2-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="c64a2-147">В верхнем меню щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="c64a2-148">![Настройка](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="c64a2-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="c64a2-149">В области навигации слева щелкните **Security Controls** (Средства управления безопасностью), а затем — **Параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="c64a2-150">![Параметры единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="c64a2-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="c64a2-151">В разделе «Параметры единого входа» выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c64a2-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="c64a2-152">![Параметры единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="c64a2-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="c64a2-153">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="c64a2-154">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-154">Click **New**.</span></span>
10. <span data-ttu-id="c64a2-155">В разделе «Параметры единого входа SAML» выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c64a2-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="c64a2-156">![Параметры единого входа SAML](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="c64a2-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="c64a2-157">В текстовом поле "Имя" введите имя конфигурации (например, *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="c64a2-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="c64a2-158">На странице **Настройка единого входа в Salesforce Sandbox** классического портала Azure скопируйте значение поля **URL-адрес издателя** и вставьте его в текстовое поле **Издатель**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="c64a2-159">В текстовом поле **Идентификатор сущности** введите **https://test.salesforce.com**, если это первый экземпляр Salesforce Sandbox, добавляемый в каталог.</span><span class="sxs-lookup"><span data-stu-id="c64a2-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="c64a2-160">Если вы уже добавили экземпляр Salesforce Sandbox, то для параметра **Идентификатор сущности** введите значение **URL-адрес входа** в следующем формате: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c64a2-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="c64a2-161">Чтобы отправить скачанный сертификат, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="c64a2-162">В поле **SAML Identity Type** (Тип удостоверения SAML) выберите значение **Assertion contains the Federation ID from the User object** (Проверочное утверждение содержит идентификатор федерации из объекта User).</span><span class="sxs-lookup"><span data-stu-id="c64a2-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="c64a2-163">В поле **SAML Identity Location** (Расположение удостоверения SAML) выберите значение **Identity is in the NameIdentifier element of the Subject statement** (Удостоверение находится в элементе NameIdentifier оператора Subject).</span><span class="sxs-lookup"><span data-stu-id="c64a2-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="c64a2-164">На странице **Настройка единого входа в Salesforce Sandbox** классического портала Azure скопируйте значение поля **URL-адрес удаленного входа** и вставьте его в текстовое поле **URL-адрес входа поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="c64a2-165">SFDC не поддерживает выход SAML.</span><span class="sxs-lookup"><span data-stu-id="c64a2-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="c64a2-166">Чтобы обойти эту проблему, вставьте значение https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0 в текстовое поле **URL-адрес для выхода поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="c64a2-167">В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="c64a2-168">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-168">Click **Save**.</span></span>
11. <span data-ttu-id="c64a2-169">На классическом портале Azure выберите подтверждение конфигурации единого входа, а затем нажмите кнопку **Завершить**, чтобы закрыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="c64a2-170">![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c64a2-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="c64a2-171">Включение домена</span><span class="sxs-lookup"><span data-stu-id="c64a2-171">Enable your domain</span></span>
<span data-ttu-id="c64a2-172">В этом разделе предполагается, что вы уже создали домен.</span><span class="sxs-lookup"><span data-stu-id="c64a2-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="c64a2-173">Дополнительные сведения см. в разделе об [определении имени домена](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="c64a2-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="c64a2-174">**Выполните следующие действия, чтобы включить домен:**</span><span class="sxs-lookup"><span data-stu-id="c64a2-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="c64a2-175">В области навигации слева щелкните **Управление доменами**, затем — **Мой домен**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="c64a2-176">![Мой домен](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="c64a2-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c64a2-177">Убедитесь в правильности настройки домена.</span><span class="sxs-lookup"><span data-stu-id="c64a2-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="c64a2-178">В разделе **Login Page Settings** (Параметры страницы входа) щелкните **Изменить**, а затем для параметра **Authentication Service** (Служба проверки подлинности) выберите имя параметра единого входа SAML из предыдущего раздела, после чего щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="c64a2-179">![Мой домен](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="c64a2-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="c64a2-180">После настройки домена для входа в песочницу Salesforce пользователям необходимо будет использовать URL-адрес домена.</span><span class="sxs-lookup"><span data-stu-id="c64a2-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="c64a2-181">Чтобы получить значение URL-адреса, щелкните профиль единого входа, созданный в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="c64a2-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="c64a2-182">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="c64a2-182">Configure user provisioning</span></span>
<span data-ttu-id="c64a2-183">В этом разделе показано, как включить подготовку учетных записей пользователей Active Directory для песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c64a2-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="c64a2-184">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c64a2-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="c64a2-185">На портале Salesforce в верхней области навигации выберите свое имя, чтобы открыть меню пользователя:</span><span class="sxs-lookup"><span data-stu-id="c64a2-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="c64a2-186">![Мои параметры](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Мои параметры")</span><span class="sxs-lookup"><span data-stu-id="c64a2-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="c64a2-187">В меню пользователя выберите **Мои параметры**, чтобы открыть страницу **Мои параметры**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="c64a2-188">В области навигации слева щелкните **Личный**, чтобы развернуть раздел "Личный", и щелкните **Reset My Security Token** (Сброс маркера безопасности).</span><span class="sxs-lookup"><span data-stu-id="c64a2-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="c64a2-189">![Мои параметры](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Мои параметры")</span><span class="sxs-lookup"><span data-stu-id="c64a2-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="c64a2-190">На странице **Reset My Security Token** (Сброс токена безопасности) щелкните **Reset Security Token** (Сбросить токен безопасности), чтобы запросить электронное сообщение, содержащее ваш токен безопасности Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="c64a2-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="c64a2-191">![Новый маркер](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "Новый маркер")</span><span class="sxs-lookup"><span data-stu-id="c64a2-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="c64a2-192">Проверьте папку "Входящие" электронной почты на наличие сообщения от Salesforce.com со строкой темы**salesforce.com.com security confirmation**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="c64a2-193">Откройте это сообщение и скопируйте значение маркера безопасности.</span><span class="sxs-lookup"><span data-stu-id="c64a2-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="c64a2-194">На странице интеграции приложений **Salesforce Sandbox** классического портала управления Azure щелкните **Настроить подготовку учетных записей пользователей**, чтобы открыть диалоговое окно **Настроить подготовку учетных записей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="c64a2-195">![Настроить подготовку учетных записей пользователей](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Настроить подготовку учетных записей пользователей")</span><span class="sxs-lookup"><span data-stu-id="c64a2-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="c64a2-196">На странице **Введите учетные данные песочницы Salesforce, чтобы включить автоматическую подготовку учетных записей пользователей** укажите следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="c64a2-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="c64a2-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="c64a2-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="c64a2-198">В текстовом поле **Имя пользователя администратора Salesforce Sandbox** введите имя учетной записи Salesforce Sandbox с профилем **системного администратора** в Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="c64a2-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="c64a2-199">В текстовом поле **Пароль администратора Salesforce Sandbox** введите пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c64a2-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="c64a2-200">В текстовом поле **Токен безопасности пользователя** вставьте значение токена безопасности.</span><span class="sxs-lookup"><span data-stu-id="c64a2-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="c64a2-201">Щелкните **Проверить** для проверки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c64a2-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="c64a2-202">Нажмите кнопку **Далее**, чтобы открыть страницу **Подтверждение**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="c64a2-203">На странице **Подтверждение** щелкните **Завершить**, чтобы сохранить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="c64a2-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="c64a2-204">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="c64a2-204">Assigning users</span></span>

<span data-ttu-id="c64a2-205">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="c64a2-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="c64a2-206">**Чтобы назначить пользователей песочницы Salesforce, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c64a2-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="c64a2-207">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="c64a2-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c64a2-208">На странице интеграции с приложением **Salesforce Sandbox** щелкните **Назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c64a2-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="c64a2-209">![Назначение пользователей](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="c64a2-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="c64a2-210">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="c64a2-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="c64a2-211">![Да](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="c64a2-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c64a2-212">Подождите 10 минут и убедитесь, что учетная запись синхронизирована с песочницей Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c64a2-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="c64a2-213">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="c64a2-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="c64a2-214">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c64a2-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

