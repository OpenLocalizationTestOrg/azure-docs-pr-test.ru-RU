---
title: "Руководство по интеграции Azure Active Directory с облачной платформой SAP HANA | Документация Майкрософт"
description: "Узнайте, как использовать SAP HANA Cloud Platform вместе с Azure Active Directory для реализации единого входа, автоматической подготовки пользователей и выполнения других задач."
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
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="dc56d-103">Учебник. Интеграция Azure Active Directory с облачной платформой SAP HANA</span><span class="sxs-lookup"><span data-stu-id="dc56d-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="dc56d-104">Цель данного учебника — показать интеграцию Azure и облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc56d-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="dc56d-105">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="dc56d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="dc56d-106">действующая подписка Azure;</span><span class="sxs-lookup"><span data-stu-id="dc56d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="dc56d-107">Учетная запись облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc56d-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="dc56d-108">По завершении работы с этим руководством пользователи Azure AD, назначенные на SAP HANA Cloud Platform, смогут выполнять единый вход в приложение следуя указаниям в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc56d-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="dc56d-109">Для тестирования единого входа необходимо развернуть собственное приложение или оформить подписку на приложение в учетной записи облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc56d-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="dc56d-110">В этом учебнике используется развертывание приложения в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="dc56d-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="dc56d-111">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="dc56d-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="dc56d-112">Включение интеграции приложений для облачной платформы SAP HANA</span><span class="sxs-lookup"><span data-stu-id="dc56d-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="dc56d-113">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="dc56d-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="dc56d-114">Назначение роли пользователю</span><span class="sxs-lookup"><span data-stu-id="dc56d-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="dc56d-115">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="dc56d-115">Assigning users</span></span>

