---
title: "Руководство по интеграции Azure Active Directory с облачной платформой SAP HANA | Документация Майкрософт"
description: "Узнайте, как toouse облачной платформы SAP HANA с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="f73a3-103">Учебник. Интеграция Azure Active Directory с облачной платформой SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f73a3-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="f73a3-104">Цель этого учебника Hello — tooshow hello интеграцию Azure и облачная платформа SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="f73a3-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="f73a3-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f73a3-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="f73a3-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="f73a3-106">A valid Azure subscription</span></span>
* <span data-ttu-id="f73a3-107">Учетная запись облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="f73a3-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="f73a3-108">После завершения этого учебника пользователи Azure AD, назначенные облачной платформы HANA будет tooSAP может toosingle входа в приложение hello hello Здравствуйте, [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f73a3-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="f73a3-109">Необходима toodeploy собственное приложение или подписаться на один tootest учетной записи входа в вашей облачной платформы SAP HANA tooan приложения.</span><span class="sxs-lookup"><span data-stu-id="f73a3-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="f73a3-110">В этом учебнике приложение развертывается в учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="f73a3-111">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="f73a3-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="f73a3-112">Включение интеграции приложений hello для облачной платформы SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f73a3-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="f73a3-113">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="f73a3-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="f73a3-114">Присвоение пользователю роли tooa</span><span class="sxs-lookup"><span data-stu-id="f73a3-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="f73a3-115">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="f73a3-115">Assigning users</span></span>

