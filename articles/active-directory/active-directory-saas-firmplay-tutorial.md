---
title: "Руководство. Интеграция Azure Active Directory с FirmPlay — Employee Advocacy for Recruiting | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в FirmPlay — Employee Advocacy for Recruiting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="268a5-103">Руководство. Интеграция Azure Active Directory с FirmPlay — Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="268a5-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="268a5-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением FirmPlay — Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="268a5-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="268a5-105">Интеграция Azure AD с приложением FirmPlay обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="268a5-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="268a5-106">Вы можете управлять доступом к FirmPlay — Employee Advocacy for Recruiting с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="268a5-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="268a5-107">Вы можете включить автоматический вход пользователей в FirmPlay — Employee Advocacy for Recruiting (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="268a5-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="268a5-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="268a5-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="268a5-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="268a5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="268a5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="268a5-110">Prerequisites</span></span>

<span data-ttu-id="268a5-111">Чтобы настроить интеграцию Azure AD с FirmPlay — Employee Advocacy for Recruiting, вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="268a5-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="268a5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="268a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="268a5-113">подписка на FirmPlay — Employee Advocacy for Recruiting с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="268a5-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="268a5-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="268a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="268a5-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="268a5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="268a5-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="268a5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="268a5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="268a5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="268a5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="268a5-118">Scenario description</span></span>
<span data-ttu-id="268a5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="268a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="268a5-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="268a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="268a5-121">Добавление FirmPlay — Employee Advocacy for Recruiting из коллекции</span><span class="sxs-lookup"><span data-stu-id="268a5-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="268a5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="268a5-123">Добавление FirmPlay — Employee Advocacy for Recruiting из коллекции</span><span class="sxs-lookup"><span data-stu-id="268a5-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="268a5-124">Чтобы настроить интеграцию FirmPlay — Employee Advocacy for Recruiting с Azure AD, необходимо добавить приложение FirmPlay из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="268a5-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="268a5-125">**Чтобы добавить FirmPlay — Employee Advocacy for Recruiting из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="268a5-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="268a5-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="268a5-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="268a5-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="268a5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="268a5-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="268a5-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="268a5-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="268a5-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="268a5-133">В поле поиска введите **FirmPlay — Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="268a5-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="268a5-135">На панели результатов выберите **FirmPlay — Employee Advocacy for Recruiting** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="268a5-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="268a5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="268a5-138">В этом разделе описана настройка и проверка единого входа Azure AD в FirmPlay — Employee Advocacy for Recruiting с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="268a5-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="268a5-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в FirmPlay — Employee Advocacy for Recruiting соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="268a5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="268a5-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в FirmPlay — Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="268a5-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="268a5-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в FirmPlay — Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="268a5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="268a5-142">Чтобы настроить и проверить единый вход Azure AD в FirmPlay, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="268a5-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="268a5-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="268a5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="268a5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="268a5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="268a5-145">**[Создание тестового пользователя FirmPlay — Employee Advocacy for Recruiting](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** требуется для дублирования пользователя Britta Simon в FirmPlay, который связан с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="268a5-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="268a5-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="268a5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="268a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="268a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="268a5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="268a5-149">В этом разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении FirmPlay — Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="268a5-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="268a5-150">**Чтобы настроить единый вход Azure AD в FirmPlay — Employee Advocacy for Recruiting, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="268a5-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="268a5-151">На портале управления Azure на странице интеграции с приложением **FirmPlay — Employee Advocacy for Recruiting** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="268a5-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="268a5-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="268a5-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="268a5-155">В текстовом поле **URL-адрес для входа** раздела **Домены и URL-адреса приложения FirmPlay — Employee Advocacy for Recruiting** введите URL-адрес в следующем формате: `https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="268a5-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="268a5-157">Обратите внимание, что это значение используется только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="268a5-157">Please note that this is not the real value.</span></span> <span data-ttu-id="268a5-158">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="268a5-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="268a5-159">Чтобы получить это значение, обратитесь в [службу поддержки FirmPlay — Employee Advocacy for Recruiting](mailto:engineering@firmplay.com).</span><span class="sxs-lookup"><span data-stu-id="268a5-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="268a5-160">В разделе **Сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="268a5-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="268a5-162">В диалоговом окне **Создание нового сертификата** щелкните значок календаря и выберите **дату окончания срока действия**.</span><span class="sxs-lookup"><span data-stu-id="268a5-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="268a5-163">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="268a5-163">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="268a5-165">В разделе **Сертификат подписи SAML** выберите **Make new certificate active** (Сделать новый сертификат активным) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="268a5-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="268a5-167">Во всплывающем окне **Rollover certificate** (Сертификат восстановления) нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="268a5-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="268a5-169">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="268a5-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="268a5-171">В разделе **конфигурации FirmPlay — Employee Advocacy for Recruiting** щелкните **Настроить FirmPlay — Employee Advocacy for Recruiting**, чтобы открыть диалоговое окно **Настройка входа**.</span><span class="sxs-lookup"><span data-stu-id="268a5-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="268a5-174">Для настройки единого входа для своего приложения обратитесь в [службу поддержки FirmPlay — Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) и укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="268a5-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="268a5-175">• скачанный **файл сертификата**;</span><span class="sxs-lookup"><span data-stu-id="268a5-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="268a5-176">• **URL-адрес службы единого входа SAML**;</span><span class="sxs-lookup"><span data-stu-id="268a5-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="268a5-177">• **идентификатор сущности SAML**;</span><span class="sxs-lookup"><span data-stu-id="268a5-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="268a5-178">• **URL-адрес выхода**.</span><span class="sxs-lookup"><span data-stu-id="268a5-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="268a5-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="268a5-180">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="268a5-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="268a5-182">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="268a5-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="268a5-183">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="268a5-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="268a5-185">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="268a5-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="268a5-187">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="268a5-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="268a5-189">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="268a5-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="268a5-191">а.</span><span class="sxs-lookup"><span data-stu-id="268a5-191">a.</span></span> <span data-ttu-id="268a5-192">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="268a5-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="268a5-193">b.</span><span class="sxs-lookup"><span data-stu-id="268a5-193">b.</span></span> <span data-ttu-id="268a5-194">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="268a5-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="268a5-195">c.</span><span class="sxs-lookup"><span data-stu-id="268a5-195">c.</span></span> <span data-ttu-id="268a5-196">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="268a5-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="268a5-197">d.</span><span class="sxs-lookup"><span data-stu-id="268a5-197">d.</span></span> <span data-ttu-id="268a5-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="268a5-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="268a5-199">Создание тестового пользователя FirmPlay — Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="268a5-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="268a5-200">В этом разделе вы создадите тестового пользователя FirmPlay — Employee Advocacy for Recruiting с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="268a5-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="268a5-201">Обратитесь в [службу поддержки FirmPlay — Employee Advocacy for Recruiting](mailto:engineering@firmplay.com), чтобы добавить пользователей в платформу FirmPlay — Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="268a5-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="268a5-202">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="268a5-203">В этом разделе объясняется, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к FirmPlay — Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="268a5-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="268a5-205">**Чтобы назначить пользователя Britta Simon приложению FirmPlay — Employee Advocacy for Recruiting, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="268a5-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="268a5-206">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="268a5-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="268a5-208">В списке приложений выберите **FirmPlay — Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="268a5-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="268a5-210">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="268a5-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="268a5-212">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="268a5-212">Click **Add** button.</span></span> <span data-ttu-id="268a5-213">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="268a5-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="268a5-215">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="268a5-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="268a5-216">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="268a5-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="268a5-217">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="268a5-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="268a5-218">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="268a5-218">Testing single sign-on</span></span>

<span data-ttu-id="268a5-219">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="268a5-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="268a5-220">Если вы щелкнете плитку FirmPlay — Employee Advocacy for Recruiting на панели доступа, вы автоматически войдете в приложение FirmPlay — Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="268a5-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="268a5-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="268a5-221">Additional resources</span></span>

* [<span data-ttu-id="268a5-222">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="268a5-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="268a5-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="268a5-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png