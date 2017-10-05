---
title: "Руководство по интеграции Azure Active Directory с Zscaler Private Access (ZPA) | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Zscaler Private Access (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 5c598bfa5b6725d21a89df54dbcb3314cc631d80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="9a3f3-103">Руководство по интеграции Azure Active Directory с Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="9a3f3-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="9a3f3-104">В этом руководстве описано, как интегрировать Zscaler Private Access (ZPA) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a3f3-105">Интеграция Azure AD с Zscaler Private Access (ZPA) обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a3f3-106">С помощью Azure AD вы можете контролировать доступ к Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="9a3f3-107">Вы можете включить автоматический вход пользователей в Zscaler Private Access (ZPA) (единый вход) с их учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a3f3-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="9a3f3-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a3f3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9a3f3-110">Prerequisites</span></span>

<span data-ttu-id="9a3f3-111">Чтобы настроить интеграцию Azure AD с Zscaler Private Access (ZPA), вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9a3f3-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span></span>

- <span data-ttu-id="9a3f3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9a3f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a3f3-113">подписка Zscaler Private Access (ZPA) с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="9a3f3-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="9a3f3-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9a3f3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a3f3-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9a3f3-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="9a3f3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9a3f3-118">Scenario description</span></span>
<span data-ttu-id="9a3f3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a3f3-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9a3f3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a3f3-121">Добавление Zscaler Private Access (ZPA) из коллекции.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-121">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
2. <span data-ttu-id="9a3f3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a3f3-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-the-gallery"></a><span data-ttu-id="9a3f3-123">Добавление Zscaler Private Access (ZPA) из коллекции</span><span class="sxs-lookup"><span data-stu-id="9a3f3-123">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
<span data-ttu-id="9a3f3-124">Чтобы настроить интеграцию Zscaler Private Access (ZPA) с Azure AD, необходимо добавить Zscaler Private Access (ZPA) из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a3f3-125">**Чтобы добавить Zscaler Private Access (ZPA) из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="9a3f3-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a3f3-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9a3f3-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a3f3-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9a3f3-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9a3f3-133">В поле поиска введите **Zscaler Private Access (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-133">In the search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="9a3f3-135">На панели результатов выберите **Zscaler Private Access (ZPA)** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9a3f3-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a3f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9a3f3-138">В этом разделе описана настройка и проверка единого входа Azure AD в Zscaler Private Access (ZPA) с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a3f3-139">Чтобы единый вход работал, Azure AD необходимо указать, какой пользователь в Zscaler Private Access (ZPA) соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span></span> <span data-ttu-id="9a3f3-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span></span>

<span data-ttu-id="9a3f3-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="9a3f3-142">Чтобы настроить и проверить единый вход Azure AD в Zscaler Private Access (ZPA), вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="9a3f3-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a3f3-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a3f3-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a3f3-145">**[Создание тестового пользователя Zscaler Private Access (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)** требуется для создания в Zscaler Private Access (ZPA) пользователя Britta Simon, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9a3f3-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a3f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9a3f3-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a3f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9a3f3-149">В этом разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="9a3f3-150">**Чтобы настроить единый вход Azure AD в Zscaler Private Access (ZPA), выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="9a3f3-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="9a3f3-151">На портале управления Azure на странице интеграции с приложением **Zscaler Private Access (ZPA)** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9a3f3-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="9a3f3-155">В разделе **Домены и URL-адреса приложения Zscaler Private Access (ZPA)** выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="9a3f3-157">а.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-157">a.</span></span> <span data-ttu-id="9a3f3-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="9a3f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-159">b.</span></span> <span data-ttu-id="9a3f3-160">В текстовом поле **Идентификатор** введите `https://samlsp.private.zscaler.com/auth/metadata`.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a3f3-161">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-161">Please note that these are not the real values.</span></span> <span data-ttu-id="9a3f3-162">Необходимо заменить эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="9a3f3-163">Мы рекомендуем использовать для идентификатора уникальное значение URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-163">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="9a3f3-164">Обратитесь к [группе поддержки Zscaler Private Access (ZPA)](https://help.zscaler.com/zpa-submit-ticket), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>

4. <span data-ttu-id="9a3f3-165">В разделе **Сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="9a3f3-167">В диалоговом окне **Создание нового сертификата** щелкните значок календаря и выберите **дату окончания срока действия**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="9a3f3-168">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-168">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="9a3f3-170">В разделе **Сертификат подписи SAML** выберите **Make new certificate active** (Сделать новый сертификат активным) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="9a3f3-172">Во всплывающем окне **Rollover certificate** (Сертификат восстановления) нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="9a3f3-174">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="9a3f3-176">В другом окне веб-браузера войдите на свой корпоративный сайт Zscaler Private Access (ZPA) в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="9a3f3-177">Выберите **Administrator** (Администратор) и щелкните **Idp Configuration** (Конфигурация IdP).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-177">Navigate to **Administrator** and then click **Idp Configuration**.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="9a3f3-179">В разделе **Idp Configuration** (Конфигурация IdP) щелкните **Add New IDP Configuration** (Добавить новую конфигурацию IdP).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="9a3f3-181">В разделе **New IDP Configuration** (Создание конфигурации IdP) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-181">In the **New IDP Configuration** section, perform the following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="9a3f3-183">а.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-183">a.</span></span> <span data-ttu-id="9a3f3-184">Чтобы отправить скачанный файл метаданных, щелкните **Select File** (Выбрать файл).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="9a3f3-185">b.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-185">b.</span></span> <span data-ttu-id="9a3f3-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9a3f3-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9a3f3-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a3f3-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9a3f3-188">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9a3f3-190">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9a3f3-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a3f3-191">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a3f3-193">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a3f3-195">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a3f3-197">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a3f3-199">а.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-199">a.</span></span> <span data-ttu-id="9a3f3-200">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a3f3-201">b.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-201">b.</span></span> <span data-ttu-id="9a3f3-202">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a3f3-203">c.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-203">c.</span></span> <span data-ttu-id="9a3f3-204">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9a3f3-205">d.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-205">d.</span></span> <span data-ttu-id="9a3f3-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="9a3f3-207">Создание тестового пользователя Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="9a3f3-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="9a3f3-208">В этом разделе описано, как создать пользователя Britta Simon в приложении Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="9a3f3-209">Обратитесь за помощью к [группе поддержки Zscaler Private Access (ZPA)](https://help.zscaler.com/zpa-submit-ticket), чтобы добавить пользователей на платформе Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9a3f3-210">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a3f3-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9a3f3-211">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9a3f3-213">**Чтобы назначить пользователя Britta Simon в Zscaler Private Access (ZPA), выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="9a3f3-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="9a3f3-214">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9a3f3-216">Из списка приложений выберите **Zscaler Private Access (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="9a3f3-218">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9a3f3-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-220">Click **Add** button.</span></span> <span data-ttu-id="9a3f3-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9a3f3-223">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a3f3-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a3f3-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="9a3f3-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9a3f3-226">Testing single sign-on</span></span>

<span data-ttu-id="9a3f3-227">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9a3f3-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9a3f3-228">Щелкнув элемент "Zscaler Private Access (ZPA)" на панели доступа, вы автоматически войдете в свое приложение Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9a3f3-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9a3f3-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9a3f3-229">Additional resources</span></span>

* [<span data-ttu-id="9a3f3-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a3f3-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a3f3-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a3f3-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png