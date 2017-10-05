---
title: "Руководство по интеграции Azure Active Directory с TOPdesk — Secure | Документация Майкрософт"
description: "Узнайте, как использовать TOPdesk — Secure с Azure Active Directory для реализации единого входа, автоматической подготовки к работе и многого другого."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="c8743-103">Учебник. Интеграция Azure Active Directory с TOPdesk — Secure</span><span class="sxs-lookup"><span data-stu-id="c8743-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="c8743-104">Цель данного учебника — показать интеграцию Azure и TOPdesk — Secure.</span><span class="sxs-lookup"><span data-stu-id="c8743-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="c8743-105">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="c8743-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c8743-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="c8743-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c8743-107">Подписка TOPdesk — Secure с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c8743-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="c8743-108">По завершении работы с этим руководством пользователи Azure AD, назначенные в TOPdesk — Secure, смогут выполнять единый вход в приложение на веб-сайте TOPdesk — Secure вашей компании (вход, инициированный поставщиком услуг) или следуя указаниям в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8743-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c8743-109">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="c8743-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="c8743-110">Включение интеграции приложений для TOPdesk — Secure</span><span class="sxs-lookup"><span data-stu-id="c8743-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="c8743-111">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="c8743-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="c8743-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="c8743-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="c8743-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="c8743-113">Assigning users</span></span>

