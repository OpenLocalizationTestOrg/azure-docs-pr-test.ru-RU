---
title: "Руководство по интеграции Azure Active Directory с Soonr Workplace | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Soonr Workplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="e0492-103">Учебник. Интеграция Azure Active Directory с Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="e0492-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="e0492-104">Цель этого учебника — показать, как интегрировать приложение Soonr Workplace с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e0492-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="e0492-105">Интеграция Soonr Workplace с Azure AD дает приведенные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="e0492-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0492-106">С помощью Azure AD вы можете контролировать доступ к приложению Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="e0492-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="e0492-107">Вы можете включить автоматический вход пользователей в Soonr Workplace (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0492-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0492-108">Вы можете управлять учетными записями централизованно — через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e0492-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="e0492-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0492-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0492-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e0492-110">Prerequisites</span></span>

<span data-ttu-id="e0492-111">Чтобы настроить интеграцию Azure AD с Soonr Workplace, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e0492-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="e0492-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e0492-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0492-113">подписка Soonr Workplace с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e0492-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="e0492-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e0492-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="e0492-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e0492-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0492-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="e0492-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e0492-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0492-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e0492-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e0492-118">Scenario description</span></span>
<span data-ttu-id="e0492-119">Цель этого учебника — научить вас проверять единый вход в Azure AD в пробной среде.</span><span class="sxs-lookup"><span data-stu-id="e0492-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="e0492-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e0492-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0492-121">Добавление Soonr Workplace из коллекции.</span><span class="sxs-lookup"><span data-stu-id="e0492-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="e0492-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0492-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="e0492-123">Добавление Soonr Workplace из коллекции.</span><span class="sxs-lookup"><span data-stu-id="e0492-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="e0492-124">Чтобы настроить интеграцию Soonr Workplace с Azure AD, необходимо добавить Soonr Workplace из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e0492-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0492-125">**Чтобы добавить Soonr Workplace из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e0492-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0492-126">На **классическом портале Azure**в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0492-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0492-128">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="e0492-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="e0492-129">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="e0492-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Приложения][2]

4. <span data-ttu-id="e0492-131">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="e0492-131">Click **Add** at the bottom of the page.</span></span>

    ![Приложения][3]

5. <span data-ttu-id="e0492-133">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="e0492-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Приложения][4]

6. <span data-ttu-id="e0492-135">В поле поиска введите **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="e0492-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="e0492-137">В области результатов выберите **Soonr Workplace** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e0492-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0492-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0492-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0492-140">Цель этого раздела — показать, как настроить и проверить единый вход Azure AD в приложении Soonr Workplace с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0492-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e0492-141">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Soonr Workplace соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0492-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="e0492-142">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="e0492-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="e0492-143">Чтобы установить эту связь, следует указать **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="e0492-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="e0492-144">Чтобы настроить и проверить единый вход Azure AD в Soonr Workplace, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="e0492-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0492-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e0492-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0492-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0492-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0492-147">**[Создание тестового пользователя Soonr Workplace](#creating-a-soonr-workplace-test-user)** требуется для создания в Soonr Workplace соответствующего пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0492-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e0492-148">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0492-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0492-149">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e0492-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0492-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0492-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0492-151">В этом разделе описано, как включить единый вход Azure AD на классическом портале и настроить его в приложении Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="e0492-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="e0492-152">**Чтобы настроить единый вход Azure AD в Soonr Workplace, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e0492-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="e0492-153">На классическом портале Azure на странице интеграции с приложением **Soonr Workplace** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e0492-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Настройка единого входа][6] 

2. <span data-ttu-id="e0492-155">На странице **Как пользователи должны входить в Soonr Workplace?** выберите **Единый вход Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0492-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="e0492-157">На странице диалогового окна **Настройка параметров приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e0492-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="e0492-159">а.</span><span class="sxs-lookup"><span data-stu-id="e0492-159">a.</span></span> <span data-ttu-id="e0492-160">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="e0492-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="e0492-161">b.</span><span class="sxs-lookup"><span data-stu-id="e0492-161">b.</span></span> <span data-ttu-id="e0492-162">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0492-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e0492-163">Обратите внимание, что это значение используется только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e0492-163">Please note that this is not the real value.</span></span> <span data-ttu-id="e0492-164">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="e0492-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="e0492-165">Чтобы получить это значение, обратитесь в службу поддержки Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="e0492-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="e0492-166">На странице **Настройка единого входа в Soonr Workplace** нажмите кнопку **Скачать метаданные**, а затем сохраните файл метаданных на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e0492-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="e0492-168">Чтобы настроить единый вход для своего приложения, обратитесь в службу поддержки Soonr Workplace и предоставьте следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e0492-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="e0492-169">• скачанный файл **метаданных**;</span><span class="sxs-lookup"><span data-stu-id="e0492-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="e0492-170">• **URL-адрес издателя**;</span><span class="sxs-lookup"><span data-stu-id="e0492-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="e0492-171">• **URL-адрес единого входа SAML**;</span><span class="sxs-lookup"><span data-stu-id="e0492-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="e0492-172">• **URL-адрес службы единого выхода**.</span><span class="sxs-lookup"><span data-stu-id="e0492-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="e0492-173">Это приложение заменено на <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a>; для настройки приложения с помощью Azure AD можно ссылаться на <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">это</a> руководство.</span><span class="sxs-lookup"><span data-stu-id="e0492-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="e0492-174">На классическом портале Azure выберите подтверждение конфигурации единого входа и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0492-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![единого входа Azure AD][10]

