---
title: "Руководство по интеграции Azure Active Directory с Weekdone | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 84aa0069dce55a6623398a99e1cac6bb21bf52f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="dc034-103">Руководство. Интеграция Azure Active Directory с Weekdone</span><span class="sxs-lookup"><span data-stu-id="dc034-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="dc034-104">В этом руководстве описано, как интегрировать Weekdone с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc034-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc034-105">Интеграция Weekdone с Azure AD дает приведенные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="dc034-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc034-106">С помощью Azure AD вы можете контролировать доступ к Weekdone.</span><span class="sxs-lookup"><span data-stu-id="dc034-106">You can control in Azure AD who has access to Weekdone</span></span>
- <span data-ttu-id="dc034-107">Вы можете включить автоматический вход пользователей в Weekdone (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc034-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc034-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dc034-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dc034-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc034-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc034-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc034-110">Prerequisites</span></span>

<span data-ttu-id="dc034-111">Чтобы настроить интеграцию Azure AD с Weekdone, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="dc034-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

- <span data-ttu-id="dc034-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dc034-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc034-113">подписка Weekdone с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dc034-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc034-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="dc034-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc034-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="dc034-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc034-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dc034-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc034-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc034-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc034-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dc034-118">Scenario description</span></span>
<span data-ttu-id="dc034-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dc034-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc034-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="dc034-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc034-121">Добавление Weekdone из коллекции</span><span class="sxs-lookup"><span data-stu-id="dc034-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="dc034-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc034-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="dc034-123">Добавление Weekdone из коллекции</span><span class="sxs-lookup"><span data-stu-id="dc034-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="dc034-124">Чтобы настроить интеграцию Weekdone с Azure AD, необходимо добавить приложение Weekdone из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dc034-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc034-125">**Чтобы добавить Weekdone из коллекции, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="dc034-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc034-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc034-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc034-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc034-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc034-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc034-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dc034-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="dc034-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dc034-133">В поле поиска введите **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="dc034-133">In the search box, type **Weekdone**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="dc034-135">На панели результатов выберите **Weekdone** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="dc034-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc034-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc034-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc034-138">В этом разделе описана настройка и проверка единого входа Azure AD в Weekdone с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc034-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc034-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Weekdone соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc034-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span></span> <span data-ttu-id="dc034-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Weekdone.</span><span class="sxs-lookup"><span data-stu-id="dc034-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="dc034-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Weekdone.</span><span class="sxs-lookup"><span data-stu-id="dc034-141">In Weekdone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dc034-142">Чтобы настроить и проверить единый вход Azure AD в Weekdone, вам потребуется выполнить действия в приведенных ниже стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="dc034-142">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc034-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="dc034-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dc034-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc034-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc034-145">**[Создание тестового пользователя Weekdone](#creating-a-weekdone-test-user)** требуется для того, чтобы в Weekdone существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc034-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc034-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc034-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc034-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dc034-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc034-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc034-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc034-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Weekdone.</span><span class="sxs-lookup"><span data-stu-id="dc034-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="dc034-150">**Чтобы настроить единый вход Azure AD в Weekdone, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="dc034-150">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="dc034-151">На портале Azure на странице интеграции с приложением **Weekdone** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="dc034-151">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dc034-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="dc034-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="dc034-155">Если вы хотите настроить приложение в **режиме, инициируемом IdP**, то в разделе **Домены и URL-адреса приложения Weekdone** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc034-155">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="dc034-157">а.</span><span class="sxs-lookup"><span data-stu-id="dc034-157">a.</span></span> <span data-ttu-id="dc034-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="dc034-158">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="dc034-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc034-159">b.</span></span> <span data-ttu-id="dc034-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://weekdone.com/a/<tenantname>`.</span><span class="sxs-lookup"><span data-stu-id="dc034-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="dc034-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="dc034-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="dc034-162">если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="dc034-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="dc034-164">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="dc034-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="dc034-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="dc034-165">These values are not real.</span></span> <span data-ttu-id="dc034-166">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="dc034-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="dc034-167">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="dc034-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span></span> 

5. <span data-ttu-id="dc034-168">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc034-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="dc034-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dc034-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="dc034-172">В разделе **Конфигурация Weekdone** щелкните **Настроить Weekdone**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dc034-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dc034-173">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="dc034-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="dc034-175">Чтобы настроить единый вход на стороне **Weekdone**, нужно отправить скачанный **XML-файл метаданных, URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="dc034-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="dc034-176">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="dc034-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dc034-177">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="dc034-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc034-178">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dc034-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc034-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc034-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc034-180">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc034-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dc034-182">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dc034-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc034-183">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc034-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc034-185">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="dc034-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc034-187">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc034-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc034-189">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc034-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc034-191">а.</span><span class="sxs-lookup"><span data-stu-id="dc034-191">a.</span></span> <span data-ttu-id="dc034-192">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc034-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc034-193">b.</span><span class="sxs-lookup"><span data-stu-id="dc034-193">b.</span></span> <span data-ttu-id="dc034-194">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc034-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc034-195">c.</span><span class="sxs-lookup"><span data-stu-id="dc034-195">c.</span></span> <span data-ttu-id="dc034-196">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="dc034-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dc034-197">d.</span><span class="sxs-lookup"><span data-stu-id="dc034-197">d.</span></span> <span data-ttu-id="dc034-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dc034-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="dc034-199">Создание тестового пользователя Weekdone</span><span class="sxs-lookup"><span data-stu-id="dc034-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="dc034-200">Цель этого раздела — создать пользователя с именем Britta Simon в Weekdone.</span><span class="sxs-lookup"><span data-stu-id="dc034-200">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="dc034-201">Приложение Weekdone поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dc034-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="dc034-202">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="dc034-202">There is no action item for you in this section.</span></span> <span data-ttu-id="dc034-203">Пользователь будет создан при попытке получить доступ к Weekdone (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="dc034-203">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="dc034-204">Если вам нужно создать пользователя вручную, необходимо обратиться к [группе поддержки клиентов Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="dc034-204">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc034-205">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc034-205">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dc034-206">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Weekdone.</span><span class="sxs-lookup"><span data-stu-id="dc034-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dc034-208">**Чтобы назначить пользователя Britta Simon в Weekdone, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="dc034-208">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="dc034-209">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc034-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dc034-211">В списке приложений выберите **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="dc034-211">In the applications list, select **Weekdone**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="dc034-213">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dc034-213">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dc034-215">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc034-215">Click **Add** button.</span></span> <span data-ttu-id="dc034-216">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dc034-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dc034-218">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dc034-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dc034-219">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dc034-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc034-220">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dc034-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc034-221">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dc034-221">Testing single sign-on</span></span>

<span data-ttu-id="dc034-222">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="dc034-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="dc034-223">Щелкнув элемент Weekdone на панели доступа, вы автоматически войдете в приложение Weekdone.</span><span class="sxs-lookup"><span data-stu-id="dc034-223">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc034-224">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dc034-224">Additional resources</span></span>

* [<span data-ttu-id="dc034-225">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc034-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc034-226">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc034-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

