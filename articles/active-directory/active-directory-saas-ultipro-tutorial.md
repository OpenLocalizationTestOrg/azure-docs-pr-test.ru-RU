---
title: "Руководство. Интеграция Azure Active Directory с UltiPro | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и UltiPro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: ab60bda1be7101d5bd0c51f5499a820db40375bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="f51e1-103">Руководство. Интеграция Azure Active Directory с UltiPro</span><span class="sxs-lookup"><span data-stu-id="f51e1-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="f51e1-104">В этом руководстве описано, как интегрировать UltiPro с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f51e1-104">In this tutorial, you learn how to integrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f51e1-105">Интеграция Azure AD с приложением UltiPro обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="f51e1-105">Integrating UltiPro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f51e1-106">С помощью Azure AD вы можете контролировать доступ к приложению UltiPro.</span><span class="sxs-lookup"><span data-stu-id="f51e1-106">You can control in Azure AD who has access to UltiPro</span></span>
- <span data-ttu-id="f51e1-107">Вы можете включить автоматический вход пользователей в UltiPro (единый вход) с использованием их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f51e1-107">You can enable your users to automatically get signed-on to UltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f51e1-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f51e1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f51e1-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f51e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f51e1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f51e1-110">Prerequisites</span></span>

<span data-ttu-id="f51e1-111">Чтобы настроить интеграцию Azure AD с UltiPro, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f51e1-111">To configure Azure AD integration with UltiPro, you need the following items:</span></span>

- <span data-ttu-id="f51e1-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f51e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f51e1-113">подписка UltiPro с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f51e1-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f51e1-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f51e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f51e1-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="f51e1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f51e1-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f51e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f51e1-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f51e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f51e1-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f51e1-118">Scenario description</span></span>
<span data-ttu-id="f51e1-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f51e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f51e1-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="f51e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f51e1-121">Добавление UltiPro из коллекции</span><span class="sxs-lookup"><span data-stu-id="f51e1-121">Adding UltiPro from the gallery</span></span>
2. <span data-ttu-id="f51e1-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f51e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-the-gallery"></a><span data-ttu-id="f51e1-123">Добавление UltiPro из коллекции</span><span class="sxs-lookup"><span data-stu-id="f51e1-123">Adding UltiPro from the gallery</span></span>
<span data-ttu-id="f51e1-124">Чтобы настроить интеграцию UltiPro с Azure AD, необходимо добавить UltiPro из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f51e1-124">To configure the integration of UltiPro into Azure AD, you need to add UltiPro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f51e1-125">**Чтобы добавить UltiPro из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f51e1-125">**To add UltiPro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f51e1-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f51e1-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f51e1-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f51e1-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f51e1-133">В поле поиска введите **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-133">In the search box, type **UltiPro**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="f51e1-135">На панели результатов выберите **UltiPro**, а затем нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="f51e1-135">In the results panel, select **UltiPro**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f51e1-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f51e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f51e1-138">В этом разделе описана настройка и проверка единого входа Azure AD в UltiPro с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f51e1-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f51e1-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в UltiPro соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f51e1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UltiPro is to a user in Azure AD.</span></span> <span data-ttu-id="f51e1-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в UltiPro.</span><span class="sxs-lookup"><span data-stu-id="f51e1-140">In other words, a link relationship between an Azure AD user and the related user in UltiPro needs to be established.</span></span>

