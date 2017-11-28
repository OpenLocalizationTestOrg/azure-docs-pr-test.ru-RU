---
title: "Руководство по интеграции Azure Active Directory с RFPIO | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="2026b-103">Руководство по интеграции Azure Active Directory с RFPIO</span><span class="sxs-lookup"><span data-stu-id="2026b-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="2026b-104">В этом руководстве описано, как интегрировать RFPIO с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2026b-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2026b-105">Интеграция Azure AD с приложением RFPIO обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="2026b-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2026b-106">С помощью Azure AD вы можете контролировать доступ к RFPIO.</span><span class="sxs-lookup"><span data-stu-id="2026b-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="2026b-107">Вы можете включить автоматический вход пользователей в RFPIO (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2026b-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2026b-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2026b-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="2026b-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2026b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2026b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2026b-110">Prerequisites</span></span>

<span data-ttu-id="2026b-111">Чтобы настроить интеграцию Azure AD с RFPIO, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="2026b-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="2026b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2026b-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="2026b-113">подписка RFPIO с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="2026b-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="2026b-114">Мы не рекомендуем использовать рабочую среду для выполнения действий в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="2026b-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="2026b-115">При проверке действий в этом руководстве соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="2026b-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="2026b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="2026b-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="2026b-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2026b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2026b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2026b-118">Scenario description</span></span>
<span data-ttu-id="2026b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2026b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2026b-120">Сценарий, описанный в этом руководстве, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="2026b-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2026b-121">Добавление RFPIO из коллекции.</span><span class="sxs-lookup"><span data-stu-id="2026b-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="2026b-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2026b-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="2026b-123">Добавление RFPIO из коллекции</span><span class="sxs-lookup"><span data-stu-id="2026b-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="2026b-124">Чтобы настроить интеграцию RFPIO с Azure AD, необходимо добавить RFPIO из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2026b-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="2026b-125">Добавление RFPIO из коллекции</span><span class="sxs-lookup"><span data-stu-id="2026b-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="2026b-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2026b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2026b-128">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2026b-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="2026b-130">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="2026b-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="2026b-132">В поле поиска введите **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="2026b-132">In the search box, type **RFPIO**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="2026b-134">На панели результатов выберите **RFPIO** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="2026b-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2026b-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2026b-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2026b-137">В этом разделе описана настройка и проверка единого входа Azure AD в приложение RFPIO с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2026b-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2026b-138">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователем в RFPIO соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2026b-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="2026b-139">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в RFPIO.</span><span class="sxs-lookup"><span data-stu-id="2026b-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="2026b-140">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в RFPIO.</span><span class="sxs-lookup"><span data-stu-id="2026b-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2026b-141">Чтобы настроить и проверить единый вход Azure AD в RFPIO, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="2026b-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2026b-142">**[Настройка единого входа Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="2026b-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2026b-143">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2026b-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2026b-144">**[Создание тестового пользователя RFPIO](#creating-a-rfpio-test-user)** требуется для создания в RFPIO пользователя Britta Simon, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2026b-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2026b-145">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2026b-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2026b-146">**[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2026b-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2026b-147">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="2026b-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2026b-148">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении RFPIO.</span><span class="sxs-lookup"><span data-stu-id="2026b-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="2026b-149">**Чтобы настроить единый вход Azure AD в RFPIO, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2026b-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="2026b-150">На портале Azure на странице интеграции с приложением **RFPIO** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="2026b-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="2026b-152">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="2026b-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="2026b-154">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения RFPIO** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2026b-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="2026b-156">а.</span><span class="sxs-lookup"><span data-stu-id="2026b-156">a.</span></span> <span data-ttu-id="2026b-157">В текстовом поле **Идентификатор** введите URL-адрес: `https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="2026b-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="2026b-159">b.</span><span class="sxs-lookup"><span data-stu-id="2026b-159">b.</span></span> <span data-ttu-id="2026b-160">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="2026b-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="2026b-161">c.</span><span class="sxs-lookup"><span data-stu-id="2026b-161">c.</span></span> <span data-ttu-id="2026b-162">В текстовом поле **Состояние ретранслятора** введите строковое значение.</span><span class="sxs-lookup"><span data-stu-id="2026b-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="2026b-163">Чтобы получить это значение, обратитесь в [службу поддержки RFPIO](https://www.rfpio.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="2026b-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="2026b-164">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="2026b-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2026b-165">если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="2026b-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="2026b-167">В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="2026b-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="2026b-168">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2026b-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="2026b-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2026b-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2026b-172">В другом окне веб-браузера войдите на веб-сайт **RFPIO** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="2026b-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="2026b-173">Щелкните раскрывающийся список в нижнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="2026b-173">Click on the bottom left corner dropdown.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="2026b-175">Щелкните **Organization Settings** (Параметры организации).</span><span class="sxs-lookup"><span data-stu-id="2026b-175">Click on the **Organization Settings**.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="2026b-177">Щелкните **FEATURES & INTEGRATION** (Функции и интеграция).</span><span class="sxs-lookup"><span data-stu-id="2026b-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="2026b-179">В окне **SAML SSO Configuration** (Конфигурация единого входа SAML) щелкните **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="2026b-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="2026b-181">В этом разделе выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2026b-181">In this Section perform following actions:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="2026b-183">а.</span><span class="sxs-lookup"><span data-stu-id="2026b-183">a.</span></span> <span data-ttu-id="2026b-184">Скопируйте содержимое **скачанного XML-файла с метаданными** и вставьте его в текстовое поле **Identity configuration** (Конфигурация удостоверений).</span><span class="sxs-lookup"><span data-stu-id="2026b-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="2026b-185">Чтобы скопировать содержимое скачанного **XML-файла с метаданными**, используйте **Notepad++** или соответствующий **редактор XML**.</span><span class="sxs-lookup"><span data-stu-id="2026b-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="2026b-186">b.</span><span class="sxs-lookup"><span data-stu-id="2026b-186">b.</span></span> <span data-ttu-id="2026b-187">Щелкните **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="2026b-187">Click **Validate**.</span></span>

    <span data-ttu-id="2026b-188">c.</span><span class="sxs-lookup"><span data-stu-id="2026b-188">c.</span></span> <span data-ttu-id="2026b-189">После нажатия кнопки **Validate** (Проверить) установите переключатель **SAML(Enabled)** (SAML (Включено)) в положение "Вкл.".</span><span class="sxs-lookup"><span data-stu-id="2026b-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="2026b-190">г)</span><span class="sxs-lookup"><span data-stu-id="2026b-190">d.</span></span> <span data-ttu-id="2026b-191">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="2026b-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="2026b-192">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="2026b-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2026b-193">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="2026b-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2026b-194">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="2026b-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2026b-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2026b-195">Create an Azure AD test user</span></span>
<span data-ttu-id="2026b-196">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2026b-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="2026b-198">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="2026b-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2026b-199">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2026b-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2026b-201">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="2026b-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2026b-203">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2026b-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2026b-205">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2026b-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2026b-207">а.</span><span class="sxs-lookup"><span data-stu-id="2026b-207">a.</span></span> <span data-ttu-id="2026b-208">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2026b-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2026b-209">b.</span><span class="sxs-lookup"><span data-stu-id="2026b-209">b.</span></span> <span data-ttu-id="2026b-210">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2026b-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2026b-211">c.</span><span class="sxs-lookup"><span data-stu-id="2026b-211">c.</span></span> <span data-ttu-id="2026b-212">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="2026b-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2026b-213">d.</span><span class="sxs-lookup"><span data-stu-id="2026b-213">d.</span></span> <span data-ttu-id="2026b-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2026b-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="2026b-215">Создание тестового пользователя RFPIO</span><span class="sxs-lookup"><span data-stu-id="2026b-215">Create a RFPIO test user</span></span>

<span data-ttu-id="2026b-216">Чтобы пользователи Azure AD могли выполнять вход в RFPIO, они должны быть подготовлены в RFPIO.</span><span class="sxs-lookup"><span data-stu-id="2026b-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="2026b-217">В случае с RFPIO подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="2026b-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="2026b-218">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2026b-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2026b-219">Войдите на веб-сайт RFPIO компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="2026b-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="2026b-220">Щелкните раскрывающийся список в нижнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="2026b-220">Click on the bottom left corner dropdown.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="2026b-222">Щелкните **Organization Settings** (Параметры организации).</span><span class="sxs-lookup"><span data-stu-id="2026b-222">Click on the **Organization Settings**.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="2026b-224">Щелкните **TEAM MEMBERS** (Участники команды).</span><span class="sxs-lookup"><span data-stu-id="2026b-224">Click **TEAM MEMBERS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="2026b-226">Щелкните **ADD MEMBERS** (Добавить участников).</span><span class="sxs-lookup"><span data-stu-id="2026b-226">Click on **ADD MEMBERS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="2026b-228">В разделе **Add New Members** (Добавление новых участников)</span><span class="sxs-lookup"><span data-stu-id="2026b-228">In the **Add New Members** section.</span></span> <span data-ttu-id="2026b-229">выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2026b-229">Perform following actions:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="2026b-231">а.</span><span class="sxs-lookup"><span data-stu-id="2026b-231">a.</span></span> <span data-ttu-id="2026b-232">Введите **адрес электронной почты** в текстовом поле **Enter one email per line** (Введите один адрес электронной почты в каждой строке).</span><span class="sxs-lookup"><span data-stu-id="2026b-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="2026b-233">b.</span><span class="sxs-lookup"><span data-stu-id="2026b-233">b.</span></span> <span data-ttu-id="2026b-234">Выберите **роль** в соответствии с требованиями.</span><span class="sxs-lookup"><span data-stu-id="2026b-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="2026b-235">c.</span><span class="sxs-lookup"><span data-stu-id="2026b-235">c.</span></span> <span data-ttu-id="2026b-236">Щелкните **ADD MEMBERS** (Добавить участников).</span><span class="sxs-lookup"><span data-stu-id="2026b-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="2026b-237">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2026b-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2026b-238">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2026b-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="2026b-239">В этом разделе описано, как предоставить пользователю Britta Simon доступ к RFPIO, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="2026b-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="2026b-241">**Чтобы назначить пользователя Britta Simon в RFPIO, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2026b-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="2026b-242">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2026b-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2026b-244">В списке приложений выберите **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="2026b-244">In the applications list, select **RFPIO**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="2026b-246">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2026b-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="2026b-248">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2026b-248">Click **Add** button.</span></span> <span data-ttu-id="2026b-249">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2026b-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="2026b-251">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2026b-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2026b-252">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2026b-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2026b-253">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="2026b-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2026b-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2026b-254">Test single sign-on</span></span>

<span data-ttu-id="2026b-255">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2026b-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="2026b-256">Щелкнув элемент RFPIO на панели доступа, вы автоматически войдете в приложение RFPIO.</span><span class="sxs-lookup"><span data-stu-id="2026b-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="2026b-257">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2026b-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2026b-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2026b-258">Additional resources</span></span>

* [<span data-ttu-id="2026b-259">Список руководств по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2026b-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2026b-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2026b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