<span data-ttu-id="f73a3-116">![Сценарий](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="f73a3-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="f73a3-117">Включение интеграции приложений hello для облачной платформы SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f73a3-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="f73a3-118">Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="f73a3-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="f73a3-119">**Интеграция приложения hello tooenable для облачной платформы SAP HANA, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="f73a3-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="f73a3-120">В hello портала управления Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="f73a3-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f73a3-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="f73a3-122">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="f73a3-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f73a3-123">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="f73a3-124">![Приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="f73a3-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="f73a3-125">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="f73a3-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="f73a3-126">![Добавление приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="f73a3-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="f73a3-127">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="f73a3-128">![Добавление приложения из коллекции](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="f73a3-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="f73a3-129">В hello **поле поиска**, тип **облачной платформы SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="f73a3-130">![Коллекция приложений](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="f73a3-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="f73a3-131">В области результатов hello выберите **облачной платформы SAP HANA**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="f73a3-132">![SAP HANA](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP HANA")</span><span class="sxs-lookup"><span data-stu-id="f73a3-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="f73a3-133">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="f73a3-133">Configure single sign-on</span></span>

<span data-ttu-id="f73a3-134">Цель этого раздела Hello — toooutline, каким образом пользователи tooenable tooauthenticate tooSAP HANA облачной платформы с помощью учетной записи в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="f73a3-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="f73a3-135">В рамках этой процедуры, необходимые tooupload клиента tooyour облачной платформы SAP HANA сертификат в кодировке base-64.</span><span class="sxs-lookup"><span data-stu-id="f73a3-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="f73a3-136">Если вы не знакомы с этой процедурой, см. раздел [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="f73a3-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="f73a3-137">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="f73a3-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="f73a3-138">В классический портал Azure, на hello hello **облачной платформы SAP HANA** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа**диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f73a3-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="f73a3-139">![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="f73a3-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="f73a3-140">На hello **предпочитаемый как toosign пользователей на tooSAP облачной платформы HANA** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="f73a3-141">![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="f73a3-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="f73a3-142">В другом окне браузера Войдите на toohello облачной платформы SAP HANA панелей в https://account. \<узла Альбомная\>.ondemand.com/cockpit (например: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="f73a3-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="f73a3-143">Нажмите кнопку hello **доверия** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f73a3-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="f73a3-144">![Доверие](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Доверие")</span><span class="sxs-lookup"><span data-stu-id="f73a3-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="f73a3-145">В раздел управления доверием выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f73a3-146">![Получение метаданных](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Получение метаданных")</span><span class="sxs-lookup"><span data-stu-id="f73a3-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="f73a3-147">Нажмите кнопку hello **локальный поставщик службы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f73a3-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="f73a3-148">Щелкните toodownload hello файл метаданных облачной платформы SAP HANA, **получить метаданные**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="f73a3-149">Hello Azure Active классического портала на hello **настроить URL-адрес приложения** страницы, выполните следующие шаги hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="f73a3-150">![Настройка URL-адреса приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="f73a3-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="f73a3-151">В hello **на URL-адрес входа** textbox hello введите URL-адрес, используемый вашей toosign пользователей в вашей **облачной платформы SAP HANA** приложения.</span><span class="sxs-lookup"><span data-stu-id="f73a3-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="f73a3-152">Это URL-адрес защищенного ресурса в приложении облачной платформы SAP HANA для конкретной учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="f73a3-153">Hello URL-адрес основан на hello следующий шаблон: *https://\<applicationName\>\<accountName\>.\< Альбомная узла\>.ondemand.com/\<путь\_для\_защищенных\_ресурсов\>*  (например: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="f73a3-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="f73a3-154">Это URL-адрес hello в приложении облачной платформы SAP HANA, требующий hello tooauthenticate пользователя.</span><span class="sxs-lookup"><span data-stu-id="f73a3-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="f73a3-155">Откройте файл метаданных облачной платформы SAP HANA hello загружены, а затем найдите hello **NS3: assertionconsumerservice** тег.</span><span class="sxs-lookup"><span data-stu-id="f73a3-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="f73a3-156">Скопируйте значение hello hello **расположение** атрибута, а затем вставьте его в hello **URL-адрес SAP HANA облачной платформы ответа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="f73a3-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="f73a3-157">На hello **настроить единый вход в облачную платформу SAP HANA** страницы, toodownload метаданные, нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f73a3-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="f73a3-158">![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="f73a3-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="f73a3-159">На hello панель для облачной платформы SAP HANA, в hello **локальный поставщик службы** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f73a3-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f73a3-160">![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Управление доверием")</span><span class="sxs-lookup"><span data-stu-id="f73a3-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="f73a3-161">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="f73a3-162">Для параметра **Configuration Type** (Тип конфигурации) выберите значение **Custom** (Настраиваемая).</span><span class="sxs-lookup"><span data-stu-id="f73a3-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="f73a3-163">Как **локальное имя поставщика**, оставьте значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="f73a3-164">toogenerate **ключа подписи** и **сертификат подписи** пары ключей, нажмите кнопку **создать пару ключей**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="f73a3-165">Для параметра **Principal Propagation** (Распространение субъектов) выберите значение **Disabled** (Отключено).</span><span class="sxs-lookup"><span data-stu-id="f73a3-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="f73a3-166">Для параметра **Force Authentication** (Принудительная аутентификация) выберите значение **Disabled** (Отключено).</span><span class="sxs-lookup"><span data-stu-id="f73a3-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="f73a3-167">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-167">Click **Save**.</span></span>

9. <span data-ttu-id="f73a3-168">Нажмите кнопку hello **доверенного поставщика удостоверений** , а затем щелкните **добавить доверенного поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="f73a3-169">![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Управление доверием")</span><span class="sxs-lookup"><span data-stu-id="f73a3-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="f73a3-170">toomanage hello список доверенных поставщиков удостоверений, необходимо toohave выбранным hello конфигурации пользовательского типа в hello раздел локальный поставщик службы.</span><span class="sxs-lookup"><span data-stu-id="f73a3-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="f73a3-171">Для типа конфигурации по умолчанию у вас есть toohello нередактируемые неявное доверие SAP ID Service.</span><span class="sxs-lookup"><span data-stu-id="f73a3-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="f73a3-172">Для значения «Нет» параметры доверия отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="f73a3-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="f73a3-173">Нажмите кнопку hello **Общие** , а затем щелкните **Обзор** tooupload hello скачать файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="f73a3-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="f73a3-174">![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Управление доверием")</span><span class="sxs-lookup"><span data-stu-id="f73a3-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="f73a3-175">После передачи файла метаданных hello hello значения для **-URL**, **URL-адрес единого выхода** и **сертификат подписи** заполняются автоматически.</span><span class="sxs-lookup"><span data-stu-id="f73a3-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="f73a3-176">Нажмите кнопку hello **атрибуты** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f73a3-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="f73a3-177">На hello **атрибуты** выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="f73a3-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="f73a3-178">![Атрибуты](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="f73a3-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="f73a3-179">Нажмите кнопку **добавить атрибут**, а затем добавьте следующие атрибуты на основе утверждений hello:</span><span class="sxs-lookup"><span data-stu-id="f73a3-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="f73a3-180">Атрибут утверждения</span><span class="sxs-lookup"><span data-stu-id="f73a3-180">Assertion Attribute</span></span> | <span data-ttu-id="f73a3-181">Атрибут субъекта</span><span class="sxs-lookup"><span data-stu-id="f73a3-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="f73a3-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="f73a3-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="f73a3-183">firstname</span><span class="sxs-lookup"><span data-stu-id="f73a3-183">firstname</span></span> |
    | <span data-ttu-id="f73a3-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="f73a3-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="f73a3-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="f73a3-185">lastname</span></span> |
    | <span data-ttu-id="f73a3-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="f73a3-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="f73a3-187">email</span><span class="sxs-lookup"><span data-stu-id="f73a3-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="f73a3-188">Конфигурация Hello hello атрибутов зависит от того, как приложения hello в HCP разрабатываются, т. е. какие атрибуты предполагается использовать в hello ответ SAML и какое имя (атрибут субъекта) их доступа к этому атрибуту в коде hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="f73a3-189">Hello **атрибут по умолчанию** в hello экрана — только для примера.</span><span class="sxs-lookup"><span data-stu-id="f73a3-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="f73a3-190">Это не требуется toomake hello сценарии работы.</span><span class="sxs-lookup"><span data-stu-id="f73a3-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="f73a3-191">Здравствуйте, имена и значения для **атрибут субъекта** показано hello экрана зависят от способа разработки приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="f73a3-192">Возможно, приложению требуются другие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="f73a3-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="f73a3-193">В классический портал Azure, на hello hello **настроить единый вход в облачную платформу SAP HANA** странице диалогового окна, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="f73a3-194">![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="f73a3-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="f73a3-195">Группы на основе утверждений</span><span class="sxs-lookup"><span data-stu-id="f73a3-195">Assertion-based groups</span></span>
<span data-ttu-id="f73a3-196">При необходимости для поставщика удостоверений Azure Active Directory можно настроить группы на основе утверждений.</span><span class="sxs-lookup"><span data-stu-id="f73a3-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="f73a3-197">С помощью групп на облачной платформы SAP HANA позволяет назначить toodynamically один или несколько tooone пользователей или несколько ролей в приложениях облачной платформы SAP HANA, определяются значения атрибутов в hello SAML 2.0 утверждение.</span><span class="sxs-lookup"><span data-stu-id="f73a3-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="f73a3-198">Например, если hello утверждение, содержащее атрибут hello»*контракта = temporary*«, вы можете все затронутые пользователи toobe toohello добавлена группа»*ВРЕМЕННЫЕ*».</span><span class="sxs-lookup"><span data-stu-id="f73a3-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="f73a3-199">Группа Hello»*ВРЕМЕННЫЕ*» может содержать одну или несколько ролей из одного или нескольких приложений, развернутых в вашей учетной записи облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="f73a3-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="f73a3-200">Используйте группы на основе утверждений, при необходимости назначьте toosimultaneously tooone много пользователей или несколько ролей приложений в вашей учетной записи облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="f73a3-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="f73a3-201">Следует tooassign только одного или небольшое число пользователей toospecific ролей рекомендуется назначить их непосредственно в hello»**авторизаций**» вкладки панелей облачной платформы SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="f73a3-202">Назначить пользователя роли tooa</span><span class="sxs-lookup"><span data-stu-id="f73a3-202">Assign a role tooa user</span></span>
<span data-ttu-id="f73a3-203">В порядке tooenable toolog пользователей Azure AD в облачную платформу SAP HANA необходимо назначить роли в облачной платформы SAP HANA toothem hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="f73a3-204">**tooassign tooa роли пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f73a3-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="f73a3-205">Войдите в tooyour **облачной платформы SAP HANA** панель.</span><span class="sxs-lookup"><span data-stu-id="f73a3-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="f73a3-206">Выполните следующие hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-206">Perform hello following:</span></span>
   
   <span data-ttu-id="f73a3-207">![Авторизации](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Авторизации")</span><span class="sxs-lookup"><span data-stu-id="f73a3-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="f73a3-208">Щелкните **Авторизация**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="f73a3-209">Нажмите кнопку hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f73a3-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="f73a3-210">В hello **пользователя** в текстовое поле адрес электронной почты пользователя типа hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="f73a3-211">Нажмите кнопку **назначить** tooa tooassign hello обязанности.</span><span class="sxs-lookup"><span data-stu-id="f73a3-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="f73a3-212">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="f73a3-213">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="f73a3-213">Assign users</span></span>
<span data-ttu-id="f73a3-214">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="f73a3-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="f73a3-215">**Пользователи tooassign tooSAP HANA Cloud Platform выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="f73a3-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="f73a3-216">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f73a3-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="f73a3-217">На hello **облачной платформы SAP HANA** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f73a3-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="f73a3-218">![Назначение пользователей](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="f73a3-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="f73a3-219">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="f73a3-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="f73a3-220">![Да](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="f73a3-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f73a3-221">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f73a3-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="f73a3-222">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f73a3-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