<span data-ttu-id="f51e1-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в UltiPro.</span><span class="sxs-lookup"><span data-stu-id="f51e1-141">In UltiPro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f51e1-142">Чтобы настроить и проверить единый вход Azure AD в UltiPro, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="f51e1-142">To configure and test Azure AD single sign-on with UltiPro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f51e1-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="f51e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f51e1-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f51e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f51e1-145">**[Создание тестового пользователя UltiPro](#creating-a-ultipro-test-user)** требуется для того, чтобы в UltiPro существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f51e1-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - to have a counterpart of Britta Simon in UltiPro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f51e1-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f51e1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f51e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f51e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f51e1-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f51e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f51e1-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении UltiPro.</span><span class="sxs-lookup"><span data-stu-id="f51e1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="f51e1-150">**Чтобы настроить единый вход Azure AD в UltiPro, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f51e1-150">**To configure Azure AD single sign-on with UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="f51e1-151">На портале Azure на странице интеграции с приложением **UltiPro** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-151">In the Azure portal, on the **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f51e1-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="f51e1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="f51e1-155">В разделе **Домены и URL-адреса приложения UltiPro** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f51e1-155">On the **UltiPro Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="f51e1-157">а.</span><span class="sxs-lookup"><span data-stu-id="f51e1-157">a.</span></span> <span data-ttu-id="f51e1-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="f51e1-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="f51e1-159">b.</span><span class="sxs-lookup"><span data-stu-id="f51e1-159">b.</span></span> <span data-ttu-id="f51e1-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="f51e1-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="f51e1-161">c.</span><span class="sxs-lookup"><span data-stu-id="f51e1-161">c.</span></span> <span data-ttu-id="f51e1-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="f51e1-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="f51e1-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f51e1-163">These values are not real.</span></span> <span data-ttu-id="f51e1-164">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="f51e1-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f51e1-165">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов UltiPro](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="f51e1-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) to get these values.</span></span> 

5. <span data-ttu-id="f51e1-166">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f51e1-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="f51e1-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f51e1-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="f51e1-170">В разделе **Конфигурация UltiPro** щелкните **Настроить UltiPro**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-170">On the **UltiPro Configuration** section, click **Configure UltiPro** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f51e1-171">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="f51e1-173">Чтобы настроить единый вход на стороне **UltiPro**, нужно отправить скачанный **сертификат в кодировке Base64, URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки UltiPro](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="f51e1-173">To configure single sign-on on **UltiPro** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="f51e1-174">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="f51e1-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f51e1-175">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="f51e1-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f51e1-176">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f51e1-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f51e1-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f51e1-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="f51e1-178">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f51e1-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f51e1-180">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f51e1-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f51e1-181">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f51e1-183">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f51e1-185">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f51e1-187">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f51e1-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f51e1-189">а.</span><span class="sxs-lookup"><span data-stu-id="f51e1-189">a.</span></span> <span data-ttu-id="f51e1-190">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f51e1-191">b.</span><span class="sxs-lookup"><span data-stu-id="f51e1-191">b.</span></span> <span data-ttu-id="f51e1-192">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f51e1-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f51e1-193">c.</span><span class="sxs-lookup"><span data-stu-id="f51e1-193">c.</span></span> <span data-ttu-id="f51e1-194">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f51e1-195">d.</span><span class="sxs-lookup"><span data-stu-id="f51e1-195">d.</span></span> <span data-ttu-id="f51e1-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="f51e1-197">Создание тестового пользователя UltiPro</span><span class="sxs-lookup"><span data-stu-id="f51e1-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="f51e1-198">В этом разделе описано, как создать пользователя Britta Simon в приложении UltiPro.</span><span class="sxs-lookup"><span data-stu-id="f51e1-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="f51e1-199">Обратитесь к [группе поддержки UltiPro](https://www.ultimatesoftware.com/ContactUs), чтобы добавить пользователей в учетную запись UltiPro.</span><span class="sxs-lookup"><span data-stu-id="f51e1-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add the users in the UltiPro platform.</span></span> <span data-ttu-id="f51e1-200">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="f51e1-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f51e1-201">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f51e1-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f51e1-202">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к UltiPro.</span><span class="sxs-lookup"><span data-stu-id="f51e1-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UltiPro.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f51e1-204">**Чтобы назначить пользователя Britta Simon приложению UltiPro, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f51e1-204">**To assign Britta Simon to UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="f51e1-205">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f51e1-207">Из списка приложений выберите **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-207">In the applications list, select **UltiPro**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="f51e1-209">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f51e1-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-211">Click **Add** button.</span></span> <span data-ttu-id="f51e1-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f51e1-214">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f51e1-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f51e1-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f51e1-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f51e1-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f51e1-217">Testing single sign-on</span></span>

<span data-ttu-id="f51e1-218">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f51e1-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f51e1-219">Щелкнув элемент UltiPro на панели доступа, вы автоматически войдете в приложение UltiPro.</span><span class="sxs-lookup"><span data-stu-id="f51e1-219">When you click the UltiPro tile in the Access Panel, you should get automatically signed-on to your UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f51e1-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f51e1-220">Additional resources</span></span>

* [<span data-ttu-id="f51e1-221">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f51e1-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f51e1-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f51e1-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png

