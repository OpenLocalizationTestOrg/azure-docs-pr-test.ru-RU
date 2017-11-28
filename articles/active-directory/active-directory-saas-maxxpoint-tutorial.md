---
title: "Руководство. Интеграция Azure Active Directory с MaxxPoint | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в MaxxPoint"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 8a7481b71df5ca407dbed5da3d3cc26991504c82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="d021f-103">Руководство. Интеграция Azure Active Directory с MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d021f-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="d021f-104">В этом руководстве описано, как интегрировать MaxxPoint с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d021f-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d021f-105">Интеграция Azure AD с приложением MaxxPoint предоставляет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d021f-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d021f-106">С помощью Azure AD вы можете контролировать доступ к MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d021f-106">You can control in Azure AD who has access to MaxxPoint</span></span>
- <span data-ttu-id="d021f-107">Вы можете включить автоматический вход пользователей в MaxxPoint (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d021f-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d021f-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d021f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d021f-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d021f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d021f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d021f-110">Prerequisites</span></span>

<span data-ttu-id="d021f-111">Чтобы настроить интеграцию Azure AD с MaxxPoint, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d021f-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span></span>

- <span data-ttu-id="d021f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d021f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d021f-113">подписка MaxxPoint с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d021f-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d021f-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d021f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d021f-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="d021f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d021f-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="d021f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d021f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d021f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d021f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d021f-118">Scenario description</span></span>
<span data-ttu-id="d021f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d021f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d021f-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="d021f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d021f-121">Добавление MaxxPoint из коллекции</span><span class="sxs-lookup"><span data-stu-id="d021f-121">Adding MaxxPoint from the gallery</span></span>
2. <span data-ttu-id="d021f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d021f-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-the-gallery"></a><span data-ttu-id="d021f-123">Добавление MaxxPoint из коллекции</span><span class="sxs-lookup"><span data-stu-id="d021f-123">Adding MaxxPoint from the gallery</span></span>
<span data-ttu-id="d021f-124">Чтобы настроить интеграцию MaxxPoint с Azure AD, необходимо добавить MaxxPoint из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d021f-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d021f-125">**Чтобы добавить MaxxPoint из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d021f-125">**To add MaxxPoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d021f-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d021f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d021f-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d021f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d021f-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d021f-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d021f-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="d021f-131">Click **New application** button on the top of dialog to add new application.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d021f-133">В поле поиска введите **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="d021f-133">In the search box, type **MaxxPoint**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="d021f-135">На панели результатов выберите **MaxxPoint** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="d021f-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d021f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d021f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d021f-138">В этом разделе описана настройка и проверка единого входа Azure AD в MaxxPoint с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d021f-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d021f-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в MaxxPoint соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d021f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span></span> <span data-ttu-id="d021f-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d021f-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span></span>

<span data-ttu-id="d021f-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d021f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span></span>

<span data-ttu-id="d021f-142">Чтобы настроить и проверить единый вход Azure AD в MaxxPoint, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="d021f-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d021f-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d021f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d021f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d021f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d021f-145">**[Создание тестового пользователя MaxxPoint](#creating-a-maxxpoint-test-user)** требуется для создания в MaxxPoint пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d021f-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d021f-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d021f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d021f-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d021f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d021f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d021f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d021f-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d021f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="d021f-150">**Чтобы настроить единый вход Azure AD в MaxxPoint, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d021f-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="d021f-151">На портале Azure на странице интеграции с приложением **MaxxPoint** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d021f-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d021f-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="d021f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="d021f-155">В разделе **Домены и URL-адреса приложения MaxxPoint** выполнять какие-либо действия не требуется, если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="d021f-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="d021f-157">В разделе **Домены и URL-адреса приложения MaxxPoint** выполните следующие действия, если вы хотите настроить приложение в **режиме, инициированном поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="d021f-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="d021f-159">а.</span><span class="sxs-lookup"><span data-stu-id="d021f-159">a.</span></span> <span data-ttu-id="d021f-160">Выберите параметр **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="d021f-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="d021f-161">b.</span><span class="sxs-lookup"><span data-stu-id="d021f-161">b.</span></span> <span data-ttu-id="d021f-162">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`.</span><span class="sxs-lookup"><span data-stu-id="d021f-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d021f-163">Обратите внимание, что это значение используется только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d021f-163">Please note that this is not the real value.</span></span> <span data-ttu-id="d021f-164">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="d021f-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="d021f-165">Чтобы получить это значение, позвоните в службу поддержки MaxxPoint по номеру **888-728-0950**.</span><span class="sxs-lookup"><span data-stu-id="d021f-165">Call MaxxPoint team on **888-728-0950** to get this value.</span></span>

5. <span data-ttu-id="d021f-166">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d021f-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="d021f-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d021f-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d021f-170">Чтобы настроить единый вход для приложения, позвоните в службу поддержки MaxxPoint по номеру **888-728-0950**. Вы получите дальнейшие указания по тому, как предоставить скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="d021f-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="d021f-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d021f-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d021f-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d021f-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d021f-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d021f-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d021f-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d021f-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="d021f-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d021f-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d021f-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d021f-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d021f-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d021f-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d021f-180">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="d021f-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d021f-182">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="d021f-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d021f-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d021f-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d021f-186">а.</span><span class="sxs-lookup"><span data-stu-id="d021f-186">a.</span></span> <span data-ttu-id="d021f-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d021f-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d021f-188">b.</span><span class="sxs-lookup"><span data-stu-id="d021f-188">b.</span></span> <span data-ttu-id="d021f-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d021f-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d021f-190">c.</span><span class="sxs-lookup"><span data-stu-id="d021f-190">c.</span></span> <span data-ttu-id="d021f-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="d021f-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d021f-192">d.</span><span class="sxs-lookup"><span data-stu-id="d021f-192">d.</span></span> <span data-ttu-id="d021f-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d021f-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="d021f-194">Создание тестового пользователя MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d021f-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="d021f-195">В этом разделе описано, как создать пользователя Britta Simon в приложении MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d021f-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="d021f-196">Позвоните в службу поддержки MaxxPoint по номеру **888-728-0950**, чтобы добавить пользователей в приложение MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d021f-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d021f-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d021f-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d021f-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d021f-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d021f-200">**Чтобы назначить пользователя Britta Simon в MaxxPoint, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d021f-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="d021f-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d021f-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d021f-203">В списке приложений выберите **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="d021f-203">In the applications list, select **MaxxPoint**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="d021f-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d021f-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d021f-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d021f-207">Click **Add** button.</span></span> <span data-ttu-id="d021f-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d021f-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d021f-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d021f-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d021f-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d021f-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d021f-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d021f-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d021f-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d021f-213">Testing single sign-on</span></span>

<span data-ttu-id="d021f-214">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d021f-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d021f-215">Щелкнув элемент MaxxPoint на панели доступа, вы автоматически войдете в приложение MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d021f-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d021f-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d021f-216">Additional resources</span></span>

* [<span data-ttu-id="d021f-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d021f-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d021f-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d021f-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png