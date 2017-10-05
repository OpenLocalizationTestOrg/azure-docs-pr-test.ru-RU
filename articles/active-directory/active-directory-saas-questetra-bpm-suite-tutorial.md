---
title: "Руководство по интеграции Azure Active Directory с Questetra BPM Suite | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="7e68c-103">Учебник. Интеграция Azure Active Directory с Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="7e68c-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="7e68c-104">Цель этого учебника — показать, как интегрировать Azure Active Directory (Azure AD) с приложением Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7e68c-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="7e68c-105">Интеграция Questetra BPM Suite с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7e68c-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="7e68c-106">С помощью Azure AD вы можете контролировать доступ к Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7e68c-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="7e68c-107">Вы можете включить автоматический вход пользователей в Questetra BPM Suite (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e68c-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="7e68c-108">Вы можете управлять учетными записями централизованно — через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7e68c-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="7e68c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e68c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e68c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7e68c-110">Prerequisites</span></span>
<span data-ttu-id="7e68c-111">Чтобы настроить интеграцию Azure AD с Questetra BPM Suite, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="7e68c-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="7e68c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7e68c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7e68c-113">Подписка [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) с включенным единым входом.</span><span class="sxs-lookup"><span data-stu-id="7e68c-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e68c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7e68c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="7e68c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7e68c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7e68c-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="7e68c-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7e68c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e68c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="7e68c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7e68c-118">Scenario Description</span></span>
<span data-ttu-id="7e68c-119">Цель этого учебника — научить вас проверять единый вход в Azure AD в пробной среде.</span><span class="sxs-lookup"><span data-stu-id="7e68c-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="7e68c-120">Сценарий, описанный в этом учебнике, состоит из следующих основных блоков.</span><span class="sxs-lookup"><span data-stu-id="7e68c-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="7e68c-121">Добавление Questetra BPM Suite из коллекции</span><span class="sxs-lookup"><span data-stu-id="7e68c-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="7e68c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e68c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="7e68c-123">Добавление Questetra BPM Suite из коллекции</span><span class="sxs-lookup"><span data-stu-id="7e68c-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="7e68c-124">Чтобы настроить интеграцию Questetra BPM Suite в Azure AD, необходимо добавить Questetra BPM Suite из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7e68c-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7e68c-125">**Чтобы добавить Questetra BPM Suite из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7e68c-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7e68c-126">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="7e68c-128">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="7e68c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7e68c-129">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="7e68c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Приложения][2]

4. <span data-ttu-id="7e68c-131">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="7e68c-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Приложения][3]

5. <span data-ttu-id="7e68c-133">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Приложения][4]

6. <span data-ttu-id="7e68c-135">В поле поиска введите **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![Приложения][5]

7. <span data-ttu-id="7e68c-137">В области результатов выберите **Questetra BPM Suite** и щелкните **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="7e68c-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e68c-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e68c-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e68c-139">Цель этого раздела — показать вам, как настроить и проверить единый вход Azure AD в Questetra BPM Suite с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e68c-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7e68c-140">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Questetra BPM Suite соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e68c-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="7e68c-141">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7e68c-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="7e68c-142">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7e68c-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="7e68c-143">Чтобы настроить и проверить единый вход Azure AD в Questetra BPM Suite, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="7e68c-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7e68c-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-single-sign-on)** необходима, чтобы позволить пользователям использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7e68c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7e68c-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e68c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e68c-146">**[Создание тестового пользователя Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)** требуется для создания соответствующего пользователя Britta Simon в Questetra BPM Suite, связанного с ее представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e68c-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7e68c-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e68c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e68c-148">**[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7e68c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e68c-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e68c-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="7e68c-150">Цель этого раздела — включить единый вход Azure AD на классическом портале Azure и настроить единый вход в приложение Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7e68c-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="7e68c-151">**Чтобы настроить единый вход Azure AD в Questetra BPM Suite, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7e68c-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7e68c-152">На странице интеграции с приложением **Questetra BPM Suite** классического портала Azure нажмите кнопку **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][8]

2. <span data-ttu-id="7e68c-154">На странице **Как пользователи должны входить в Questetra BPM Suite?** выберите **Единый вход Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![единого входа Azure AD][9]

3. <span data-ttu-id="7e68c-156">В другом окне веб-браузера войдите в свой корпоративный веб-сайт **Questetra BPM Suite** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="7e68c-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="7e68c-157">В верхнем меню щелкните пункт **Системные параметры**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![единого входа Azure AD][10]

5. <span data-ttu-id="7e68c-159">Чтобы открыть страницу **SingleSignOnSAML**, щелкните **SSO (SAML)** (Единый вход (SAML)).</span><span class="sxs-lookup"><span data-stu-id="7e68c-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![единого входа Azure AD][11]

6. <span data-ttu-id="7e68c-161">На диалоговой странице **Настройка параметров приложения** классического портала Azure выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7e68c-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Настройка параметров приложения][13]
   
    <span data-ttu-id="7e68c-163">А.</span><span class="sxs-lookup"><span data-stu-id="7e68c-163">a.</span></span> <span data-ttu-id="7e68c-164">На веб-сайте компании **Questetra BPM Suite** в разделе SP Information (Сведения о SP) скопируйте значение поля **ACS URL** (URL-адрес ACS) и вставьте его в текстовом поле **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="7e68c-165">b.</span><span class="sxs-lookup"><span data-stu-id="7e68c-165">b.</span></span> <span data-ttu-id="7e68c-166">На веб-сайте компании **Questetra BPM Suite** в разделе SP Information (Сведения о SP) скопируйте значение поля **Entity ID** (Идентификатор сущности) и вставьте его в текстовом поле **Issuer URL** (URL-адрес издателя).</span><span class="sxs-lookup"><span data-stu-id="7e68c-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="7e68c-167">c.</span><span class="sxs-lookup"><span data-stu-id="7e68c-167">c.</span></span> <span data-ttu-id="7e68c-168">На веб-сайте компании **Questetra BPM Suite** в разделе SP Information (Сведения о SP) скопируйте значение поля **ACS URL** (URL-адрес ACS) и вставьте его в текстовом поле **Reply URL** (URL-адрес ответа).</span><span class="sxs-lookup"><span data-stu-id="7e68c-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="7e68c-169">d.</span><span class="sxs-lookup"><span data-stu-id="7e68c-169">d.</span></span> <span data-ttu-id="7e68c-170">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-170">Click **Next**.</span></span>

