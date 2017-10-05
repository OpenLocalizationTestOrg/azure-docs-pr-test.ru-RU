---
title: "Учебник: Интеграция Azure Active Directory с @Task| Документы Microsoft"
description: "Узнайте, как настроить единый вход между Azure Active Directory и @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: ebb19ca6cbaf04106fbce937d95651e709854cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="e3eb4-103">Учебник. Интеграция Azure Active Directory с @Task</span><span class="sxs-lookup"><span data-stu-id="e3eb4-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="e3eb4-104">Цель этого учебника — показать, как интегрировать Azure Active Directory (Azure AD) с приложением @Task.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="e3eb4-105">Интеграция Azure AD с приложением @Task обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e3eb4-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="e3eb4-106">С помощью Azure AD вы можете контролировать доступ к @Task.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="e3eb4-107">Вы можете включить автоматический вход пользователей в @Task (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="e3eb4-108">Вы можете управлять учетными записями централизованно — на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="e3eb4-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3eb4-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3eb4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e3eb4-110">Prerequisites</span></span>
<span data-ttu-id="e3eb4-111">Для настройки интеграции с Azure AD с @Task, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="e3eb4-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="e3eb4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e3eb4-112">An Azure AD subscription</span></span>
* <span data-ttu-id="e3eb4-113">подписка на @Task с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3eb4-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="e3eb4-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e3eb4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="e3eb4-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e3eb4-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3eb4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="e3eb4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e3eb4-118">Scenario Description</span></span>
<span data-ttu-id="e3eb4-119">Цель этого учебника — научить вас проверять единый вход в Azure AD в пробной среде.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="e3eb4-120">Сценарий, описанный в этом учебнике, состоит из следующих основных блоков.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="e3eb4-121">Добавление @Task из коллекции</span><span class="sxs-lookup"><span data-stu-id="e3eb4-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="e3eb4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3eb4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="e3eb4-123">Добавление @Task из коллекции</span><span class="sxs-lookup"><span data-stu-id="e3eb4-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="e3eb4-124">Чтобы настроить интеграцию @Task с Azure AD, необходимо добавить @Task из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e3eb4-125">**Чтобы добавить @Task из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e3eb4-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e3eb4-126">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="e3eb4-128">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e3eb4-129">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Приложения][2] 
4. <span data-ttu-id="e3eb4-131">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="e3eb4-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Приложения][3] 
5. <span data-ttu-id="e3eb4-133">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Приложения][4] 
6. <span data-ttu-id="e3eb4-135">В поле поиска введите **@Task**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-135">In the search box, type **@Task**.</span></span>
   
    ![Приложения][5] 
7. <span data-ttu-id="e3eb4-137">В области результатов выберите **@Task** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![Приложения][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e3eb4-139">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e3eb4-140">Цель этого раздела — показать, как настроить и проверить единый вход Azure AD в @Task с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e3eb4-141">Для работы единого входа в Azure AD необходимо знать, какой пользователь в @Task соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="e3eb4-142">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в @Task.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="e3eb4-143">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в @Task.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="e3eb4-144">Для настройки и проверки Azure AD единого входа с @Task, необходимо выполнить следующие стандартные блоки:</span><span class="sxs-lookup"><span data-stu-id="e3eb4-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e3eb4-145">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e3eb4-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3eb4-147">**[Создание тестового пользователя @Tasktest](#creating-a-halogen-software-test-user)** требуется для создания в @Taskthat пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e3eb4-148">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3eb4-149">**[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e3eb4-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3eb4-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="e3eb4-151">В этом разделе описано, как включить единый вход Azure AD на классическом портале Azure AD и настроить единый вход в приложение @Task.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="e3eb4-152">**Чтобы настроить Azure AD единого входа с @Task, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e3eb4-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="e3eb4-153">На классическом портале Azure на странице интеграции с приложением **@Task** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][6] 
2. <span data-ttu-id="e3eb4-155">На странице **Как пользователи должны входить в @Task?** выберите **Единый вход Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![единого входа Azure AD][7] 
3. <span data-ttu-id="e3eb4-157">В диалоговом окне на странице **Настройка параметров приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Настройка параметров приложения][8] 
   
     <span data-ttu-id="e3eb4-159">а.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-159">a.</span></span> <span data-ttu-id="e3eb4-160">В текстовом поле **URL-адрес входа** введите URL-адрес, используемый пользователями для входа в приложение @Task (например, *https://<Tenant name>.attask-ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="e3eb4-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="e3eb4-161">b.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-161">b.</span></span> <span data-ttu-id="e3eb4-162">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-162">Click **Next**.</span></span>
4. <span data-ttu-id="e3eb4-163">На странице **Настройка единого входа в @Task** нажмите кнопку **Скачать метаданные**, а затем сохраните файл метаданных на локальном компьютере и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Что такое Azure AD Connect?][9] 
5. <span data-ttu-id="e3eb4-165">Выполните вход на сайт компании @Task в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="e3eb4-166">Перейдите к **Настройке единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="e3eb4-167">В диалоговом окне **Единый вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![Настройка единого входа][23]
   
    <span data-ttu-id="e3eb4-169">а.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-169">a.</span></span> <span data-ttu-id="e3eb4-170">Для параметра **Тип** выберите значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="e3eb4-171">b.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-171">b.</span></span> <span data-ttu-id="e3eb4-172">Выберите **идентификатор поставщика службы**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="e3eb4-173">c.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-173">c.</span></span> <span data-ttu-id="e3eb4-174">На классическом портале Azure скопируйте **URL-адрес удаленного входа** и вставьте его в текстовое поле **Login Portal URL** (URL-адрес портала входа).</span><span class="sxs-lookup"><span data-stu-id="e3eb4-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="e3eb4-175">d.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-175">d.</span></span> <span data-ttu-id="e3eb4-176">На классическом портале Azure скопируйте **URL-адрес службы единого выхода** и вставьте его в текстовое поле **URL-адрес выхода**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="e3eb4-177">д.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-177">e.</span></span> <span data-ttu-id="e3eb4-178">На классическом портале Azure скопируйте адрес в поле **Изменить URL-адрес пароля** и вставьте его в текстовое поле **Изменить URL-адрес пароля**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="e3eb4-179">Е.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-179">f.</span></span> <span data-ttu-id="e3eb4-180">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-180">Click **Save**.</span></span>
