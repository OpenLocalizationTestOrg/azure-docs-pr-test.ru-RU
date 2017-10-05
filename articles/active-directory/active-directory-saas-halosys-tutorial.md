---
title: "Руководство по интеграции Azure Active Directory с Halosys | Документация Майкрософт"
description: "Узнайте, как использовать Halosys вместе с Azure Active Directory для реализации единого входа, автоматической подготовки пользователей и выполнения других задач."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="b9f91-103">Руководство по интеграции Azure Active Directory с Halosys</span><span class="sxs-lookup"><span data-stu-id="b9f91-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="b9f91-104">В этом руководстве описано, как интегрировать приложение Halosys с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9f91-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9f91-105">Интеграция Halosys с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b9f91-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9f91-106">С помощью Azure AD вы можете контролировать доступ к Halosys.</span><span class="sxs-lookup"><span data-stu-id="b9f91-106">You can control in Azure AD who has access to Halosys</span></span>
- <span data-ttu-id="b9f91-107">Вы можете включить автоматический вход пользователей в Halosys (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9f91-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9f91-108">Вы можете управлять учетными записями централизованно — через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f91-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="b9f91-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9f91-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9f91-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b9f91-110">Prerequisites</span></span>

<span data-ttu-id="b9f91-111">Чтобы настроить интеграцию Azure AD с Halosys, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b9f91-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="b9f91-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b9f91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9f91-113">подписка Halosys с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9f91-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="b9f91-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b9f91-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="b9f91-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b9f91-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9f91-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="b9f91-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b9f91-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9f91-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b9f91-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b9f91-118">Scenario description</span></span>
<span data-ttu-id="b9f91-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b9f91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="b9f91-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b9f91-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9f91-121">Добавление Halosys из коллекции</span><span class="sxs-lookup"><span data-stu-id="b9f91-121">Adding Halosys from the gallery</span></span>
2. <span data-ttu-id="b9f91-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9f91-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="b9f91-123">Добавление Halosys из коллекции</span><span class="sxs-lookup"><span data-stu-id="b9f91-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="b9f91-124">Чтобы настроить интеграцию Halosys с Azure AD, необходимо добавить Halosys из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b9f91-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9f91-125">**Чтобы добавить Halosys из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b9f91-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9f91-126">На **классическом портале Azure**в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="b9f91-128">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="b9f91-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b9f91-129">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="b9f91-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Приложения][2]

4. <span data-ttu-id="b9f91-131">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="b9f91-131">Click **Add** at the bottom of the page.</span></span>

    ![Приложения][3]

5. <span data-ttu-id="b9f91-133">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Приложения][4]

6. <span data-ttu-id="b9f91-135">В поле поиска введите **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-135">In the search box, type **Halosys**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="b9f91-137">В области результатов выберите **Halosys** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="b9f91-137">In the results pane, select **Halosys**, and then click **Complete** to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9f91-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9f91-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9f91-140">В этом разделе описана настройка и проверка единого входа Azure AD в Halosys с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9f91-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9f91-141">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Halosys соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9f91-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="b9f91-142">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Halosys.</span><span class="sxs-lookup"><span data-stu-id="b9f91-142">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="b9f91-143">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Halosys.</span><span class="sxs-lookup"><span data-stu-id="b9f91-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halosys.</span></span>

<span data-ttu-id="b9f91-144">Чтобы настроить и проверить единый вход Azure AD в Halosys, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="b9f91-144">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9f91-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b9f91-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9f91-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9f91-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9f91-147">**[Создание тестового пользователя Halosys](#creating-a-halosys-test-user)** требуется для создания в Halosys пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9f91-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b9f91-148">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9f91-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9f91-149">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b9f91-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9f91-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9f91-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9f91-151">В этом разделе описано, как включить единый вход Azure AD на классическом портале и настроить его в приложении Halosys.</span><span class="sxs-lookup"><span data-stu-id="b9f91-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="b9f91-152">**Чтобы настроить единый вход Azure AD в Halosys, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b9f91-152">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="b9f91-153">На классическом портале на странице интеграции с приложением **Halosys** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-153">In the classic portal, on the **Halosys** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Настройка единого входа][6] 

2. <span data-ttu-id="b9f91-155">На странице **Как пользователи должны входить в Halosys?** выберите **Единый вход Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-155">On the **How would you like users to sign on to Halosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="b9f91-157">В диалоговом окне на странице **Настройка параметров приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b9f91-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="b9f91-159">а.</span><span class="sxs-lookup"><span data-stu-id="b9f91-159">a.</span></span> <span data-ttu-id="b9f91-160">В текстовом поле **URL-адрес для входа** введите URL-адрес, используемый пользователями для входа в приложение Halosys, в следующем формате: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="b9f91-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Halosys application using the following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="b9f91-161">В текстовом поле **Identifier URL** (URL-адрес идентификатора) введите URL-адрес в следующем формате: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="b9f91-161">b.In the **Identifier URL** textbox, type the URL in the following pattern: `https://<company-name>.Halosys.com`.</span></span>   
         