<span data-ttu-id="c8743-114">![Сценарий](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="c8743-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="c8743-115">Включение интеграции приложений для TOPdesk — Secure</span><span class="sxs-lookup"><span data-stu-id="c8743-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="c8743-116">В этом разделе показано, как включить интеграцию приложений для TOPdesk — Secure.</span><span class="sxs-lookup"><span data-stu-id="c8743-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="c8743-117">Чтобы включить интеграцию приложений для TOPdesk — Secure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c8743-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="c8743-118">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8743-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="c8743-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c8743-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="c8743-120">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="c8743-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c8743-121">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="c8743-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="c8743-122">![Приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="c8743-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="c8743-123">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="c8743-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="c8743-124">![Добавление приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="c8743-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="c8743-125">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="c8743-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="c8743-126">![Добавление приложения из коллекции](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="c8743-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="c8743-127">В **поле поиска** введите **TOPdesk — Secure**.</span><span class="sxs-lookup"><span data-stu-id="c8743-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="c8743-128">![Коллекция приложений](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="c8743-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="c8743-129">В области результатов выберите **TOPdesk — Secure** и щелкните **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="c8743-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="c8743-130">![TOPdesk — Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk — Secure")</span><span class="sxs-lookup"><span data-stu-id="c8743-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="c8743-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="c8743-131">Configuring single sign-on</span></span>
<span data-ttu-id="c8743-132">В этом разделе показано, как разрешить пользователям проходить проверку подлинности в TOPdesk — Secure с помощью своей учетной записи Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="c8743-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="c8743-133">Для настройки единого входа для TOPdesk — Secure вам необходимо отправить файл значка с логотипом.</span><span class="sxs-lookup"><span data-stu-id="c8743-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="c8743-134">Для получения файла значка обратитесь в службу поддержки TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="c8743-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="c8743-135">Чтобы настроить единый вход, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c8743-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="c8743-136">Выполните вход на веб-сайт **TOPdesk — Secure** своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c8743-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="c8743-137">В меню **TOPdesk** выберите пункт **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="c8743-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="c8743-138">![Параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="c8743-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="c8743-139">Щелкните **Параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="c8743-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="c8743-140">![Параметры входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Параметры входа")</span><span class="sxs-lookup"><span data-stu-id="c8743-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="c8743-141">Разверните меню **Login Settings** (Параметры входа), а затем выберите **General** (Общие).</span><span class="sxs-lookup"><span data-stu-id="c8743-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="c8743-142">![Общие](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Общие")</span><span class="sxs-lookup"><span data-stu-id="c8743-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="c8743-143">В разделе **Secure** (Безопасность) для конфигурации **SAML login** (Вход SAML) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="c8743-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="c8743-144">![Технические параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Технические параметры")</span><span class="sxs-lookup"><span data-stu-id="c8743-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="c8743-145">а.</span><span class="sxs-lookup"><span data-stu-id="c8743-145">a.</span></span> <span data-ttu-id="c8743-146">Нажмите кнопку **Скачать** , чтобы скачать общедоступный файл метаданных, а затем сохраните его локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c8743-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="c8743-147">b.</span><span class="sxs-lookup"><span data-stu-id="c8743-147">b.</span></span> <span data-ttu-id="c8743-148">Откройте файл метаданных и определите местоположение узла **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="c8743-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="c8743-149">![Служба обработчика утверждений](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Служба обработчика утверждений")</span><span class="sxs-lookup"><span data-stu-id="c8743-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="c8743-150">c.</span><span class="sxs-lookup"><span data-stu-id="c8743-150">c.</span></span> <span data-ttu-id="c8743-151">Скопируйте значение **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="c8743-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="c8743-152">Это значение потребуется в разделе **Настройка URL-адреса приложения** далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="c8743-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="c8743-153">В другом окне веб-браузера войдите на **классический портал Azure** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c8743-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="c8743-154">На **безопасной версии TOPdesk** странице интеграции приложения щелкните **настроить единый вход** Открытие ** Настройка единого входа ** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c8743-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="c8743-155">![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c8743-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="c8743-156">На странице **Как пользователи будут входить в TOPdesk — Secure** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c8743-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="c8743-157">![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c8743-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="c8743-158">На странице **Настройка URL-адреса приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c8743-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="c8743-159">![Настройка URL-адреса приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="c8743-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="c8743-160">а.</span><span class="sxs-lookup"><span data-stu-id="c8743-160">a.</span></span> <span data-ttu-id="c8743-161">В текстовом поле **URL-адрес для входа в TOPdesk — Secure** введите URL-адрес, используемый пользователями для входа в ваше приложение TOPdesk — Secure (например, *https://qssolutions.topdesk.net*).</span><span class="sxs-lookup"><span data-stu-id="c8743-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="c8743-162">b.</span><span class="sxs-lookup"><span data-stu-id="c8743-162">b.</span></span> <span data-ttu-id="c8743-163">В текстовое поле **URL-адрес ответа TOPdesk — Secure** вставьте значение **TOPdesk - Secure AssertionConsumerService URL** (URL-адрес AssertionConsumerService для TOPdesk — Secure) (например, *https://qssolutions.topdesk.net/tas/public/login/saml*).</span><span class="sxs-lookup"><span data-stu-id="c8743-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="c8743-164">c.</span><span class="sxs-lookup"><span data-stu-id="c8743-164">c.</span></span> <span data-ttu-id="c8743-165">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c8743-165">Click **Next**.</span></span>

10. <span data-ttu-id="c8743-166">На странице **Настройка единого входа в TOPdesk — Secure** щелкните **Скачать метаданные**, чтобы скачать метаданные, а затем сохраните файл данных локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c8743-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="c8743-167">![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c8743-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="c8743-168">Чтобы создать файл сертификата, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c8743-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="c8743-169">![Сертификат](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Сертификат")</span><span class="sxs-lookup"><span data-stu-id="c8743-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="c8743-170">а.</span><span class="sxs-lookup"><span data-stu-id="c8743-170">a.</span></span> <span data-ttu-id="c8743-171">Откройте скачанный файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="c8743-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="c8743-172">b.</span><span class="sxs-lookup"><span data-stu-id="c8743-172">b.</span></span> <span data-ttu-id="c8743-173">Разверните узел **RoleDescriptor**, содержащий **xsi:type** со значением **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="c8743-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="c8743-174">c.</span><span class="sxs-lookup"><span data-stu-id="c8743-174">c.</span></span> <span data-ttu-id="c8743-175">Скопируйте значение узла **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="c8743-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="c8743-176">d.</span><span class="sxs-lookup"><span data-stu-id="c8743-176">d.</span></span> <span data-ttu-id="c8743-177">Сохраните скопированное значение узла **X509Certificate** локально в файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c8743-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="c8743-178">На веб-сайте TOPdesk — Secure своей компании в меню **TOPdesk** выберите **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="c8743-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="c8743-179">![Параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="c8743-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="c8743-180">Щелкните **Параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="c8743-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="c8743-181">![Параметры входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Параметры входа")</span><span class="sxs-lookup"><span data-stu-id="c8743-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="c8743-182">Разверните меню **Login Settings** (Параметры входа), а затем выберите **General** (Общие).</span><span class="sxs-lookup"><span data-stu-id="c8743-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="c8743-183">![Общие](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Общие")</span><span class="sxs-lookup"><span data-stu-id="c8743-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="c8743-184">В разделе **Public** (Общедоступные) щелкните **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="c8743-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="c8743-185">![Добавление](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="c8743-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="c8743-186">На странице диалогового окна **Помощник настройки SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c8743-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="c8743-187">![Помощник по настройке SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Помощник по настройке SAML")</span><span class="sxs-lookup"><span data-stu-id="c8743-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="c8743-188">а.</span><span class="sxs-lookup"><span data-stu-id="c8743-188">a.</span></span> <span data-ttu-id="c8743-189">Чтобы отправить скачанный файл метаданных, напротив пункта **Federation Metadata** (Метаданные федерации) нажмите кнопку **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="c8743-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="c8743-190">b.</span><span class="sxs-lookup"><span data-stu-id="c8743-190">b.</span></span> <span data-ttu-id="c8743-191">Чтобы отправить файл сертификата, напротив пункта **Certificate (RSA)** (Сертификат (RSA)) нажмите кнопку **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="c8743-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="c8743-192">c.</span><span class="sxs-lookup"><span data-stu-id="c8743-192">c.</span></span> <span data-ttu-id="c8743-193">Чтобы отправить файл с логотипом, полученный от службы поддержки TOPdesk, напротив пункта **Logo icon** (Значок логотипа) нажмите кнопку **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="c8743-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="c8743-194">d.</span><span class="sxs-lookup"><span data-stu-id="c8743-194">d.</span></span> <span data-ttu-id="c8743-195">В текстовом поле **User name attribute** (Атрибут имени пользователя) введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="c8743-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="c8743-196">д.</span><span class="sxs-lookup"><span data-stu-id="c8743-196">e.</span></span> <span data-ttu-id="c8743-197">В текстовом поле **Отображаемое имя** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c8743-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="c8743-198">Е.</span><span class="sxs-lookup"><span data-stu-id="c8743-198">f.</span></span> <span data-ttu-id="c8743-199">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c8743-199">Click **Save**.</span></span>

17. <span data-ttu-id="c8743-200">На классическом портале Azure выберите подтверждение конфигурации единого входа, а затем нажмите кнопку **Завершить**, чтобы закрыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c8743-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="c8743-201">![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c8743-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="c8743-202">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="c8743-202">Configuring user provisioning</span></span>
<span data-ttu-id="c8743-203">Чтобы пользователи Azure AD могли выполнять вход в систему TOPdesk — Secure, они должны быть подготовлены для нее.</span><span class="sxs-lookup"><span data-stu-id="c8743-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="c8743-204">В случае TOPdesk — Secure подготовка пользователей осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="c8743-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="c8743-205">Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c8743-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="c8743-206">Выполните вход на веб-сайт **TOPdesk — Secure** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c8743-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="c8743-207">В меню в верхней части страницы щелкните **TOPdesk \> New (Создать) \> Support Files (Файлы поддержки) \> Operator (Оператор)**.</span><span class="sxs-lookup"><span data-stu-id="c8743-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="c8743-208">![Оператор](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Оператор")</span><span class="sxs-lookup"><span data-stu-id="c8743-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="c8743-209">В диалоговом окне **Новый оператор** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c8743-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c8743-210">![Новый оператор](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Новый оператор")</span><span class="sxs-lookup"><span data-stu-id="c8743-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="c8743-211">а.</span><span class="sxs-lookup"><span data-stu-id="c8743-211">a.</span></span> <span data-ttu-id="c8743-212">Перейдите на вкладку "Общее".</span><span class="sxs-lookup"><span data-stu-id="c8743-212">Click the General tab.</span></span>
   
    <span data-ttu-id="c8743-213">b.</span><span class="sxs-lookup"><span data-stu-id="c8743-213">b.</span></span> <span data-ttu-id="c8743-214">В текстовом поле **Surname** (Фамилия) в разделе **General** (Общее) введите фамилию пользователя действующей учетной записи Azure Active Directory, которую нужно подготовить.</span><span class="sxs-lookup"><span data-stu-id="c8743-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="c8743-215">c.</span><span class="sxs-lookup"><span data-stu-id="c8743-215">c.</span></span> <span data-ttu-id="c8743-216">Выберите для этой учетной записи **Site** (Веб-сайт) в разделе **Location** (Расположение).</span><span class="sxs-lookup"><span data-stu-id="c8743-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="c8743-217">d.</span><span class="sxs-lookup"><span data-stu-id="c8743-217">d.</span></span> <span data-ttu-id="c8743-218">В текстовом поле **Login Name** (Имя для входа в систему) в разделе **TOPdesk Login** (Вход в TOPdesk) введите имя для входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="c8743-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="c8743-219">д.</span><span class="sxs-lookup"><span data-stu-id="c8743-219">e.</span></span> <span data-ttu-id="c8743-220">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c8743-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="c8743-221">Вы можете использовать любые другие инструменты создания учетных записей пользователей TOPdesk — Secure или API-интерфейсы, предоставляемые TOPdesk — Secure для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="c8743-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="c8743-222">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="c8743-222">Assigning users</span></span>
<span data-ttu-id="c8743-223">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="c8743-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="c8743-224">Чтобы назначить пользователей TOPdesk — Secure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c8743-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="c8743-225">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="c8743-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c8743-226">На ** безопасной версии TOPdesk ** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c8743-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="c8743-227">![Назначение пользователей](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="c8743-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="c8743-228">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="c8743-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="c8743-229">![Да](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="c8743-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c8743-230">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="c8743-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c8743-231">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8743-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

