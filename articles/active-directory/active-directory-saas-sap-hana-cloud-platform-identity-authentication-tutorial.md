---
title: "Руководство по интеграции Azure Active Directory с приложением SAP HANA Cloud Platform Identity Authentication | Документация Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и SAP HANA Cloud Platform Identity Authentication."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 7799bf03cc6705f805a48f329a265a3d84bed55f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="40eeb-103">Руководство по интеграции Azure Active Directory с приложением SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="40eeb-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="40eeb-104">В этом руководстве описано, как интегрировать приложение SAP HANA Cloud Platform Identity Authentication с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40eeb-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="40eeb-105">Приложение SAP HANA Cloud Platform Identity Authentication используется в качестве поставщика удостоверений прокси-сервера для доступа к приложениям SAP с использованием Azure AD в качестве главного поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="40eeb-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span></span>

<span data-ttu-id="40eeb-106">Интеграция приложения SAP HANA Cloud Platform Identity Authentication с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="40eeb-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40eeb-107">с помощью Azure AD вы можете контролировать доступ к приложению SAP;</span><span class="sxs-lookup"><span data-stu-id="40eeb-107">You can control in Azure AD who has access to SAP application</span></span>
- <span data-ttu-id="40eeb-108">Вы можете включить автоматический вход пользователей в приложения SAP (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40eeb-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="40eeb-109">Вы можете управлять учетными записями централизованно — через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="40eeb-109">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="40eeb-110">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40eeb-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="40eeb-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="40eeb-111">Prerequisites</span></span>

<span data-ttu-id="40eeb-112">Чтобы настроить интеграцию Azure AD с приложением SAP HANA Cloud Platform Identity Authentication, вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="40eeb-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span></span>

- <span data-ttu-id="40eeb-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="40eeb-113">An Azure AD subscription</span></span>
- <span data-ttu-id="40eeb-114">Подписка на **SAP HANA Cloud Platform Identity Authentication** с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="40eeb-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="40eeb-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="40eeb-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="40eeb-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="40eeb-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40eeb-117">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="40eeb-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="40eeb-118">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40eeb-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40eeb-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="40eeb-119">Scenario description</span></span>
<span data-ttu-id="40eeb-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="40eeb-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="40eeb-121">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="40eeb-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40eeb-122">Добавление приложения SAP HANA Cloud Platform Identity Authentication из коллекции</span><span class="sxs-lookup"><span data-stu-id="40eeb-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
2. <span data-ttu-id="40eeb-123">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40eeb-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="40eeb-124">Прежде чем углубиться в технические сведения, очень важно разобраться в основных понятиях, которые здесь будут представлены.</span><span class="sxs-lookup"><span data-stu-id="40eeb-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span></span> <span data-ttu-id="40eeb-125">Федерация SAP HANA Cloud Platform Identity Authentication и Azure Active Directory позволяет реализовать единый вход между приложениями и службами, защищенными с помощью AAD (выступающего в качестве поставщика удостоверений), и приложениями и службами SAP, защищенными с помощью SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="40eeb-126">В настоящее время приложение SAP HANA Cloud Platform Identity Authentication выступает в качестве поставщика удостоверений прокси-сервера для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="40eeb-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span></span> <span data-ttu-id="40eeb-127">В свою очередь, Azure Active Directory выступает ведущим поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="40eeb-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="40eeb-128">Этот пример представлен на схеме ниже.</span><span class="sxs-lookup"><span data-stu-id="40eeb-128">The following diagram illustrates this:</span></span>    

![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="40eeb-130">При такой конфигурации клиент SAP HANA Cloud Platform Identity Authentication будет настроен как надежное приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40eeb-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="40eeb-131">Все приложения и службы SAP, которые необходимо защитить таким образом, впоследствии настраиваются в консоли управления SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="40eeb-132">Это означает, что авторизация для предоставления доступа к приложениям и службам SAP для данной установки должна выполняться в приложении SAP HANA Cloud Platform Identity Authentication (в отличие от настройки авторизации в Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="40eeb-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="40eeb-133">Настроив SAP HANA Cloud Platform Identity Authentication как приложение в магазине Azure Active Directory, вам не нужно будет настраивать отдельные утверждения или утверждения SAML и преобразования, необходимые для создания действительного маркера проверки подлинности для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="40eeb-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="40eeb-134">В настоящее время единый вход для интернет-решений был проверен только обеими сторонами.</span><span class="sxs-lookup"><span data-stu-id="40eeb-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="40eeb-135">Потоки, необходимые для связи "приложение — API" и "API — API", работают, но они еще не проверялись.</span><span class="sxs-lookup"><span data-stu-id="40eeb-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="40eeb-136">Они будут проверены в ходе последующих действий.</span><span class="sxs-lookup"><span data-stu-id="40eeb-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a><span data-ttu-id="40eeb-137">Добавление приложения SAP HANA Cloud Platform Identity Authentication из коллекции</span><span class="sxs-lookup"><span data-stu-id="40eeb-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
<span data-ttu-id="40eeb-138">Для настройки интеграции SAP HANA Cloud Platform Identity Authentication с Azure AD необходимо добавить данное приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="40eeb-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40eeb-139">**Чтобы добавить SAP HANA Cloud Platform Identity Authentication из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="40eeb-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40eeb-140">На [**портале управления Azure**](https://portal.azure.com) в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40eeb-142">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40eeb-143">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-143">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="40eeb-145">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="40eeb-145">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="40eeb-147">В поле поиска введите **SAP HANA Cloud Platform Identity Authentication**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="40eeb-149">На панели результатов выберите **SAP HANA Cloud Platform Identity Authentication**, а затем нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="40eeb-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="40eeb-151">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40eeb-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="40eeb-152">В этом разделе описана настройка и проверка единого входа Azure AD в SAP HANA Cloud Platform Identity Authentication с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40eeb-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40eeb-153">Чтобы единый вход работал, в Azure AD необходимо указать, какой пользователь в SAP HANA Cloud Platform Identity Authentication соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40eeb-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span></span> <span data-ttu-id="40eeb-154">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span></span>

<span data-ttu-id="40eeb-155">Чтобы установить эту связь, следует указать **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="40eeb-156">Чтобы настроить и проверить единый вход Azure AD в SAP HANA Cloud Platform Identity Authentication, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="40eeb-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40eeb-157">**[Настройка единого входа Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="40eeb-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40eeb-158">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40eeb-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40eeb-159">**[Создание тестового пользователя SAP HANA Cloud Platform Identity Authentication](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** требуется для создания пользователя Britta Simon в SAP HANA Cloud Platform Identity Authentication, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40eeb-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="40eeb-160">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40eeb-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40eeb-161">**[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40eeb-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="40eeb-162">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="40eeb-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="40eeb-163">В данном разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="40eeb-164">Приложение SAP HANA Cloud Platform Identity Authentication ожидает утверждений SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="40eeb-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="40eeb-165">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="40eeb-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="40eeb-166">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="40eeb-166">The following screenshot shows an example for this.</span></span>

![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="40eeb-168">**Чтобы настроить единый вход Azure AD в приложении SAP HANA Cloud Platform Identity Authentication, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="40eeb-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="40eeb-169">На портале управления Azure на странице интеграции приложения **SAP HANA Cloud Platform Identity Authentication** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="40eeb-171">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="40eeb-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа][5]

3. <span data-ttu-id="40eeb-173">В диалоговом окне **Единый вход** в разделе **Атрибуты пользователя** укажите, ожидает ли приложение SAP атрибут, например firstName.</span><span class="sxs-lookup"><span data-stu-id="40eeb-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="40eeb-174">В диалоговом окне "Атрибуты токена SAML" добавьте атрибут firstName.</span><span class="sxs-lookup"><span data-stu-id="40eeb-174">On the SAML token attributes dialog, add the "firstName" attribute.</span></span>
 1. <span data-ttu-id="40eeb-175">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
 
    ![Настройка единого входа][6]

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="40eeb-178">В текстовом поле **Имя атрибута** введите firstName.</span><span class="sxs-lookup"><span data-stu-id="40eeb-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span></span>
 3. <span data-ttu-id="40eeb-179">В списке **Значение атрибута** выберите user.givenname.</span><span class="sxs-lookup"><span data-stu-id="40eeb-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="40eeb-180">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-180">Click **Ok**.</span></span>

4. <span data-ttu-id="40eeb-181">В разделе **Домены и URL-адреса приложения SAP HANA Cloud Platform Identity Authentication** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="40eeb-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="40eeb-183">В текстовом поле **URL-адрес для входа** введите URL-адрес входа для приложения SAP.</span><span class="sxs-lookup"><span data-stu-id="40eeb-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span></span>
 2. <span data-ttu-id="40eeb-184">В текстовом поле **Идентификатор** введите значение в следующем формате: `<entity-id>.accounts.ondemand.com`.</span><span class="sxs-lookup"><span data-stu-id="40eeb-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="40eeb-185">Если вы не знаете это значение, следуйте инструкциям документации SAP HANA Cloud Platform Identity Authentication по [настройке клиента SAML 2.0](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="40eeb-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="40eeb-186">В разделе **Настройка SAP HANA Cloud Platform Identity Authentication** щелкните **Настроить SAP HANA Cloud Platform Identity Authentication**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="40eeb-187">Щелкните **SAML XML Metadata** (Метаданные XML-элемента SAML), а затем сохраните файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="40eeb-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="40eeb-190">Чтобы настроить единый вход для приложения, перейдите к консоли администрирования SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="40eeb-191">URL-адрес имеет следующий формат: `https://<tenant-id>.accounts.ondemand.com/admin`.</span><span class="sxs-lookup"><span data-stu-id="40eeb-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="40eeb-192">Следуйте инструкциям документации SAP HANA Cloud Platform Identity Authentication, чтобы [настроить Microsoft Azure AD в качестве корпоративного поставщика удостоверений в SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="40eeb-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="40eeb-193">На портале управления Azure нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-193">In the Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="40eeb-194">Продолжайте выполнять описанные действия, только если вы хотите добавить и включить единый вход для другого приложения SAP.</span><span class="sxs-lookup"><span data-stu-id="40eeb-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span></span> <span data-ttu-id="40eeb-195">Повторите шаги, описанные в разделе "Добавление приложения SAP HANA Cloud Platform Identity Authentication из коллекции", чтобы добавить другой экземпляр SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="40eeb-196">На портале управления Azure на странице интеграции приложения **SAP HANA Cloud Platform Identity Authentication** щелкните **Связанный единый вход**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Настройка связанного единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="40eeb-198">Сохраните конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="40eeb-198">Then, save the configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="40eeb-199">Новое приложение будет использовать конфигурацию единого входа для предыдущих приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="40eeb-199">The new application will leverage the SSO configuration for the previous SAP application.</span></span> <span data-ttu-id="40eeb-200">Убедитесь в том, что в консоли администрирования SAP HANA Cloud Platform Identity Authentication используются те же поставщики корпоративных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="40eeb-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="40eeb-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="40eeb-201">Create an Azure AD test user</span></span>
<span data-ttu-id="40eeb-202">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40eeb-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="40eeb-204">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="40eeb-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40eeb-205">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40eeb-207">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="40eeb-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40eeb-209">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40eeb-211">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="40eeb-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="40eeb-213">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-213">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="40eeb-214">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="40eeb-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="40eeb-215">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-215">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="40eeb-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="40eeb-217">Создание тестового пользователя SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="40eeb-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="40eeb-218">В приложении SAP HANA Cloud Platform Identity Authentication не нужно создавать пользователя.</span><span class="sxs-lookup"><span data-stu-id="40eeb-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="40eeb-219">Пользователи, находящиеся в хранилище пользователей в Azure AD, могут использовать функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="40eeb-219">Users who are in the Azure AD user store can use the SSO functionality.</span></span>

<span data-ttu-id="40eeb-220">Приложение SAP HANA Cloud Platform Identity Authentication поддерживает параметр федерации удостоверений.</span><span class="sxs-lookup"><span data-stu-id="40eeb-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span></span> <span data-ttu-id="40eeb-221">Он позволяет приложению проверять, существуют ли пользователи, прошедшие проверку с помощью корпоративного поставщика удостоверений, в хранилище пользователей в приложении SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="40eeb-222">По умолчанию параметр федерации удостоверений отключен.</span><span class="sxs-lookup"><span data-stu-id="40eeb-222">In the default setting, the Identity Federation option is disabled.</span></span> <span data-ttu-id="40eeb-223">Если он включен, только пользователи, импортированные в SAP HANA Cloud Platform Identity Authentication, имеют доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="40eeb-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span></span> 

<span data-ttu-id="40eeb-224">Дополнительные сведения о включении или отключении параметра федерации удостоверений с помощью SAP HANA Cloud Platform Identity Authentication см. в разделе о включении этого параметра статьи [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html) (Настройка параметра федерации удостоверений с использованием хранилища пользователей в приложении SAP HANA Cloud Platform Identity Authentication).</span><span class="sxs-lookup"><span data-stu-id="40eeb-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="40eeb-225">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="40eeb-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="40eeb-226">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="40eeb-228">**Чтобы назначить пользователя Britta Simon в SAP HANA Cloud Platform Identity Authentication, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="40eeb-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="40eeb-229">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="40eeb-231">В списке приложений выберите **SAP HANA Cloud Platform Identity Authentication**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="40eeb-233">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="40eeb-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-235">Click **Add** button.</span></span> <span data-ttu-id="40eeb-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="40eeb-238">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40eeb-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40eeb-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="40eeb-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="40eeb-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="40eeb-241">Test single sign-on</span></span>

<span data-ttu-id="40eeb-242">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="40eeb-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="40eeb-243">Щелкнув плитку "SAP HANA Cloud Platform Identity Authentication" на панели доступа, вы автоматически войдете в приложение SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="40eeb-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="40eeb-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="40eeb-244">Additional resources</span></span>

* [<span data-ttu-id="40eeb-245">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40eeb-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40eeb-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="40eeb-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png