8. <span data-ttu-id="e3eb4-181">На классическом портале Azure выберите подтверждение конфигурации единого входа и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Что такое Azure AD Connect?][10]
9. <span data-ttu-id="e3eb4-183">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Что такое Azure AD Connect?][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e3eb4-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3eb4-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="e3eb4-186">Цель этого раздела — создать на классическом портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Создание пользователя Azure AD][20]

<span data-ttu-id="e3eb4-188">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e3eb4-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e3eb4-189">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="e3eb4-191">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e3eb4-192">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="e3eb4-194">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="e3eb4-196">На странице диалогового окна **Тип учетной записи пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="e3eb4-198">а.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-198">a.</span></span> <span data-ttu-id="e3eb4-199">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="e3eb4-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="e3eb4-200">b.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-200">b.</span></span> <span data-ttu-id="e3eb4-201">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="e3eb4-202">c.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-202">c.</span></span> <span data-ttu-id="e3eb4-203">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-203">Click **Next**.</span></span>
6. <span data-ttu-id="e3eb4-204">На странице диалогового окна **Профиль пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="e3eb4-206">а.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-206">a.</span></span> <span data-ttu-id="e3eb4-207">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="e3eb4-208">b.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-208">b.</span></span> <span data-ttu-id="e3eb4-209">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="e3eb4-210">c.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-210">c.</span></span> <span data-ttu-id="e3eb4-211">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="e3eb4-212">d.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-212">d.</span></span> <span data-ttu-id="e3eb4-213">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="e3eb4-214">д.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-214">e.</span></span> <span data-ttu-id="e3eb4-215">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-215">Click **Next**.</span></span>

7. <span data-ttu-id="e3eb4-216">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="e3eb4-218">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="e3eb4-220">а.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-220">a.</span></span> <span data-ttu-id="e3eb4-221">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="e3eb4-222">b.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-222">b.</span></span> <span data-ttu-id="e3eb4-223">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="e3eb4-224">Создание тестового пользователя @Task</span><span class="sxs-lookup"><span data-stu-id="e3eb4-224">Creating an @Task test user</span></span>
<span data-ttu-id="e3eb4-225">Цель этого раздела — создать пользователя с именем Britta Simon в @Task.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="e3eb4-226">**Чтобы создать пользователя с именем Саймон Britta @Task, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e3eb4-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="e3eb4-227">Выполните вход на сайт компании @Task в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="e3eb4-228">В верхнем меню щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="e3eb4-229">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="e3eb4-230">В диалоговом окне "Новый пользователь" выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e3eb4-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![Создание тестового пользователя @Task][21] 
   
    <span data-ttu-id="e3eb4-232">а.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-232">a.</span></span> <span data-ttu-id="e3eb4-233">В текстовом поле **Имя** введите Britta.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="e3eb4-234">b.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-234">b.</span></span> <span data-ttu-id="e3eb4-235">В текстовом поле **Фамилия** введите Simon.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="e3eb4-236">c.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-236">c.</span></span> <span data-ttu-id="e3eb4-237">В текстовом поле **адрес электронной почты** введите адрес электронной почты пользователя Britta Simon в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="e3eb4-238">d.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-238">d.</span></span> <span data-ttu-id="e3eb4-239">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e3eb4-240">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3eb4-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="e3eb4-241">Цель этого раздела — позволить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к @Task.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e3eb4-243">**Для назначения Саймон Britta для @Task, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e3eb4-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="e3eb4-244">Чтобы открыть представление приложений, на классическом портале Azure в представлении каталога щелкните **Приложения** в меню вверху.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Назначение пользователя][201] 
2. <span data-ttu-id="e3eb4-246">В списке приложений выберите **@Task**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-246">In the applications list, select **@Task**.</span></span>
   
    ![Назначение пользователя][202] 
3. <span data-ttu-id="e3eb4-248">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-248">In the menu on the top, click **Users**.</span></span>
   
    ![Назначение пользователя][203] 
4. <span data-ttu-id="e3eb4-250">В списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="e3eb4-251">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="e3eb4-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e3eb4-253">Testing Single Sign-On</span></span>
<span data-ttu-id="e3eb4-254">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="e3eb4-255">Щелкнув элемент @Task на панели доступа, вы автоматически войдете в приложение @Task.</span><span class="sxs-lookup"><span data-stu-id="e3eb4-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3eb4-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e3eb4-256">Additional Resources</span></span>
* [<span data-ttu-id="e3eb4-257">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3eb4-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3eb4-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e3eb4-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