7. <span data-ttu-id="7e68c-171">На странице **Настройка единого входа в Questetra BPM Suite** нажмите кнопку **Скачать сертификат**, а затем сохраните файл сертификата локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7e68c-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Настройка единого входа][14]

8. <span data-ttu-id="7e68c-173">На веб-сайте компании **Questetra BPM Suite** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7e68c-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Настройка единого входа][15]
   
    <span data-ttu-id="7e68c-175">а.</span><span class="sxs-lookup"><span data-stu-id="7e68c-175">a.</span></span> <span data-ttu-id="7e68c-176">Выберите пункт **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="7e68c-177">b.</span><span class="sxs-lookup"><span data-stu-id="7e68c-177">b.</span></span> <span data-ttu-id="7e68c-178">На классическом портале Azure скопируйте значение поля **URL-адрес издателя** и вставьте его в текстовом поле **Идентификатор сущности**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="7e68c-179">c.</span><span class="sxs-lookup"><span data-stu-id="7e68c-179">c.</span></span> <span data-ttu-id="7e68c-180">На классическом портале Azure скопируйте значение поля **URL-адрес службы единого входа** и вставьте его в текстовом поле **URL-адрес страницы входа**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="7e68c-181">d.</span><span class="sxs-lookup"><span data-stu-id="7e68c-181">d.</span></span> <span data-ttu-id="7e68c-182">На классическом портале Azure скопируйте значение поля **URL-адрес службы единого выхода** и вставьте его в текстовом поле **URL-адрес страницы выхода**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="7e68c-183">д.</span><span class="sxs-lookup"><span data-stu-id="7e68c-183">e.</span></span> <span data-ttu-id="7e68c-184">В текстовом поле **NameID format** (Формат идентификатора имени) введите **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="7e68c-185">Е.</span><span class="sxs-lookup"><span data-stu-id="7e68c-185">f.</span></span> <span data-ttu-id="7e68c-186">Создайте файл в кодировке Base-64 из загруженного сертификата.</span><span class="sxs-lookup"><span data-stu-id="7e68c-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="7e68c-187">Дополнительные сведения можно узнать в видео [Преобразование двоичного сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="7e68c-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="7e68c-188">g.</span><span class="sxs-lookup"><span data-stu-id="7e68c-188">g.</span></span> <span data-ttu-id="7e68c-189">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат проверки** .</span><span class="sxs-lookup"><span data-stu-id="7e68c-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="7e68c-190">h.</span><span class="sxs-lookup"><span data-stu-id="7e68c-190">h.</span></span> <span data-ttu-id="7e68c-191">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-191">Click **Save**.</span></span>

1. <span data-ttu-id="7e68c-192">На классическом портале Azure выберите подтверждение конфигурации единого входа и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Что такое Azure AD Connect?][17]

2. <span data-ttu-id="7e68c-194">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Что такое Azure AD Connect?][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e68c-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e68c-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e68c-197">Цель этого раздела — создать на классическом портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e68c-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="7e68c-198">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7e68c-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7e68c-199">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD][100] 

2. <span data-ttu-id="7e68c-201">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="7e68c-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7e68c-202">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD][101] 

4. <span data-ttu-id="7e68c-204">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Создание тестового пользователя Azure AD][102] 

5. <span data-ttu-id="7e68c-206">На странице диалогового окна **Тип учетной записи пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7e68c-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][103]
   
    <span data-ttu-id="7e68c-208">а.</span><span class="sxs-lookup"><span data-stu-id="7e68c-208">a.</span></span> <span data-ttu-id="7e68c-209">В поле **Тип пользователя** выберите значение **Новый пользователь в вашей организации**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="7e68c-210">b.</span><span class="sxs-lookup"><span data-stu-id="7e68c-210">b.</span></span> <span data-ttu-id="7e68c-211">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="7e68c-212">c.</span><span class="sxs-lookup"><span data-stu-id="7e68c-212">c.</span></span> <span data-ttu-id="7e68c-213">Нажмите кнопку Далее.</span><span class="sxs-lookup"><span data-stu-id="7e68c-213">Click Next.</span></span>

