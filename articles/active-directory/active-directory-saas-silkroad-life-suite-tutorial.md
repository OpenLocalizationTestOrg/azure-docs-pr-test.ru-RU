---
title: "Руководство по интеграции Azure Active Directory с решением SilkRoad Life Suite | Документация Майкрософт"
description: "Узнайте, как настроить единый вход для Azure Active Directory и SilkRoad Life Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="4b81f-103">Руководство по интеграции Azure Active Directory с решением SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="4b81f-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="4b81f-104">Цель этого руководства — показать, как интегрировать Azure Active Directory (Azure AD) с приложением SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="4b81f-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="4b81f-105">Интеграция SilkRoad Life Suite с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4b81f-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="4b81f-106">С помощью Azure AD вы можете контролировать доступ к SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="4b81f-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="4b81f-107">Вы можете включить автоматический вход пользователей в SilkRoad Life Suite (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b81f-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="4b81f-108">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b81f-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b81f-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4b81f-109">Prerequisites</span></span>
<span data-ttu-id="4b81f-110">Чтобы настроить интеграцию Azure AD с SilkRoad Life Suite, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="4b81f-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="4b81f-111">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4b81f-111">An Azure AD subscription</span></span>
* <span data-ttu-id="4b81f-112">подписка SilkRoad Life Suite с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4b81f-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="4b81f-113">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="4b81f-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="4b81f-114">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="4b81f-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4b81f-115">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="4b81f-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4b81f-116">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b81f-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="4b81f-117">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4b81f-117">Scenario Description</span></span>
<span data-ttu-id="4b81f-118">Цель этого руководства — научить вас проверять единый вход Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4b81f-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="4b81f-119">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="4b81f-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b81f-120">Добавление SilkRoad Life Suite из коллекции.</span><span class="sxs-lookup"><span data-stu-id="4b81f-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="4b81f-121">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b81f-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="4b81f-122">Добавление SilkRoad Life Suite из коллекции</span><span class="sxs-lookup"><span data-stu-id="4b81f-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="4b81f-123">Чтобы настроить интеграцию SilkRoad Life Suite в Azure AD, необходимо добавить SilkRoad Life Suite из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4b81f-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b81f-124">**Чтобы добавить SilkRoad Life Suite из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4b81f-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b81f-125">На **классическом портале Azure**в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="4b81f-127">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="4b81f-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="4b81f-128">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="4b81f-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Приложения][2]

4. <span data-ttu-id="4b81f-130">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="4b81f-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Приложения][3]

5. <span data-ttu-id="4b81f-132">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Приложения][4]

6. <span data-ttu-id="4b81f-134">В поле поиска введите **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Приложения][5]

7. <span data-ttu-id="4b81f-136">В области результатов выберите **SilkRoad Life Suite** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="4b81f-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Приложения][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4b81f-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b81f-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4b81f-139">Цель этого раздела — показать, как настроить и проверить единый вход Azure AD в SilkRoad Life Suite с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b81f-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b81f-140">Для работы единого входа в Azure AD необходимо знать, какой пользователь в SilkRoad Life Suite соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b81f-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="4b81f-141">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="4b81f-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="4b81f-142">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="4b81f-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="4b81f-143">Чтобы настроить и проверить единый вход Azure AD в SilkRoad Life Suite, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="4b81f-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b81f-144">**[Настройка единого входа Azure AD](#configuring-azure-ad-single-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="4b81f-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b81f-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b81f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b81f-146">**[Создание тестового пользователя SilkRoad Life Suite](#creating-a-silkroad-life-suite-test-user)** требуется для создания пользователя Britta Simon в SilkRoad Life Suite, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b81f-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4b81f-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b81f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b81f-148">**[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4b81f-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4b81f-149">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b81f-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="4b81f-150">Цель этого раздела — включить единый вход Azure AD на классическом портале Azure и настроить его в приложении SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="4b81f-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="4b81f-151">**Чтобы настроить единый вход в Azure AD в SilkRoad Life Suite, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4b81f-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="4b81f-152">Войдите на сайт компании SilkRoad от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="4b81f-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="4b81f-153">Чтобы получить доступ к приложению SilkRoad Life Suite Authentication для настройки федерации с Microsoft Azure AD, обратитесь в службу поддержки компании SilkRoad или к представителю отдела обслуживания клиентов компании SilkRoad.</span><span class="sxs-lookup"><span data-stu-id="4b81f-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="4b81f-154">В разделе **Service Provider** (Поставщик услуг) щелкните **Federation Details** (Сведения о федерации).</span><span class="sxs-lookup"><span data-stu-id="4b81f-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![единого входа Azure AD][10] 

3. <span data-ttu-id="4b81f-156">Щелкните **Download Federation Metadata**(Загрузить метаданные федерации), а затем сохраните файл метаданных на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4b81f-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![единого входа Azure AD][11] 

4. <span data-ttu-id="4b81f-158">На классическом портале Azure на странице интеграции с приложением **SilkRoad Life Suite** нажмите кнопку **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][6] 