7. <span data-ttu-id="e0492-176">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="e0492-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![единого входа Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0492-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0492-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0492-179">Цель этого раздела — создать на классическом портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0492-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Создание пользователя Azure AD][20]

<span data-ttu-id="e0492-181">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e0492-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0492-182">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0492-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="e0492-184">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="e0492-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="e0492-185">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e0492-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0492-187">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="e0492-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="e0492-189">На странице диалогового окна **Тип учетной записи пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e0492-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="e0492-191">а.</span><span class="sxs-lookup"><span data-stu-id="e0492-191">a.</span></span> <span data-ttu-id="e0492-192">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="e0492-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="e0492-193">b.</span><span class="sxs-lookup"><span data-stu-id="e0492-193">b.</span></span> <span data-ttu-id="e0492-194">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e0492-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e0492-195">c.</span><span class="sxs-lookup"><span data-stu-id="e0492-195">c.</span></span> <span data-ttu-id="e0492-196">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0492-196">Click **Next**.</span></span>

6.  <span data-ttu-id="e0492-197">На странице диалогового окна **Профиль пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e0492-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="e0492-199">а.</span><span class="sxs-lookup"><span data-stu-id="e0492-199">a.</span></span> <span data-ttu-id="e0492-200">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e0492-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="e0492-201">b.</span><span class="sxs-lookup"><span data-stu-id="e0492-201">b.</span></span> <span data-ttu-id="e0492-202">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e0492-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="e0492-203">c.</span><span class="sxs-lookup"><span data-stu-id="e0492-203">c.</span></span> <span data-ttu-id="e0492-204">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e0492-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="e0492-205">d.</span><span class="sxs-lookup"><span data-stu-id="e0492-205">d.</span></span> <span data-ttu-id="e0492-206">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="e0492-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="e0492-207">д.</span><span class="sxs-lookup"><span data-stu-id="e0492-207">e.</span></span> <span data-ttu-id="e0492-208">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e0492-208">Click **Next**.</span></span>

7. <span data-ttu-id="e0492-209">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e0492-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="e0492-211">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e0492-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="e0492-213">а.</span><span class="sxs-lookup"><span data-stu-id="e0492-213">a.</span></span> <span data-ttu-id="e0492-214">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="e0492-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="e0492-215">b.</span><span class="sxs-lookup"><span data-stu-id="e0492-215">b.</span></span> <span data-ttu-id="e0492-216">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="e0492-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="e0492-217">Создание тестового пользователя Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="e0492-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="e0492-218">Цель этого раздела — создать в приложении Soonr Workplace пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0492-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="e0492-219">Чтобы создать пользователя на платформе, свяжитесь со службой поддержки Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="e0492-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="e0492-220">Создать запрос в службу поддержки Soonr можно <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">здесь</a>.</span><span class="sxs-lookup"><span data-stu-id="e0492-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0492-221">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0492-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0492-222">Цель этого раздела — разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="e0492-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e0492-224">**Чтобы назначить пользователя Britta Simon приложению Soonr Workplace, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e0492-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="e0492-225">Чтобы открыть представление приложений, на классическом портале Azure в представлении каталога щелкните **Приложения** в меню вверху.</span><span class="sxs-lookup"><span data-stu-id="e0492-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e0492-227">Из списка приложений выберите **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="e0492-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="e0492-229">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e0492-229">In the menu on the top, click **Users**.</span></span>

    ![Назначение пользователя][203] 

1. <span data-ttu-id="e0492-231">В списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e0492-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="e0492-232">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e0492-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Назначение пользователя][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="e0492-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e0492-234">Testing single sign-on</span></span>

<span data-ttu-id="e0492-235">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e0492-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="e0492-236">Щелкнув элемент Soonr Workplace на панели доступа, вы автоматически войдете в приложение Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="e0492-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e0492-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e0492-237">Additional resources</span></span>

* [<span data-ttu-id="e0492-238">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0492-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0492-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e0492-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
