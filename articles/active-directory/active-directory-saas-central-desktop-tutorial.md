---
title: "Руководство. Интеграция Azure Active Directory с Central Desktop | Документация Майкрософт"
description: "Узнайте, как toouse Central Desktop с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="5e23b-103">Учебник. Интеграция Azure Active Directory с Central Desktop</span><span class="sxs-lookup"><span data-stu-id="5e23b-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="5e23b-104">Цель этого учебника Hello — tooshow hello интеграцию Azure и Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="5e23b-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="5e23b-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5e23b-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="5e23b-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="5e23b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5e23b-107">Подписка с поддержкой единого входа в Central Desktop/клиент Central Desktop</span><span class="sxs-lookup"><span data-stu-id="5e23b-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="5e23b-108">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="5e23b-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="5e23b-109">Включение интеграции приложений hello для Central Desktop</span><span class="sxs-lookup"><span data-stu-id="5e23b-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="5e23b-110">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="5e23b-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="5e23b-111">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="5e23b-111">Configuring user provisioning</span></span>
* <span data-ttu-id="5e23b-112">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="5e23b-112">Assigning users</span></span>

<span data-ttu-id="5e23b-113">![Сценарий](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="5e23b-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="5e23b-114">Включить hello интеграции приложений для Central Desktop</span><span class="sxs-lookup"><span data-stu-id="5e23b-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="5e23b-115">Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="5e23b-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="5e23b-116">**Интеграция приложения hello tooenable для Central Desktop выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="5e23b-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e23b-117">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5e23b-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5e23b-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5e23b-119">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="5e23b-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="5e23b-120">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="5e23b-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="5e23b-121">![Приложения](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="5e23b-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5e23b-122">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="5e23b-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="5e23b-123">![Добавление приложения](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="5e23b-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5e23b-124">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="5e23b-125">![Добавление приложения из коллекции](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="5e23b-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5e23b-126">В hello **поле поиска**, тип **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="5e23b-127">![Коллекция приложений](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="5e23b-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="5e23b-128">В области результатов hello выберите **Central Desktop**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5e23b-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="5e23b-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="5e23b-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5e23b-130">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="5e23b-130">Configure single sign-on</span></span>

<span data-ttu-id="5e23b-131">Цель этого раздела Hello — toooutline, каким образом пользователи tooenable tooauthenticate tooCentral рабочего стола с помощью учетной записи в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="5e23b-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="5e23b-132">В рамках этой процедуры, необходимые tooupload клиента tooyour Central Desktop сертификат в кодировке base-64.</span><span class="sxs-lookup"><span data-stu-id="5e23b-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="5e23b-133">Если вы не знакомы с этой процедурой, см. раздел [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="5e23b-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="5e23b-134">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="5e23b-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e23b-135">В классический портал Azure, на hello hello **Central Desktop** странице интеграции приложения щелкните **настроить единый вход** tooopen hello ** Настройка единого входа ** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5e23b-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="5e23b-136">![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="5e23b-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="5e23b-137">На hello **предпочитаемый как toosign пользователей на tooCentral рабочего стола** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5e23b-138">![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="5e23b-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="5e23b-139">На hello **настроить URL-адрес приложения** страницы, выполните следующие шаги hello и нажмите кнопку **Далее**:</span><span class="sxs-lookup"><span data-stu-id="5e23b-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="5e23b-140">В hello **рабочий стол входа в URL-адрес центра** в текстовое поле введите hello URL-адрес клиента Central Desktop (например: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="5e23b-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="5e23b-141">Hello URL-адрес ответа центра рабочего стола введите текстовое поле URL-адрес центра Desktop AssertionConsumerService (например: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="5e23b-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="5e23b-142">Hello значение можно получить из метаданных central desktop hello (например: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="5e23b-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="5e23b-143">![Настройка URL-адреса приложения](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="5e23b-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="5e23b-144">На hello **настроить единый вход в Central Desktop** страницы, toodownload свой сертификат, нажмите кнопку **загрузки сертификата**, а затем сохраните файл сертификата hello на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5e23b-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="5e23b-145">![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="5e23b-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="5e23b-146">Войдите в tooyour **Central Desktop** клиента.</span><span class="sxs-lookup"><span data-stu-id="5e23b-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="5e23b-147">Go слишком**параметры**, нажмите кнопку **Дополнительно**, а затем нажмите кнопку **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="5e23b-148">![Настройка — Дополнительно](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Настройка — Дополнительно")</span><span class="sxs-lookup"><span data-stu-id="5e23b-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="5e23b-149">На hello **настройки единого входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e23b-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="5e23b-150">![Параметры единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="5e23b-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="5e23b-151">Установите флажок **Разрешить единый вход SAML версии 2**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="5e23b-152">В классический портал Azure, на hello hello **настроить единый вход в Central Desktop** страницы, копировать hello **URL-адрес издателя** значение, а затем вставьте его в hello **URL-адрес SSO** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="5e23b-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="5e23b-153">В классический портал Azure, на hello hello **настроить единый вход в Central Desktop** страницы, копировать hello **URL-адрес удаленного входа** значение, а затем вставьте его в hello **URL-адрес входа SSO**текстового поля.</span><span class="sxs-lookup"><span data-stu-id="5e23b-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="5e23b-154">В классический портал Azure, на hello hello **настроить единый вход в Central Desktop** страницы, копировать hello **URL-адрес службы единого выхода** значение, а затем вставьте его в hello **URL-адрес выхода SSO** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="5e23b-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="5e23b-155">В hello **метод проверки подписи сообщения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5e23b-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="5e23b-156">![Метод проверки подписей в сообщениях](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Метод проверки подписей в сообщениях")</span><span class="sxs-lookup"><span data-stu-id="5e23b-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="5e23b-157">Выберите **Сертификат**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="5e23b-158">Из hello **сертификат SSO** выберите **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="5e23b-159">Создайте текстовый файл из сертификата загружен hello, hello копирования содержимого hello текстового файла, а затем вставьте его в hello **сертификат SSO** поля.</span><span class="sxs-lookup"><span data-stu-id="5e23b-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="5e23b-160">Дополнительные сведения см. в разделе [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="5e23b-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="5e23b-161">Выберите **отображать страницу входа tooyour SAMLv2 ссылку**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="5e23b-162">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-162">Click **Update**.</span></span>
10. <span data-ttu-id="5e23b-163">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5e23b-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="5e23b-164">![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="5e23b-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="5e23b-165">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="5e23b-165">Configure user provisioning</span></span>

<span data-ttu-id="5e23b-166">Для AAD пользователей toobe может toosign в они должны быть подготовленных toohello приложении Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="5e23b-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="5e23b-167">В этом разделе описывается, как учетные записи пользователей toocreate AAD в Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="5e23b-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="5e23b-168">**tooCentral учетных записей пользователя tooprovision рабочего стола:**</span><span class="sxs-lookup"><span data-stu-id="5e23b-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="5e23b-169">Войдите в систему tooyour клиента Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="5e23b-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="5e23b-170">Go слишком**людей \> внутренние члены**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="5e23b-171">Нажмите кнопку **Добавить внутренних участников**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="5e23b-172">![Люди](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="5e23b-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="5e23b-173">В hello **электронной почты адрес новых членов** текстовом поле введите учетную запись AAD tooprovision и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="5e23b-174">![Адреса электронной почты новых участников](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Адреса электронной почты новых участников")</span><span class="sxs-lookup"><span data-stu-id="5e23b-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="5e23b-175">Нажмите кнопку **Добавить внутренних участников**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="5e23b-176">![Добавление внутренних участников](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Добавление внутренних участников")</span><span class="sxs-lookup"><span data-stu-id="5e23b-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="5e23b-177">Hello пользователей, которые были добавлены получит сообщение электронной почты, включающий ссылку для подтверждения они необходима учетная запись hello tooactivate tooclick.</span><span class="sxs-lookup"><span data-stu-id="5e23b-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="5e23b-178">Можно использовать любые другие Central Desktop пользователя средства создания учетных записей или интерфейсы API, предоставляемые Central Desktop tooprovision учетных записей пользователей AAD</span><span class="sxs-lookup"><span data-stu-id="5e23b-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="5e23b-179">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="5e23b-179">Assign users</span></span>
<span data-ttu-id="5e23b-180">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="5e23b-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="5e23b-181">**Пользователи tooassign tooCentral рабочего стола, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="5e23b-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e23b-182">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="5e23b-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5e23b-183">На hello **Central Desktop** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5e23b-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5e23b-184">![Назначение пользователей](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="5e23b-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="5e23b-185">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="5e23b-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="5e23b-186">![Да](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="5e23b-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5e23b-187">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5e23b-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="5e23b-188">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e23b-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