4. <span data-ttu-id="b9f91-162">На странице **Настройка единого входа в Halosys** нажмите кнопку **Скачать метаданные**, а затем сохраните файл метаданных на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b9f91-162">On the **Configure single sign-on at Halosys** page, click **Download metadata**, and then save the file on your computer:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="b9f91-164">Чтобы настроить единый вход для своего приложения, обратитесь в службу поддержки Halosys и предоставьте следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="b9f91-164">To get SSO configured for your application, contact Halosys support team and provide them with the following:</span></span>

    <span data-ttu-id="b9f91-165">• скачанный файл **метаданных**;</span><span class="sxs-lookup"><span data-stu-id="b9f91-165">• The downloaded **metadata file**</span></span>
    
    <span data-ttu-id="b9f91-166">• **URL-адрес единого входа SAML**</span><span class="sxs-lookup"><span data-stu-id="b9f91-166">• The **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="b9f91-167">На классическом портале выберите подтверждение конфигурации единого входа и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![единого входа Azure AD][10]

7. <span data-ttu-id="b9f91-169">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![единого входа Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9f91-171">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9f91-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9f91-172">В этом разделе описано, как создать на классическом портале тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9f91-172">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Создание пользователя Azure AD][20]

<span data-ttu-id="b9f91-174">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b9f91-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9f91-175">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="b9f91-177">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="b9f91-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b9f91-178">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9f91-180">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="b9f91-182">На **сообщите нам об этом пользователе** диалогового окна выполните следующие действия: ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="b9f91-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="b9f91-183">а.</span><span class="sxs-lookup"><span data-stu-id="b9f91-183">a.</span></span> <span data-ttu-id="b9f91-184">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="b9f91-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="b9f91-185">b.</span><span class="sxs-lookup"><span data-stu-id="b9f91-185">b.</span></span> <span data-ttu-id="b9f91-186">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9f91-187">c.</span><span class="sxs-lookup"><span data-stu-id="b9f91-187">c.</span></span> <span data-ttu-id="b9f91-188">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-188">Click **Next**.</span></span>

6.  <span data-ttu-id="b9f91-189">На странице диалогового окна **Профиль пользователя** выполните следующие действия. ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="b9f91-189">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="b9f91-190">а.</span><span class="sxs-lookup"><span data-stu-id="b9f91-190">a.</span></span> <span data-ttu-id="b9f91-191">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-191">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="b9f91-192">b.</span><span class="sxs-lookup"><span data-stu-id="b9f91-192">b.</span></span> <span data-ttu-id="b9f91-193">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-193">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="b9f91-194">c.</span><span class="sxs-lookup"><span data-stu-id="b9f91-194">c.</span></span> <span data-ttu-id="b9f91-195">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="b9f91-196">d.</span><span class="sxs-lookup"><span data-stu-id="b9f91-196">d.</span></span> <span data-ttu-id="b9f91-197">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-197">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="b9f91-198">д.</span><span class="sxs-lookup"><span data-stu-id="b9f91-198">e.</span></span> <span data-ttu-id="b9f91-199">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-199">Click **Next**.</span></span>

7. <span data-ttu-id="b9f91-200">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="b9f91-202">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b9f91-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="b9f91-204">а.</span><span class="sxs-lookup"><span data-stu-id="b9f91-204">a.</span></span> <span data-ttu-id="b9f91-205">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-205">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="b9f91-206">b.</span><span class="sxs-lookup"><span data-stu-id="b9f91-206">b.</span></span> <span data-ttu-id="b9f91-207">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="b9f91-208">Создание тестового пользователя Halosys</span><span class="sxs-lookup"><span data-stu-id="b9f91-208">Creating a Halosys test user</span></span>

<span data-ttu-id="b9f91-209">В этом разделе описано, как создать пользователя Britta Simon в приложении Halosys.</span><span class="sxs-lookup"><span data-stu-id="b9f91-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="b9f91-210">Обратитесь в службу поддержки Halosys, чтобы добавить пользователей на платформу Halosys.</span><span class="sxs-lookup"><span data-stu-id="b9f91-210">Please work with Halosys support team to add the users in the Halosys platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b9f91-211">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9f91-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b9f91-212">Цель этого раздела — разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Halosys.</span><span class="sxs-lookup"><span data-stu-id="b9f91-212">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Halosys.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b9f91-214">**Чтобы назначить пользователя Britta Simon в Halosys, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b9f91-214">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="b9f91-215">Чтобы открыть представление приложений, в представлении каталога на классическом портале щелкните **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="b9f91-215">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b9f91-217">В списке приложений выберите **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-217">In the applications list, select **Halosys**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="b9f91-219">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-219">In the menu on the top, click **Users**.</span></span>

    ![Назначение пользователя][203]

4. <span data-ttu-id="b9f91-221">В списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-221">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="b9f91-222">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b9f91-222">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Назначение пользователя][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="b9f91-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b9f91-224">Testing single sign-on</span></span>

<span data-ttu-id="b9f91-225">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b9f91-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9f91-226">Щелкнув элемент Halosys на панели доступа, вы автоматически войдете в приложение Halosys.</span><span class="sxs-lookup"><span data-stu-id="b9f91-226">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b9f91-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b9f91-227">Additional resources</span></span>

* [<span data-ttu-id="b9f91-228">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9f91-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9f91-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9f91-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