<span data-ttu-id="dc56d-116">![Сценарий](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="dc56d-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="dc56d-117">Включение интеграции приложений для облачной платформы SAP HANA</span><span class="sxs-lookup"><span data-stu-id="dc56d-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="dc56d-118">В этом разделе показано, как включить интеграцию приложений для облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc56d-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="dc56d-119">**Чтобы включить интеграцию приложений для облачной платформы SAP HANA, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="dc56d-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="dc56d-120">На портале управления Azure в левой области навигации нажмите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="dc56d-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="dc56d-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="dc56d-122">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="dc56d-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="dc56d-123">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="dc56d-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="dc56d-124">![Приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="dc56d-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="dc56d-125">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="dc56d-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="dc56d-126">![Добавление приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="dc56d-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="dc56d-127">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="dc56d-128">![Добавление приложения из коллекции](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="dc56d-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="dc56d-129">В **поле поиска** введите **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="dc56d-130">![Коллекция приложений](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="dc56d-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="dc56d-131">В области результатов выберите **SAP HANA Cloud Platform** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="dc56d-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="dc56d-132">![SAP HANA](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP HANA")</span><span class="sxs-lookup"><span data-stu-id="dc56d-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="dc56d-133">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="dc56d-133">Configure single sign-on</span></span>

<span data-ttu-id="dc56d-134">В этом разделе показано, как разрешить пользователям проходить аутентификацию в облачной платформе SAP HANA со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="dc56d-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="dc56d-135">В рамках этой процедуры потребуется отправить сертификат в кодировке Base-64 в клиент облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc56d-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="dc56d-136">Если вы не знакомы с этой процедурой, посмотрите видео [Преобразование двоичного сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="dc56d-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="dc56d-137">**Чтобы настроить единый вход, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dc56d-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="dc56d-138">На классическом портале Azure на странице интеграции с приложением **SAP HANA Cloud Platform** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Configure Single Sign On** (Настройка единого входа).</span><span class="sxs-lookup"><span data-stu-id="dc56d-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="dc56d-139">![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="dc56d-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="dc56d-140">На странице **Как пользователи должны входить на SAP HANA Cloud Platform?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="dc56d-141">![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="dc56d-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="dc56d-142">В другом окне веб-браузера войдите в панель SAP HANA Cloud Platform по адресу https://account.\<узел_среды\>.ondemand.com/cockpit (например, *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="dc56d-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="dc56d-143">Щелкните вкладку **Доверие** .</span><span class="sxs-lookup"><span data-stu-id="dc56d-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="dc56d-144">![Доверие](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Доверие")</span><span class="sxs-lookup"><span data-stu-id="dc56d-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="dc56d-145">В разделе управления доверием выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dc56d-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="dc56d-146">![Получение метаданных](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Получение метаданных")</span><span class="sxs-lookup"><span data-stu-id="dc56d-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="dc56d-147">Щелкните вкладку **Поставщик локальных служб** .</span><span class="sxs-lookup"><span data-stu-id="dc56d-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="dc56d-148">Чтобы скачать файл метаданных SAP HANA Cloud Platform, щелкните **Получить метаданные**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="dc56d-149">На странице **Настроить URL-адрес приложения** классического портала Azure выполните приведенные ниже действия, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="dc56d-150">![Настройка URL-адреса приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="dc56d-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="dc56d-151">В текстовом поле **URL-адрес единого входа** введите URL-адрес, который пользователи используют для входа в приложение **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="dc56d-152">Это URL-адрес защищенного ресурса для конкретной учетной записи в приложении облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc56d-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="dc56d-153">URL-адрес составлен по следующей схеме: *https://\<имя_приложения\>\<имя_учетной_записи\>.\<узел_среды\>.ondemand.com/\<путь\_к\_защищенному\_ресурсу\>* (например: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*).</span><span class="sxs-lookup"><span data-stu-id="dc56d-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="dc56d-154">Это URL-адрес в приложении облачной платформы SAP HANA, запрашивающий аутентификацию пользователя.</span><span class="sxs-lookup"><span data-stu-id="dc56d-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="dc56d-155">Откройте скачанный файл метаданных облачной платформы SAP HANA, а затем найдите тег **ns3:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="dc56d-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="dc56d-156">Скопируйте значение атрибута **Location** и вставьте его в текстовое поле **URL-адрес ответа SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="dc56d-157">На странице **Настройка единого входа в SAP HANA Cloud Platform** щелкните **Скачать метаданные**, чтобы скачать метаданные, а затем сохраните файл метаданных на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc56d-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="dc56d-158">![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="dc56d-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="dc56d-159">В разделе **Поставщик локальных служб** пульта управления SAP HANA Cloud Platform сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="dc56d-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dc56d-160">![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Управление доверием")</span><span class="sxs-lookup"><span data-stu-id="dc56d-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="dc56d-161">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="dc56d-162">Для параметра **Configuration Type** (Тип конфигурации) выберите значение **Custom** (Настраиваемая).</span><span class="sxs-lookup"><span data-stu-id="dc56d-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="dc56d-163">В поле **Имя поставщика локальных служб**оставьте значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dc56d-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="dc56d-164">Чтобы создать пару ключей **Signing Key** (Ключ подписывания) и **Signing Certificate** (Сертификат подписывания), щелкните **Generate Key Pair** (Создать пару ключей).</span><span class="sxs-lookup"><span data-stu-id="dc56d-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="dc56d-165">Для параметра **Principal Propagation** (Распространение субъектов) выберите значение **Disabled** (Отключено).</span><span class="sxs-lookup"><span data-stu-id="dc56d-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="dc56d-166">Для параметра **Force Authentication** (Принудительная аутентификация) выберите значение **Disabled** (Отключено).</span><span class="sxs-lookup"><span data-stu-id="dc56d-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="dc56d-167">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-167">Click **Save**.</span></span>

9. <span data-ttu-id="dc56d-168">Откройте вкладку **Trusted Identity Provider** (Доверенный поставщик удостоверений) и щелкните **Add Trusted Identity Provider** (Добавить доверенный поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="dc56d-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="dc56d-169">![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Управление доверием")</span><span class="sxs-lookup"><span data-stu-id="dc56d-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="dc56d-170">Для управления списком доверенных поставщиков удостоверений необходимо выбрать тип конфигурации «Настраиваемая» в разделе «Поставщик локальных служб».</span><span class="sxs-lookup"><span data-stu-id="dc56d-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="dc56d-171">В качестве типа конфигурации по умолчанию используется неизменяемое неявное доверие к службе SAP ID Service.</span><span class="sxs-lookup"><span data-stu-id="dc56d-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="dc56d-172">Для значения «Нет» параметры доверия отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="dc56d-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="dc56d-173">Откройте вкладку **General** (Общие) и нажмите кнопку **Browse** (Обзор), чтобы передать скачанный файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="dc56d-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="dc56d-174">![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Управление доверием")</span><span class="sxs-lookup"><span data-stu-id="dc56d-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="dc56d-175">После передачи файла метаданных поля **Single Sign-on URL** (URL-адрес единого входа), **Single Logout URL** (URL-адрес единого выхода) и **Signing Certificate** (Сертификат для подписи) заполняются автоматически.</span><span class="sxs-lookup"><span data-stu-id="dc56d-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="dc56d-176">Перейдите на вкладку **Атрибуты** .</span><span class="sxs-lookup"><span data-stu-id="dc56d-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="dc56d-177">На вкладке **Атрибуты** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="dc56d-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="dc56d-178">![Атрибуты](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="dc56d-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="dc56d-179">Щелкните **Add Assertion-Based Attribute** (Добавить атрибут на основе утверждений) и добавьте следующие атрибуты на основе утверждений:</span><span class="sxs-lookup"><span data-stu-id="dc56d-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="dc56d-180">Атрибут утверждения</span><span class="sxs-lookup"><span data-stu-id="dc56d-180">Assertion Attribute</span></span> | <span data-ttu-id="dc56d-181">Атрибут субъекта</span><span class="sxs-lookup"><span data-stu-id="dc56d-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="dc56d-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="dc56d-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="dc56d-183">firstname</span><span class="sxs-lookup"><span data-stu-id="dc56d-183">firstname</span></span> |
    | <span data-ttu-id="dc56d-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="dc56d-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="dc56d-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="dc56d-185">lastname</span></span> |
    | <span data-ttu-id="dc56d-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="dc56d-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="dc56d-187">email</span><span class="sxs-lookup"><span data-stu-id="dc56d-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="dc56d-188">Конфигурация атрибутов зависит от способа разработки приложений в HCP, т. е. какие атрибуты предполагается использовать в ответе SAML и какое имя (атрибут субъекта) используется для доступа к этому атрибуту в коде.</span><span class="sxs-lookup"><span data-stu-id="dc56d-188">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="dc56d-189">**Атрибут по умолчанию** на снимке экрана предоставляется только для примера.</span><span class="sxs-lookup"><span data-stu-id="dc56d-189">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="dc56d-190">Он не требуется для того, чтобы сценарий работал.</span><span class="sxs-lookup"><span data-stu-id="dc56d-190">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="dc56d-191">Имена и значения для **атрибута субъекта** , показанные на снимке экрана, зависят от способа разработки приложения.</span><span class="sxs-lookup"><span data-stu-id="dc56d-191">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="dc56d-192">Возможно, приложению требуются другие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="dc56d-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="dc56d-193">На классическом портале Azure в диалоговом окне **Настройка единого входа в SAP HANA Cloud Platform** выберите подтверждение настройки единого входа и нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-193">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="dc56d-194">![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="dc56d-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="dc56d-195">Группы на основе утверждений</span><span class="sxs-lookup"><span data-stu-id="dc56d-195">Assertion-based groups</span></span>
<span data-ttu-id="dc56d-196">При необходимости для поставщика удостоверений Azure Active Directory можно настроить группы на основе утверждений.</span><span class="sxs-lookup"><span data-stu-id="dc56d-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="dc56d-197">Использование групп на облачной платформе SAP HANA позволяет динамически назначать одного или нескольких пользователей одной или нескольким ролям в приложениях облачной платформы SAP HANA, которые определяются по значениям атрибутов в утверждении SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="dc56d-197">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="dc56d-198">Например, если утверждение содержит атрибут *contract=temporary*, возможно, вам потребуется добавить всех затронутых пользователей в группу *TEMPORARY*.</span><span class="sxs-lookup"><span data-stu-id="dc56d-198">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="dc56d-199">Группа*TEMPORARY*может содержать одну или несколько ролей из одного или нескольких приложений, развернутых в учетной записи SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="dc56d-199">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="dc56d-200">Используйте группы на основе утверждений, чтобы одновременно назначить большое число пользователей для одной или нескольких ролей приложений в учетной записи облачной платформы SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc56d-200">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="dc56d-201">Если требуется назначить одного или небольшое число пользователей конкретным ролям, мы рекомендуем назначить их непосредственно на вкладке **Authorizations** (Разрешения) панели SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="dc56d-201">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="dc56d-202">Назначение роли пользователю</span><span class="sxs-lookup"><span data-stu-id="dc56d-202">Assign a role to a user</span></span>
<span data-ttu-id="dc56d-203">Чтобы разрешить пользователям Azure AD входить в облачную платформу SAP HANA, им необходимо назначить роли в облачной платформе SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc56d-203">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="dc56d-204">**Чтобы назначить роль пользователю, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="dc56d-204">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="dc56d-205">Войдите в пульт управления **SAP HANA Cloud Platform** .</span><span class="sxs-lookup"><span data-stu-id="dc56d-205">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="dc56d-206">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc56d-206">Perform the following:</span></span>
   
   <span data-ttu-id="dc56d-207">![Авторизации](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Авторизации")</span><span class="sxs-lookup"><span data-stu-id="dc56d-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="dc56d-208">Щелкните **Авторизация**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="dc56d-209">Откройте вкладку **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="dc56d-209">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="dc56d-210">В тестовом поле **Пользователь** введите электронный адрес пользователя.</span><span class="sxs-lookup"><span data-stu-id="dc56d-210">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="dc56d-211">Щелкните **Назначить** , чтобы назначить роль пользователю.</span><span class="sxs-lookup"><span data-stu-id="dc56d-211">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="dc56d-212">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="dc56d-213">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="dc56d-213">Assign users</span></span>
<span data-ttu-id="dc56d-214">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="dc56d-214">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="dc56d-215">**Чтобы назначить пользователей облачной платформы SAP HANA, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="dc56d-215">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="dc56d-216">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="dc56d-216">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="dc56d-217">На странице интеграции с приложением **SAP HANA Cloud Platform** щелкните **Назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="dc56d-217">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="dc56d-218">![Назначение пользователей](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="dc56d-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="dc56d-219">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="dc56d-219">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="dc56d-220">![Да](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="dc56d-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="dc56d-221">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="dc56d-221">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="dc56d-222">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc56d-222">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