6. <span data-ttu-id="7e68c-214">На странице диалогового окна **Профиль пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7e68c-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD][104] 
   
    <span data-ttu-id="7e68c-216">а.</span><span class="sxs-lookup"><span data-stu-id="7e68c-216">a.</span></span> <span data-ttu-id="7e68c-217">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="7e68c-218">b.</span><span class="sxs-lookup"><span data-stu-id="7e68c-218">b.</span></span> <span data-ttu-id="7e68c-219">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="7e68c-220">c.</span><span class="sxs-lookup"><span data-stu-id="7e68c-220">c.</span></span> <span data-ttu-id="7e68c-221">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="7e68c-222">d.</span><span class="sxs-lookup"><span data-stu-id="7e68c-222">d.</span></span> <span data-ttu-id="7e68c-223">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="7e68c-224">д.</span><span class="sxs-lookup"><span data-stu-id="7e68c-224">e.</span></span> <span data-ttu-id="7e68c-225">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-225">Click **Next**.</span></span>

7. <span data-ttu-id="7e68c-226">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD][105]  

8. <span data-ttu-id="7e68c-228">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7e68c-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][106]   
   
    <span data-ttu-id="7e68c-230">а.</span><span class="sxs-lookup"><span data-stu-id="7e68c-230">a.</span></span> <span data-ttu-id="7e68c-231">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="7e68c-232">b.</span><span class="sxs-lookup"><span data-stu-id="7e68c-232">b.</span></span> <span data-ttu-id="7e68c-233">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="7e68c-234">Создание тестового пользователя Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="7e68c-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="7e68c-235">Цель этого раздела — создать пользователя с именем Britta Simon в Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7e68c-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="7e68c-236">**Чтобы создать пользователя с именем Britta Simon в Questetra BPM Suite, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7e68c-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7e68c-237">Выполните входа на сайт компании Questetra BPM Suite в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="7e68c-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="7e68c-238">Выберите **System Settings > User List > New User** (Системные параметры > Список пользователей > Новый пользователь).</span><span class="sxs-lookup"><span data-stu-id="7e68c-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="7e68c-239">В диалоговом окне создания нового пользователя выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7e68c-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![Создание тестового пользователя][300] 
   
    <span data-ttu-id="7e68c-241">а.</span><span class="sxs-lookup"><span data-stu-id="7e68c-241">a.</span></span> <span data-ttu-id="7e68c-242">В текстовом поле **Имя** в Azure AD введите имя пользователя Britta.</span><span class="sxs-lookup"><span data-stu-id="7e68c-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="7e68c-243">b.</span><span class="sxs-lookup"><span data-stu-id="7e68c-243">b.</span></span> <span data-ttu-id="7e68c-244">В текстовом поле **Электронная почта** в Azure AD введите адрес электронной почты пользователя Britta.</span><span class="sxs-lookup"><span data-stu-id="7e68c-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="7e68c-245">c.</span><span class="sxs-lookup"><span data-stu-id="7e68c-245">c.</span></span> <span data-ttu-id="7e68c-246">В текстовом поле **Пароль** введите пароль.</span><span class="sxs-lookup"><span data-stu-id="7e68c-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="7e68c-247">Нажмите кнопку **Добавить нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7e68c-248">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e68c-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="7e68c-249">Цель этого раздела — позволить пользователю Britta Simon использовать единый вход в Azure, предоставив ей доступ к Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7e68c-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![Что такое Azure AD Connect?][200]

<span data-ttu-id="7e68c-251">**Чтобы назначить Britta Simon в Questetra BPM Suite, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7e68c-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7e68c-252">Чтобы открыть представление приложений, на классическом портале Azure в представлении каталога щелкните **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="7e68c-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Что такое Azure AD Connect?][201]
2. <span data-ttu-id="7e68c-254">В списке приложений выберите **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Что такое Azure AD Connect?][205]
3. <span data-ttu-id="7e68c-256">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-256">In the menu on the top, click **Users**.</span></span>
   
    ![Что такое Azure AD Connect?][202]
4. <span data-ttu-id="7e68c-258">В списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![Что такое Azure AD Connect?][203]
5. <span data-ttu-id="7e68c-260">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7e68c-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Что такое Azure AD Connect?][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="7e68c-262">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7e68c-262">Testing Single Sign-On</span></span>
<span data-ttu-id="7e68c-263">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7e68c-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="7e68c-264">Щелкнув элемент Questetra BPM Suite на панели доступа, вы автоматически войдете в приложение Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7e68c-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e68c-265">дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7e68c-265">Additional Resources</span></span>
* [<span data-ttu-id="7e68c-266">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e68c-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e68c-267">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e68c-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