5. <span data-ttu-id="4b81f-160">На странице **Как пользователи должны входить в SilkRoad Life Suite?** выберите **Единый вход Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![единого входа Azure AD][7] 

6. <span data-ttu-id="4b81f-162">В диалоговом окне на странице **Настройка параметров приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4b81f-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![единого входа Azure AD][8]   
 1. <span data-ttu-id="4b81f-164">В текстовом поле **URL-адрес для входа** введите URL-адрес, используемый пользователями для входа на сайт SilkRoad Life Suite (например, *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="4b81f-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="4b81f-165">Откройте скачанный файл метаданных **Silkroad** .</span><span class="sxs-lookup"><span data-stu-id="4b81f-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="4b81f-166">Найдите тег **AssertionConsumerService**, а затем скопируйте атрибут **Location**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![единого входа Azure AD][21] 
 4. <span data-ttu-id="4b81f-168">Вставьте значение в текстовое поле **URL-адрес ответа**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="4b81f-169">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-169">Click **Next**.</span></span>

6. <span data-ttu-id="4b81f-170">На странице **Настройка единого входа в SilkRoad Life Suite** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4b81f-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![единого входа Azure AD][9]  
 1. <span data-ttu-id="4b81f-172">Нажмите "Загрузить сертификат" и сохраните файл сертификата на свой компьютер.</span><span class="sxs-lookup"><span data-stu-id="4b81f-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="4b81f-173">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-173">Click **Next**.</span></span>

7. <span data-ttu-id="4b81f-174">В приложении **SilkRoad** щелкните **Authentication Sources** (Источники проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="4b81f-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![единого входа Azure AD][12] 

8. <span data-ttu-id="4b81f-176">Щелкните **Add Authentication Source**(Добавить источник аутентификации).</span><span class="sxs-lookup"><span data-stu-id="4b81f-176">Click **Add Authentication Source**.</span></span> 
   
    ![Единый вход в Azure AD][13] 

9. <span data-ttu-id="4b81f-178">В разделе **Add Authentication Source** (Добавление источника аутентификации) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4b81f-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![единого входа Azure AD][14]  
 1. <span data-ttu-id="4b81f-180">В разделе **Option 2 - Metadata File** (Вариант 2 — файл метаданных) нажмите кнопку **Browse** (Обзор), чтобы отправить скачанный файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="4b81f-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="4b81f-181">Нажмите кнопку **Создать поставщик удостоверений с помощью данных из файла**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="4b81f-182">В разделе **Authentication Sources** (Источники проверки подлинности) нажмите кнопку **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="4b81f-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![единого входа Azure AD][15] 

11. <span data-ttu-id="4b81f-184">В диалоговом окне **Edit Authentication Source** (Изменение источника аутентификации) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4b81f-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![единого входа Azure AD][16] 
 1. <span data-ttu-id="4b81f-186">В поле **Enabled** (Включено) выберите **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="4b81f-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="4b81f-187">В текстовом поле **Описание IdP** введите описание вашей конфигурации (например, *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="4b81f-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="4b81f-188">В текстовом поле **IdP Name** (Имя IdP) введите уникальное имя вашей конфигурации (например, *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="4b81f-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="4b81f-189">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-189">Click **Save**.</span></span>

12. <span data-ttu-id="4b81f-190">Отключите все остальные источники аутентификации.</span><span class="sxs-lookup"><span data-stu-id="4b81f-190">Disable all other authentication sources.</span></span> 
    
     ![единого входа Azure AD][17]

13. <span data-ttu-id="4b81f-192">На классическом портале Azure на странице **Подтверждение единого входа** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![единого входа Azure AD][18]

14. <span data-ttu-id="4b81f-194">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![единого входа Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4b81f-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b81f-196">Create an Azure AD test user</span></span>
<span data-ttu-id="4b81f-197">Цель этого раздела — создать на классическом портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b81f-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="4b81f-199">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4b81f-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b81f-200">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="4b81f-202">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="4b81f-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="4b81f-203">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b81f-205">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="4b81f-207">На странице диалогового окна **Тип учетной записи пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4b81f-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="4b81f-209">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="4b81f-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="4b81f-210">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="4b81f-211">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-211">Click **Next**.</span></span>

6. <span data-ttu-id="4b81f-212">На странице диалогового окна **Профиль пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4b81f-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="4b81f-214">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="4b81f-215">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="4b81f-216">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="4b81f-217">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="4b81f-218">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-218">Click **Next**.</span></span>

7. <span data-ttu-id="4b81f-219">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="4b81f-221">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4b81f-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="4b81f-223">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="4b81f-224">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="4b81f-225">Создание тестового пользователя SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="4b81f-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="4b81f-226">Цель этого раздела — создать в SilkRoad Life Suite пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b81f-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="4b81f-227">Пользователь Britta должен иметь идентификатор единого входа (иногда называемый *AuthParam*), который соответствует **адресу электронной почты** этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b81f-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="4b81f-228">**Чтобы создать пользователя с именем Britta Simon в SilkRoad Life Suite, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4b81f-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="4b81f-229">Попросите службу поддержки SilkRoad Life Suite создать пользователя, у которого значение атрибута **Код SSO** совпадает с **адресом электронной почты** пользователя Britta Simon в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b81f-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4b81f-230">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b81f-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="4b81f-231">Цель этого раздела — позволить пользователю Britta Simon использовать единый вход Azure, предоставив ей доступ к SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="4b81f-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4b81f-233">**Чтобы назначить Britta Simon в SilkRoad Life Suite, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4b81f-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="4b81f-234">Чтобы открыть представление приложений, на классическом портале Azure в представлении каталога щелкните **Приложения** в меню вверху.</span><span class="sxs-lookup"><span data-stu-id="4b81f-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Назначение пользователя][201] 

2. <span data-ttu-id="4b81f-236">В списке приложений выберите **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Назначение пользователя][202] 

3. <span data-ttu-id="4b81f-238">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-238">In the menu on the top, click **Users**.</span></span>
   
    ![Назначение пользователя][203] 

4. <span data-ttu-id="4b81f-240">В списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="4b81f-241">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4b81f-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="4b81f-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4b81f-243">Test single sign-on</span></span>
<span data-ttu-id="4b81f-244">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="4b81f-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="4b81f-245">Щелкнув плитку SilkRoad Life Suite на панели доступа, вы автоматически войдете в приложение SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="4b81f-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b81f-246">дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4b81f-246">Additional Resources</span></span>
* [<span data-ttu-id="4b81f-247">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b81f-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b81f-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b81f-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





