---
title: "Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Splunk Enterprise и Splunk Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="692eb-103">Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="692eb-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="692eb-104">В этом руководстве описано, как интегрировать Splunk Enterprise и Splunk Cloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="692eb-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="692eb-105">Интеграция Splunk Enterprise и Splunk Cloud с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="692eb-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="692eb-106">С помощью Azure AD можно контролировать доступ к Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="692eb-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="692eb-107">Вы можете включить автоматический вход пользователей в Splunk Enterprise и Splunk Cloud (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692eb-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="692eb-108">Вы можете управлять учетными записями централизованно — через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="692eb-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="692eb-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="692eb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="692eb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="692eb-110">Prerequisites</span></span>

<span data-ttu-id="692eb-111">Чтобы настроить интеграцию Azure AD с приложениями Splunk Enterprise и Splunk Cloud, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="692eb-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="692eb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="692eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="692eb-113">подписка Splunk Enterprise или Splunk Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="692eb-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="692eb-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="692eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="692eb-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="692eb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="692eb-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="692eb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="692eb-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="692eb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="692eb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="692eb-118">Scenario description</span></span>
<span data-ttu-id="692eb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="692eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="692eb-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="692eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="692eb-121">Добавление Splunk Enterprise и Splunk Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="692eb-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="692eb-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692eb-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="692eb-123">Добавление Splunk Enterprise и Splunk Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="692eb-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="692eb-124">Чтобы настроить интеграцию Splunk Enterprise и Splunk Cloud с Azure AD, необходимо добавить Splunk Enterprise и Splunk Cloud из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="692eb-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="692eb-125">**Чтобы добавить Splunk Enterprise и Splunk Cloud из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="692eb-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="692eb-126">На **классическом портале Azure**в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="692eb-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="692eb-128">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="692eb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="692eb-129">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="692eb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Приложения][2]

4. <span data-ttu-id="692eb-131">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="692eb-131">Click **Add** at the bottom of the page.</span></span>

    ![Приложения][3]

5. <span data-ttu-id="692eb-133">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="692eb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Приложения][4]

6. <span data-ttu-id="692eb-135">В поле поиска введите **Splunk Enterprise или Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="692eb-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="692eb-137">В области результатов выберите **Splunk Enterprise и Splunk Cloud**, а затем нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="692eb-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="692eb-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="692eb-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="692eb-140">В этом разделе описывается настройка и проверка единого входа Azure AD в Splunk Enterprise и Splunk Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692eb-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="692eb-141">Для работы единого входа в Azure AD необходимо указать, какой пользователь в Splunk Enterprise и Splunk Cloud соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692eb-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="692eb-142">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="692eb-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="692eb-143">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="692eb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="692eb-144">Чтобы настроить и проверить единый вход Azure AD в Splunk Enterprise и Splunk Cloud, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="692eb-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="692eb-145">**[Настройка единого входа Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="692eb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="692eb-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692eb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="692eb-147">**[Создание тестового пользователя Splunk Enterprise и Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** требуется для создания пользователя Britta Simon в Splunk Enterprise и Splunk Cloud, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692eb-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="692eb-148">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692eb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="692eb-149">**[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="692eb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="692eb-150">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="692eb-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="692eb-151">В этом разделе описано, как включить единый вход Azure AD на классическом портале и настроить единый вход в приложении Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="692eb-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="692eb-152">**Чтобы настроить единый вход Azure AD в Splunk Enterprise и Splunk Cloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="692eb-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="692eb-153">На странице интеграции с приложениями **Splunk Enterprise и Splunk Cloud** классического портала щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="692eb-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Настройка единого входа][6] 

2. <span data-ttu-id="692eb-155">На странице **Как пользователи должны входить в Splunk Enterprise и Splunk Cloud** выберите **Единый вход Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="692eb-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="692eb-157">В диалоговом окне на странице **Настройка параметров приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="692eb-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="692eb-159">В текстовом поле **URL-адрес входа** введите URL-адрес, с помощью которого пользователи входят в приложение Splunk Enterprise и Splunk Cloud, в следующем формате: `https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="692eb-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="692eb-160">В текстовом поле **Идентификатор** введите URL-адрес сервера Splunk Server.</span><span class="sxs-lookup"><span data-stu-id="692eb-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="692eb-161">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="692eb-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="692eb-162">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="692eb-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="692eb-163">На странице **Настройка единого входа в Splunk Enterprise и Splunk Cloud** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="692eb-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="692eb-165">Нажмите **Загрузить метаданные**и сохраните файл на свой компьютер.</span><span class="sxs-lookup"><span data-stu-id="692eb-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="692eb-166">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="692eb-166">Click **Next**.</span></span>

5. <span data-ttu-id="692eb-167">Чтобы настроить единый вход для своего приложения, обратитесь в службу поддержки Splunk Enterprise и Splunk Cloud и укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="692eb-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="692eb-168">Скачанный файл с **метаданными федерации**.</span><span class="sxs-lookup"><span data-stu-id="692eb-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="692eb-169">На классическом портале подтвердите конфигурацию единого входа и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="692eb-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![единого входа Azure AD][10]

7. <span data-ttu-id="692eb-171">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="692eb-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![единого входа Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="692eb-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="692eb-173">Create an Azure AD test user</span></span>
<span data-ttu-id="692eb-174">В этом разделе описано, как создать на классическом портале тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692eb-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="692eb-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="692eb-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="692eb-177">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="692eb-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="692eb-179">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="692eb-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="692eb-180">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="692eb-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="692eb-182">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="692eb-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="692eb-184">На странице диалогового окна **Тип учетной записи пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="692eb-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="692eb-186">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="692eb-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="692eb-187">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="692eb-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="692eb-188">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="692eb-188">Click **Next**.</span></span>

6.  <span data-ttu-id="692eb-189">На странице диалогового окна **Профиль пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="692eb-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="692eb-191">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="692eb-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="692eb-192">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="692eb-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="692eb-193">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="692eb-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="692eb-194">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="692eb-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="692eb-195">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="692eb-195">Click **Next**.</span></span>

7. <span data-ttu-id="692eb-196">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="692eb-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="692eb-198">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="692eb-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="692eb-200">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="692eb-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="692eb-201">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="692eb-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="692eb-202">Создание тестового пользователя Splunk Enterprise и Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="692eb-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="692eb-203">В этом разделе описано, как создать пользователя Britta Simon в Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="692eb-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="692eb-204">Чтобы добавить пользователей в Splunk Enterprise и Splunk Cloud, обратитесь в службу поддержки платформы Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="692eb-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="692eb-205">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="692eb-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="692eb-206">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ей доступ к Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="692eb-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="692eb-208">**Чтобы назначить Britta Simon в Splunk Enterprise и Splunk Cloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="692eb-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="692eb-209">Чтобы открыть представление приложений, в представлении каталога на классическом портале щелкните **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="692eb-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="692eb-211">В списке приложений выберите **Splunk Enterprise и Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="692eb-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="692eb-213">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="692eb-213">In the menu on the top, click **Users**.</span></span>

    ![Назначение пользователя][203]

4. <span data-ttu-id="692eb-215">В списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="692eb-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="692eb-216">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="692eb-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="692eb-218">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="692eb-218">Test single sign-on</span></span>

<span data-ttu-id="692eb-219">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="692eb-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="692eb-220">Щелкнув плитку Splunk Enterprise и Splunk Cloud на панели доступа, вы автоматически войдете в приложение Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="692eb-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="692eb-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="692eb-221">Additional resources</span></span>

* [<span data-ttu-id="692eb-222">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="692eb-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="692eb-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="692eb-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
