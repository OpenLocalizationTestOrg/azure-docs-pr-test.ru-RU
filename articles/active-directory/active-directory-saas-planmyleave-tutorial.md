---
title: "Руководство. Интеграция Azure Active Directory с PlanMyLeave | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="096f4-103">Руководство. Интеграция Azure Active Directory с PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="096f4-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="096f4-104">В этом руководстве описано, как интегрировать PlanMyLeave с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="096f4-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="096f4-105">Интеграция PlanMyLeave с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="096f4-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="096f4-106">С помощью Azure AD вы можете контролировать доступ к PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="096f4-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="096f4-107">Вы можете включить автоматический вход пользователей в PlanMyLeave (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="096f4-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="096f4-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="096f4-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="096f4-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="096f4-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="096f4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="096f4-110">Prerequisites</span></span>

<span data-ttu-id="096f4-111">Чтобы настроить интеграцию Azure AD с PlanMyLeave, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="096f4-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="096f4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="096f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="096f4-113">подписка PlanMyLeave с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="096f4-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="096f4-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="096f4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="096f4-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="096f4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="096f4-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="096f4-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="096f4-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="096f4-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="096f4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="096f4-118">Scenario description</span></span>
<span data-ttu-id="096f4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="096f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="096f4-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="096f4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="096f4-121">Добавление PlanMyLeave из коллекции</span><span class="sxs-lookup"><span data-stu-id="096f4-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="096f4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="096f4-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="096f4-123">Добавление PlanMyLeave из коллекции</span><span class="sxs-lookup"><span data-stu-id="096f4-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="096f4-124">Чтобы настроить интеграцию PlanMyLeave с Azure AD, необходимо добавить PlanMyLeave из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="096f4-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="096f4-125">**Чтобы добавить PlanMyLeave из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="096f4-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="096f4-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="096f4-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="096f4-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="096f4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="096f4-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="096f4-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="096f4-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="096f4-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="096f4-133">В поле поиска введите **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="096f4-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="096f4-135">На панели результатов выберите **PlanMyLeave** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="096f4-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="096f4-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="096f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="096f4-138">В этом разделе описана настройка и проверка единого входа Azure AD в PlanMyLeave с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="096f4-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="096f4-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в PlanMyLeave соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="096f4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="096f4-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="096f4-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="096f4-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="096f4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="096f4-142">Чтобы настроить и проверить единый вход Azure AD в PlanMyLeave, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="096f4-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="096f4-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="096f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="096f4-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="096f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="096f4-145">**[Создание тестового пользователя приложения PlanMyLeave](#creating-a-planmyleave-test-user)** требуется для создания в PlanMyLeave пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="096f4-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="096f4-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="096f4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="096f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="096f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="096f4-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="096f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="096f4-149">В данном разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="096f4-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="096f4-150">**Чтобы настроить единый вход Azure AD в PlanMyLeave, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="096f4-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="096f4-151">На портале управления Azure на странице интеграции с приложением **PlanMyLeave** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="096f4-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="096f4-153">На странице диалогового окна **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="096f4-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="096f4-155">В разделе **Домены и URL-адреса приложения PlanMyLeave** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="096f4-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="096f4-157">а.</span><span class="sxs-lookup"><span data-stu-id="096f4-157">a.</span></span> <span data-ttu-id="096f4-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company-name>.planmyleave.com/Login.aspx`.</span><span class="sxs-lookup"><span data-stu-id="096f4-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="096f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="096f4-159">b.</span></span> <span data-ttu-id="096f4-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="096f4-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="096f4-161">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="096f4-161">Please note that these are not the real values.</span></span> <span data-ttu-id="096f4-162">Необходимо заменить эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="096f4-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="096f4-163">Чтобы получить эти значения, обратитесь в [группе поддержки PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="096f4-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="096f4-164">В разделе **Сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="096f4-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="096f4-166">В диалоговом окне **Создание нового сертификата** щелкните значок календаря и выберите **дату окончания срока действия**.</span><span class="sxs-lookup"><span data-stu-id="096f4-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="096f4-167">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="096f4-167">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="096f4-169">В разделе **Сертификат подписи SAML** выберите **Make new certificate active** (Сделать новый сертификат активным) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="096f4-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="096f4-171">Во всплывающем окне **Rollover certificate** (Сертификат восстановления) нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="096f4-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="096f4-173">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="096f4-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="096f4-175">В разделе **PlanMyLeave Configuration** (Конфигурация Fuse) щелкните **Configure PlanMyLeave** (Настроить Fuse), чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="096f4-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="096f4-178">В другом окне веб-браузера войдите в свой клиент PlanMyLeave в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="096f4-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="096f4-179">Перейдите в окно **System Setup** (Настройка системы).</span><span class="sxs-lookup"><span data-stu-id="096f4-179">Go to **System Setup**.</span></span> <span data-ttu-id="096f4-180">Затем в разделе **Security Management** (Управление безопасностью) щелкните **Company SAML settings** (Параметры SAML компании).</span><span class="sxs-lookup"><span data-stu-id="096f4-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="096f4-182">В разделе **SAML Settings** (Параметры SAML) щелкните значок редактора.</span><span class="sxs-lookup"><span data-stu-id="096f4-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="096f4-184">В разделе **Update SAML Settings** (Изменение параметров SAML) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="096f4-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="096f4-186">а.</span><span class="sxs-lookup"><span data-stu-id="096f4-186">a.</span></span>  <span data-ttu-id="096f4-187">В текстовом поле **URL-адрес для входа** введите значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML) из окна настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="096f4-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="096f4-188">b.</span><span class="sxs-lookup"><span data-stu-id="096f4-188">b.</span></span>  <span data-ttu-id="096f4-189">Откройте скачанный файл сертификата в Блокноте, скопируйте его содержимое между метками ---Begin Certificate--- и ---End certificate---- в буфер обмена, а затем вставьте его в текстовое поле **Certificate** (Сертификат).</span><span class="sxs-lookup"><span data-stu-id="096f4-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="096f4-190">c.</span><span class="sxs-lookup"><span data-stu-id="096f4-190">c.</span></span> <span data-ttu-id="096f4-191">Для параметра "**Is Enable**" (Включено) установите значение "**Yes**" (Да).</span><span class="sxs-lookup"><span data-stu-id="096f4-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="096f4-192">d.</span><span class="sxs-lookup"><span data-stu-id="096f4-192">d.</span></span> <span data-ttu-id="096f4-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="096f4-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="096f4-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="096f4-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="096f4-195">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="096f4-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="096f4-197">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="096f4-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="096f4-198">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="096f4-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="096f4-200">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="096f4-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="096f4-202">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="096f4-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="096f4-204">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="096f4-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="096f4-206">а.</span><span class="sxs-lookup"><span data-stu-id="096f4-206">a.</span></span> <span data-ttu-id="096f4-207">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="096f4-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="096f4-208">b.</span><span class="sxs-lookup"><span data-stu-id="096f4-208">b.</span></span> <span data-ttu-id="096f4-209">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="096f4-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="096f4-210">c.</span><span class="sxs-lookup"><span data-stu-id="096f4-210">c.</span></span> <span data-ttu-id="096f4-211">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="096f4-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="096f4-212">d.</span><span class="sxs-lookup"><span data-stu-id="096f4-212">d.</span></span> <span data-ttu-id="096f4-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="096f4-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="096f4-214">Создание тестового пользователя PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="096f4-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="096f4-215">Цель этого раздела — создать пользователя с именем Britta Simon в PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="096f4-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="096f4-216">Приложение PlanMyLeave поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="096f4-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="096f4-217">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="096f4-217">There is no action item for you in this section.</span></span> <span data-ttu-id="096f4-218">Пользователь будет создан при попытке получить доступ к PlanMyLeave (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="096f4-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="096f4-219">Если нужно создать пользователя вручную, обратитесь к [группе поддержки PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="096f4-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="096f4-220">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="096f4-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="096f4-221">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="096f4-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="096f4-223">**Чтобы назначить пользователя Britta Simon в PlanMyLeave, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="096f4-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="096f4-224">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="096f4-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="096f4-226">В списке приложений выберите **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="096f4-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="096f4-228">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="096f4-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="096f4-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="096f4-230">Click **Add** button.</span></span> <span data-ttu-id="096f4-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="096f4-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="096f4-233">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="096f4-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="096f4-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="096f4-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="096f4-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="096f4-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="096f4-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="096f4-236">Testing single sign-on</span></span>

<span data-ttu-id="096f4-237">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="096f4-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="096f4-238">Щелкнув элемент PlanMyLeave на панели доступа, вы автоматически войдете в приложение PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="096f4-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="096f4-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="096f4-239">Additional resources</span></span>

* [<span data-ttu-id="096f4-240">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="096f4-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="096f4-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="096f4-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png