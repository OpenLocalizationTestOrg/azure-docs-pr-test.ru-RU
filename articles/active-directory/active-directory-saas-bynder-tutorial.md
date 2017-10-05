---
title: "Руководство. Интеграция Azure Active Directory с приложением Bynder | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="7f47e-103">Руководство. Интеграция Azure Active Directory с Bynder</span><span class="sxs-lookup"><span data-stu-id="7f47e-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="7f47e-104">Цель этого руководства — показать, как интегрировать Azure Active Directory (Azure AD) с приложением Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f47e-105">Интеграция Azure AD с приложением Bynder обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7f47e-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="7f47e-106">С помощью Azure AD вы можете контролировать доступ к Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="7f47e-107">Вы можете включить автоматический вход пользователей в Bynder (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f47e-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="7f47e-108">Вы можете управлять учетными записями централизованно — через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7f47e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="7f47e-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f47e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f47e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7f47e-110">Prerequisites</span></span>
<span data-ttu-id="7f47e-111">Чтобы настроить интеграцию Azure AD с Bynder, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="7f47e-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="7f47e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7f47e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7f47e-113">подписка на Bynder с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f47e-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="7f47e-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7f47e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="7f47e-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7f47e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7f47e-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="7f47e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7f47e-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f47e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f47e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7f47e-118">Scenario description</span></span>
<span data-ttu-id="7f47e-119">Цель этого руководства — научить вас проверять единый вход Microsoft Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7f47e-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="7f47e-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="7f47e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f47e-121">Добавление Bynder из коллекции.</span><span class="sxs-lookup"><span data-stu-id="7f47e-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="7f47e-122">Настройка и проверка единого входа Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f47e-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="7f47e-123">Добавление Bynder из коллекции</span><span class="sxs-lookup"><span data-stu-id="7f47e-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="7f47e-124">Чтобы настроить интеграцию Bynder с Azure AD, необходимо добавить Bynder из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7f47e-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f47e-125">**Чтобы добавить Bynder из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="7f47e-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7f47e-126">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="7f47e-128">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="7f47e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7f47e-129">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="7f47e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Приложения][2]
4. <span data-ttu-id="7f47e-131">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="7f47e-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Приложения][3]
5. <span data-ttu-id="7f47e-133">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Приложения][4]
6. <span data-ttu-id="7f47e-135">В поле поиска введите **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-135">In the search box, type **Bynder**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="7f47e-137">На панели результатов выберите **Bynder** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="7f47e-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![Выбор приложения в коллекции](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="7f47e-139">Настройка и проверка единого входа Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f47e-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="7f47e-140">Цель этого раздела — показать, как настроить и проверить единый вход Microsoft Azure AD в Bynder с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f47e-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f47e-141">Чтобы единый вход работал, в Azure AD необходимо указать, какой пользователь в Bynder соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f47e-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="7f47e-142">Другими словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="7f47e-143">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="7f47e-144">Чтобы настроить и проверить единый вход Microsoft Azure AD в Bynder, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="7f47e-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f47e-145">**[Настройка единого входа Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)** необходима, чтобы позволить пользователям использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7f47e-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7f47e-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Microsoft Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f47e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="7f47e-147">**[Создание тестового пользователя Bynder](#creating-a-bynder-test-user)** требуется для создания пользователя Britta Simon в Bynder, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f47e-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7f47e-148">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f47e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="7f47e-149">**[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7f47e-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="7f47e-150">Настройка единого входа Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f47e-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="7f47e-151">В этом разделе описано, как включить единый вход Microsoft Azure AD на классическом портале и настроить его в приложении Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="7f47e-152">**Чтобы настроить единый вход Microsoft Azure AD в Bynder, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="7f47e-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="7f47e-153">На классическом портале на странице интеграции с приложением **Bynder** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][6] 
2. <span data-ttu-id="7f47e-155">На странице **Как пользователи должны входить в Bynder?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="7f47e-157">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то на странице диалогового окна **Настроить параметры приложения** выполните следующие действия и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="7f47e-159">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<company name>.getbynder.com/sso/SAML/authenticate/`.</span><span class="sxs-lookup"><span data-stu-id="7f47e-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="7f47e-160">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-160">Click **Next**.</span></span>
4. <span data-ttu-id="7f47e-161">Если вы хотите настроить приложение в **режиме, инициированном поставщиком услуг**, то на странице диалогового окна **Настроить параметры приложения** щелкните **Показать дополнительные параметры (необязательно)**, а затем введите **URL-адрес для входа** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="7f47e-163">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.getbynder.com/login/`.</span><span class="sxs-lookup"><span data-stu-id="7f47e-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="7f47e-164">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="7f47e-165">Значение URL-адреса входа в этом руководстве — просто заполнитель.</span><span class="sxs-lookup"><span data-stu-id="7f47e-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="7f47e-166">Чтобы получить фактическое значение для своей среды, обратитесь в службу поддержки Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="7f47e-167">На странице **Настройка единого входа в Bynder** выполните следующие действия и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="7f47e-169">Нажмите **Загрузить метаданные**и сохраните файл на свой компьютер.</span><span class="sxs-lookup"><span data-stu-id="7f47e-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="7f47e-170">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-170">Click **Next**.</span></span>
6. <span data-ttu-id="7f47e-171">Чтобы настроить единый вход для своего приложения, обратитесь в службу поддержки Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="7f47e-172">Присоедините к сообщению скачанный файл метаданных, чтобы специалисты Bynder смогли настроить единый вход со своей стороны.</span><span class="sxs-lookup"><span data-stu-id="7f47e-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="7f47e-173">На классическом портале подтвердите конфигурацию единого входа и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![единого входа Azure AD][10]
8. <span data-ttu-id="7f47e-175">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![единого входа Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f47e-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f47e-177">Create an Azure AD test user</span></span>
<span data-ttu-id="7f47e-178">Цель этого раздела — создать на классическом портале тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f47e-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="7f47e-180">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7f47e-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7f47e-181">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="7f47e-183">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="7f47e-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7f47e-184">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="7f47e-186">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="7f47e-188">На странице диалогового окна **Тип учетной записи пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7f47e-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="7f47e-190">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="7f47e-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="7f47e-191">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="7f47e-192">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-192">Click **Next**.</span></span>
6. <span data-ttu-id="7f47e-193">На странице диалогового окна **Профиль пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7f47e-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="7f47e-195">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="7f47e-196">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="7f47e-197">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="7f47e-198">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="7f47e-199">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-199">Click **Next**.</span></span>
7. <span data-ttu-id="7f47e-200">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="7f47e-202">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7f47e-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="7f47e-204">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="7f47e-205">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="7f47e-206">Создание тестового пользователя Bynder</span><span class="sxs-lookup"><span data-stu-id="7f47e-206">Create a Bynder test user</span></span>
<span data-ttu-id="7f47e-207">Цель этого раздела — создать пользователя с именем Britta Simon в приложении Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="7f47e-208">Приложение Bynder поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7f47e-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7f47e-209">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="7f47e-209">There is no action item for you in this section.</span></span> <span data-ttu-id="7f47e-210">Пользователь будет создан при попытке получить доступ к приложению Bynder (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="7f47e-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7f47e-211">Чтобы создать пользователя вручную, необходимо обратиться в службу поддержки Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7f47e-212">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f47e-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="7f47e-213">Цель этого раздела — предоставить пользователю Britta Simon доступ к Bynder, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="7f47e-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Назначение пользователя][200]

<span data-ttu-id="7f47e-215">**Чтобы назначить пользователя Britta Simon в приложении Bynder, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="7f47e-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="7f47e-216">Чтобы открыть представление приложений, в представлении каталога на классическом портале щелкните **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="7f47e-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Назначение пользователя][201]
2. <span data-ttu-id="7f47e-218">В списке приложений выберите **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-218">In the applications list, select **Bynder**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="7f47e-220">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-220">In the menu on the top, click **Users**.</span></span>
   
    ![Назначение пользователя][203]
4. <span data-ttu-id="7f47e-222">В списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7f47e-223">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7f47e-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="7f47e-225">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7f47e-225">Test single sign-on</span></span>
<span data-ttu-id="7f47e-226">Цель этого раздела — проверить конфигурацию единого входа Microsoft Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7f47e-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7f47e-227">Щелкнув элемент Bynder на панели доступа, вы автоматически войдете в приложение Bynder.</span><span class="sxs-lookup"><span data-stu-id="7f47e-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7f47e-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7f47e-228">Additional resources</span></span>
* [<span data-ttu-id="7f47e-229">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f47e-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f47e-230">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f47e-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
