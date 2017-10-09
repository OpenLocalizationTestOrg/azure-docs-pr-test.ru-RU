---
title: "Руководство по интеграции Azure Active Directory с песочницей Salesforce | Документация Майкрософт"
description: "Узнайте, как toouse песочницы Salesforce с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!."
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
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="b7c65-103">Учебник. Интеграция Azure Active Directory с песочницей Salesforce</span><span class="sxs-lookup"><span data-stu-id="b7c65-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="b7c65-104">Цель этого учебника Hello — tooshow hello интеграцию Azure и песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="b7c65-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="b7c65-105">Для обратной связи, в разделе hello [страницы поддержки Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="b7c65-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="b7c65-106">"Песочницы" предоставляют вы hello возможность toocreate несколько копий организации в отдельных средах для разных целей: разработки, тестирования и обучения — без нарушения hello данных и приложений в вашей рабочей среде Salesforce организация.</span><span class="sxs-lookup"><span data-stu-id="b7c65-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="b7c65-107">Дополнительные сведения см. в [статье о песочницах](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="b7c65-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="b7c65-108">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b7c65-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="b7c65-109">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="b7c65-109">A valid Azure subscription</span></span>
* <span data-ttu-id="b7c65-110">Песочница на сайте Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="b7c65-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="b7c65-111">Если вы еще нет действительной песочницы в Salesforce.com, то необходимо toocontact Salesforce.</span><span class="sxs-lookup"><span data-stu-id="b7c65-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="b7c65-112">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="b7c65-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="b7c65-113">Включение интеграции приложений hello для песочницы Salesforce</span><span class="sxs-lookup"><span data-stu-id="b7c65-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="b7c65-114">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="b7c65-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="b7c65-115">Включение домена</span><span class="sxs-lookup"><span data-stu-id="b7c65-115">Enabling your domain</span></span>
4. <span data-ttu-id="b7c65-116">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="b7c65-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="b7c65-117">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="b7c65-117">Assigning users</span></span>

<span data-ttu-id="b7c65-118">![Сценарий](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="b7c65-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="b7c65-119">Включить hello интеграции приложений для песочницы Salesforce</span><span class="sxs-lookup"><span data-stu-id="b7c65-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="b7c65-120">Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="b7c65-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="b7c65-121">**Интеграция приложения hello tooenable для песочницы Salesforce, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b7c65-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7c65-122">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="b7c65-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="b7c65-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="b7c65-124">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="b7c65-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="b7c65-125">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="b7c65-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="b7c65-126">![Приложения](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="b7c65-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="b7c65-127">tooopen hello **коллекцию приложений**, нажмите кнопку **добавить приложение**и нажмите кнопку **добавить приложение для моей организации toouse**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="b7c65-128">![Что вам требуется toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Что вам требуется toodo?")</span><span class="sxs-lookup"><span data-stu-id="b7c65-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="b7c65-129">В hello **поле поиска**, тип **песочницы Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="b7c65-130">![Коллекция приложений](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="b7c65-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="b7c65-131">В области результатов hello выберите **песочницы Salesforce**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b7c65-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="b7c65-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="b7c65-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="b7c65-133">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="b7c65-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="b7c65-134">Цель этого раздела Hello — toooutline как tooSalesforce tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="b7c65-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="b7c65-135">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="b7c65-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7c65-136">В классический портал Azure, на hello hello **песочницы Salesforce** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b7c65-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="b7c65-137">![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="b7c65-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="b7c65-138">На hello **предпочитаемый как toosign пользователей на tooSalesforce "песочницы"** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="b7c65-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="b7c65-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="b7c65-140">На hello **настроить URL-адрес приложения** страницы в hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello `http://company.my.salesforce.com`и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="b7c65-141">![Настройка URL-адреса приложения](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="b7c65-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="b7c65-142">Если вы уже настроили единого входа для другого экземпляра песочницы Salesforce в вашем каталоге, то необходимо также настроить hello **идентификатор** toohave hello совпадает со значением hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="b7c65-143">Hello **идентификатор** поле можно найти путем проверки hello **Показывать дополнительные параметры** флажок на hello **настроить URL-адрес приложения** страницы диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b7c65-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="b7c65-144">На hello **настройки единого входа в песочницу Salesforce** щелкните **загрузки сертификата**, а затем сохраните файл сертификата hello на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b7c65-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="b7c65-145">![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="b7c65-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="b7c65-146">В другом окне веб-браузера войдите в свою песочницу Salesforce в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b7c65-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="b7c65-147">В меню в верхней части hello hello выберите **установки**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="b7c65-148">![Настройка](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="b7c65-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="b7c65-149">Hello hello левой панели навигации щелкните **управления безопасностью**, а затем нажмите кнопку **параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="b7c65-150">![Параметры единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="b7c65-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="b7c65-151">На hello раздел параметров единого входа выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b7c65-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="b7c65-152">![Параметры единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="b7c65-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="b7c65-153">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="b7c65-154">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-154">Click **New**.</span></span>
10. <span data-ttu-id="b7c65-155">На hello SAML единого входа «параметры» выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b7c65-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="b7c65-156">![Параметры единого входа SAML](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="b7c65-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="b7c65-157">Hello в текстовое поле имя, введите имя hello hello конфигурации (например: *SPSSOWAAD\_тест*).</span><span class="sxs-lookup"><span data-stu-id="b7c65-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="b7c65-158">В классический портал Azure, на hello hello **настройки единого входа в песочницу Salesforce** диалоговой страницы, копировать hello **URL-адрес издателя** значение, а затем вставьте его в hello **издателя**текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b7c65-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="b7c65-159">В hello **идентификатор сущности** введите **https://test.salesforce.com** Если hello добавляется каталог tooyour первый экземпляр песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="b7c65-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="b7c65-160">При добавлении экземпляра песочницы Salesforce, а затем для hello **идентификатор сущности** типа в hello **на URL-адрес входа**, которые должны быть в следующем формате:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="b7c65-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="b7c65-161">Нажмите кнопку **Обзор** tooupload hello загрузить сертификат.</span><span class="sxs-lookup"><span data-stu-id="b7c65-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="b7c65-162">Как **типа удостоверения SAML**выберите **утверждение, содержащее hello идентификатор федерации из объекта пользователя hello**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="b7c65-163">Как **расположения удостоверения SAML**выберите **удостоверение находится в элемент hello NameIdentifier оператора Subject hello**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="b7c65-164">В классический портал Azure, на hello hello **настройки единого входа в песочницу Salesforce** диалоговой страницы, копировать hello **URL-адрес удаленного входа** значение, а затем вставьте его в hello **поставщика удостоверений URL-адрес входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b7c65-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="b7c65-165">SFDC не поддерживает выход SAML.</span><span class="sxs-lookup"><span data-stu-id="b7c65-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="b7c65-166">Чтобы избежать этого, вставьте «https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0» в hello **URL-адрес выхода поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b7c65-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="b7c65-167">В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="b7c65-168">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-168">Click **Save**.</span></span>
11. <span data-ttu-id="b7c65-169">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b7c65-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="b7c65-170">![Настройка единого входа](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="b7c65-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="b7c65-171">Включение домена</span><span class="sxs-lookup"><span data-stu-id="b7c65-171">Enable your domain</span></span>
<span data-ttu-id="b7c65-172">В этом разделе предполагается, что вы уже создали домен.</span><span class="sxs-lookup"><span data-stu-id="b7c65-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="b7c65-173">Дополнительные сведения см. в разделе об [определении имени домена](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="b7c65-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="b7c65-174">**tooenable к домену, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="b7c65-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7c65-175">Hello панели навигации слева щелкните **Управление доменами**, а затем нажмите кнопку **Мой домен.**</span><span class="sxs-lookup"><span data-stu-id="b7c65-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="b7c65-176">![Мой домен](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="b7c65-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="b7c65-177">Убедитесь в правильности настройки домена.</span><span class="sxs-lookup"><span data-stu-id="b7c65-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="b7c65-178">В hello **параметры страницы входа** щелкните **изменить**, затем, по мере **службы проверки подлинности**, выберите имя hello hello SAML единого входа параметр из предыдущего hello статьи, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="b7c65-179">![Мой домен](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="b7c65-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="b7c65-180">Как только домен настроен, пользователям следует использовать hello домена URL-адрес toologin toohello песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="b7c65-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="b7c65-181">значение hello tooget hello URL-адреса, щелкните профиль единого входа hello, созданный в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="b7c65-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="b7c65-182">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="b7c65-182">Configure user provisioning</span></span>
<span data-ttu-id="b7c65-183">Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooSalesforce "песочницы".</span><span class="sxs-lookup"><span data-stu-id="b7c65-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="b7c65-184">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b7c65-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7c65-185">На портале Salesforce hello hello верхней панели навигации выберите ваш tooexpand имя меню пользователя:</span><span class="sxs-lookup"><span data-stu-id="b7c65-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="b7c65-186">![Мои параметры](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Мои параметры")</span><span class="sxs-lookup"><span data-stu-id="b7c65-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="b7c65-187">Меню пользователя, выберите **мои параметры** tooopen вашей **мои параметры** страницы.</span><span class="sxs-lookup"><span data-stu-id="b7c65-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="b7c65-188">Hello левой панели щелкните **личных** tooexpand hello личный раздел, а затем нажмите кнопку **Сброс личного токена безопасности**:</span><span class="sxs-lookup"><span data-stu-id="b7c65-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="b7c65-189">![Мои параметры](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Мои параметры")</span><span class="sxs-lookup"><span data-stu-id="b7c65-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="b7c65-190">На hello **Сброс личного токена безопасности** щелкните **сбросить токен безопасности** toorequest сообщение электронной почты, содержащее ваш токен безопасности Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="b7c65-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="b7c65-191">![Новый маркер](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "Новый маркер")</span><span class="sxs-lookup"><span data-stu-id="b7c65-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="b7c65-192">Проверьте папку "Входящие" электронной почты на наличие сообщения от Salesforce.com со строкой темы**salesforce.com.com security confirmation**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="b7c65-193">Просмотрите этот электронной почты и скопируйте hello значение токена безопасности.</span><span class="sxs-lookup"><span data-stu-id="b7c65-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="b7c65-194">В классический портал Azure, на hello hello **песочницы salesforce** странице интеграции приложения щелкните **Настройка подготовки пользователя** tooopen hello **Настройка подготовки пользователя**диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b7c65-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="b7c65-195">![Настроить подготовку учетных записей пользователей](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Настроить подготовку учетных записей пользователей")</span><span class="sxs-lookup"><span data-stu-id="b7c65-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="b7c65-196">На hello **введите вашей песочницы Salesforce учетные данные tooenable автоматическую подготовку пользователей** укажите следующие параметры конфигурации hello:</span><span class="sxs-lookup"><span data-stu-id="b7c65-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="b7c65-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="b7c65-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="b7c65-198">В hello **имя пользователя администратора песочницы Salesforce** введите имя учетной записи Salesforce, имеет hello **системный администратор** профиля в Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="b7c65-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="b7c65-199">В hello **пароль администратора песочницы Salesforce** текстового поля, типа hello пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b7c65-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="b7c65-200">В hello **токен безопасности пользователя** текстовое значение токена безопасности hello вставки.</span><span class="sxs-lookup"><span data-stu-id="b7c65-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="b7c65-201">Нажмите кнопку **проверки** tooverify конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b7c65-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="b7c65-202">Нажмите кнопку hello **Далее** hello tooopen кнопку **Подтверждение** страницы.</span><span class="sxs-lookup"><span data-stu-id="b7c65-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="b7c65-203">На hello **Подтверждение** щелкните **завершить** toosave конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b7c65-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="b7c65-204">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="b7c65-204">Assigning users</span></span>

<span data-ttu-id="b7c65-205">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="b7c65-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="b7c65-206">**Пользователи tooassign tooSalesforce "песочницы", выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b7c65-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7c65-207">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="b7c65-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="b7c65-208">На hello ** песочницы Salesforce ** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b7c65-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="b7c65-209">![Назначение пользователей](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="b7c65-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="b7c65-210">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="b7c65-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="b7c65-211">![Да](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="b7c65-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="b7c65-212">Теперь следует подождать 10 минут и убедиться в устранении учетной записи hello синхронизированные tooSalesforce "песочницы".</span><span class="sxs-lookup"><span data-stu-id="b7c65-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="b7c65-213">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b7c65-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="b7c65-214">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b7c65-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

