---
title: "Руководство по интеграции Azure Active Directory с Proofpoint on Demand | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в Proofpoint on Demand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="9faa6-103">Руководство. Интеграция Azure Active Directory с Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="9faa6-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="9faa6-104">В этом руководстве описано, как интегрировать Proofpoint on Demand с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9faa6-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9faa6-105">Интеграция Azure AD с приложением Proofpoint on Demand обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9faa6-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9faa6-106">С помощью Azure AD вы можете контролировать доступ к Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="9faa6-107">Вы можете включить автоматический вход пользователей в Proofpoint on Demand (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9faa6-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9faa6-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9faa6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9faa6-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9faa6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9faa6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9faa6-110">Prerequisites</span></span>

<span data-ttu-id="9faa6-111">Чтобы настроить интеграцию Azure AD с Proofpoint on Demand, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9faa6-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="9faa6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9faa6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9faa6-113">подписка с поддержкой единого входа Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9faa6-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9faa6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9faa6-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9faa6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9faa6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9faa6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9faa6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9faa6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9faa6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9faa6-118">Scenario description</span></span>
<span data-ttu-id="9faa6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9faa6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9faa6-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9faa6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9faa6-121">Добавление Proofpoint on Demand из коллекции</span><span class="sxs-lookup"><span data-stu-id="9faa6-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="9faa6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9faa6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="9faa6-123">Добавление Proofpoint on Demand из коллекции</span><span class="sxs-lookup"><span data-stu-id="9faa6-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="9faa6-124">Чтобы настроить интеграцию приложения Proofpoint on Demand с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9faa6-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9faa6-125">**Чтобы добавить Proofpoint on Demand из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9faa6-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9faa6-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9faa6-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9faa6-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9faa6-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9faa6-133">В поле поиска введите **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="9faa6-135">В области результатов выберите **Proofpoint on Demand** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="9faa6-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9faa6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9faa6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9faa6-138">Этот раздел описывает, как настроить и проверить единый вход Azure AD в Proofpoint on Demand с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9faa6-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9faa6-139">Чтобы настроить единый вход в Azure AD, необходимо знать, какой пользователь в Proofpoint on Demand соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9faa6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="9faa6-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="9faa6-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="9faa6-142">Чтобы настроить и проверить единый вход Azure AD в Proofpoint on Demand, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="9faa6-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9faa6-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9faa6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9faa6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9faa6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9faa6-145">**[Создание тестового пользователя Proofpoint on Demand](#creating-a-proofpoint-on-demand-test-user)** требуется для создания пользователя Britta Simon в Proofpoint on Demand, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9faa6-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9faa6-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9faa6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9faa6-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9faa6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9faa6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9faa6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9faa6-149">Этот раздел описывает, как включить единый вход Azure AD на портале Azure и настроить его в приложении Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="9faa6-150">**Чтобы настроить единый вход Azure AD в Proofpoint on Demand, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9faa6-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="9faa6-151">На портале Azure на странице интеграции с приложением **Proofpoint on Demand** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9faa6-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9faa6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="9faa6-155">В разделе **Домены и URL-адреса приложения Proofpoint on Demand** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9faa6-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="9faa6-157">a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="9faa6-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="9faa6-158">b.</span><span class="sxs-lookup"><span data-stu-id="9faa6-158">b.</span></span> <span data-ttu-id="9faa6-159">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="9faa6-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="9faa6-160">c.</span><span class="sxs-lookup"><span data-stu-id="9faa6-160">c.</span></span>  <span data-ttu-id="9faa6-161">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`.</span><span class="sxs-lookup"><span data-stu-id="9faa6-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9faa6-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9faa6-162">These values are not the real.</span></span> <span data-ttu-id="9faa6-163">Замените их на фактические значения идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="9faa6-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="9faa6-164">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Proofpoint on Demand](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="9faa6-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="9faa6-165">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9faa6-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="9faa6-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9faa6-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="9faa6-169">В разделе **Конфигурация Proofpoint on Demand** щелкните **Настроить Proofpoint on Demand**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9faa6-170">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="9faa6-172">Чтобы настроить единый вход на стороне **Proofpoint on Demand**, нужно отправить скачанный **сертификат (Base64)**, **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** [группе поддержки клиентов Proofpoint on Demand](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="9faa6-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="9faa6-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="9faa6-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9faa6-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="9faa6-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9faa6-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9faa6-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9faa6-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9faa6-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="9faa6-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9faa6-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9faa6-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9faa6-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9faa6-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9faa6-182">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9faa6-182">These values are not the real.</span></span> <span data-ttu-id="9faa6-183">Замените эти значения фактическими значениями.</span><span class="sxs-lookup"><span data-stu-id="9faa6-183">Update these values with the actual</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9faa6-185">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9faa6-187">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9faa6-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9faa6-189">А.</span><span class="sxs-lookup"><span data-stu-id="9faa6-189">a.</span></span> <span data-ttu-id="9faa6-190">В текстовом поле **Name** (Имя) введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="9faa6-191">b.</span><span class="sxs-lookup"><span data-stu-id="9faa6-191">b.</span></span> <span data-ttu-id="9faa6-192">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9faa6-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="9faa6-193">c.</span><span class="sxs-lookup"><span data-stu-id="9faa6-193">c.</span></span> <span data-ttu-id="9faa6-194">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9faa6-195">d.</span><span class="sxs-lookup"><span data-stu-id="9faa6-195">d.</span></span> <span data-ttu-id="9faa6-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="9faa6-197">Создание тестового пользователя Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="9faa6-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="9faa6-198">В этом разделе описано, как создать пользователя Britta Simon в Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="9faa6-199">Обратитесь в [службу поддержки клиентов Proofpoint on Demand](https://www.proofpoint.com/us/support-services), чтобы добавить пользователей на платформу Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9faa6-200">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9faa6-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9faa6-201">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9faa6-203">**Чтобы назначить пользователя Britta Simon в Proofpoint on Demand, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9faa6-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="9faa6-204">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9faa6-206">В списке приложений выберите **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="9faa6-208">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9faa6-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-210">Click **Add** button.</span></span> <span data-ttu-id="9faa6-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9faa6-213">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9faa6-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9faa6-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9faa6-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9faa6-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9faa6-216">Testing single sign-on</span></span>

<span data-ttu-id="9faa6-217">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9faa6-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9faa6-218">Щелкнув плитку **Proofpoint on Demand** на панели доступа, вы автоматически войдете в приложение Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="9faa6-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="9faa6-219">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9faa6-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="9faa6-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9faa6-220">Additional resources</span></span>

* [<span data-ttu-id="9faa6-221">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9faa6-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9faa6-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9faa6-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

