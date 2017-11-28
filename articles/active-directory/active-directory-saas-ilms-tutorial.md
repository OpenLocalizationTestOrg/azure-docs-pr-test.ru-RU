---
title: "Руководство. Интеграция Azure Active Directory с iLMS | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="2aa11-103">Руководство. Интеграция Azure Active Directory с iLMS</span><span class="sxs-lookup"><span data-stu-id="2aa11-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="2aa11-104">В этом руководстве описано, как интегрировать iLMS с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2aa11-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2aa11-105">Интеграция Azure AD с приложением iLMS обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="2aa11-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2aa11-106">С помощью Azure AD вы можете контролировать доступ к iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="2aa11-107">Вы можете включить автоматический вход пользователей в iLMS (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aa11-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2aa11-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa11-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2aa11-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2aa11-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2aa11-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2aa11-110">Prerequisites</span></span>

<span data-ttu-id="2aa11-111">Чтобы настроить интеграцию Azure AD с iLMS, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="2aa11-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="2aa11-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2aa11-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2aa11-113">подписка iLMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="2aa11-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2aa11-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="2aa11-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2aa11-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="2aa11-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2aa11-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="2aa11-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2aa11-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2aa11-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2aa11-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2aa11-118">Scenario description</span></span>
<span data-ttu-id="2aa11-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2aa11-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2aa11-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="2aa11-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2aa11-121">Добавление iLMS из коллекции</span><span class="sxs-lookup"><span data-stu-id="2aa11-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="2aa11-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aa11-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="2aa11-123">Добавление iLMS из коллекции</span><span class="sxs-lookup"><span data-stu-id="2aa11-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="2aa11-124">Чтобы настроить интеграцию iLMS с Azure AD, необходимо добавить iLMS из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2aa11-125">**Чтобы добавить iLMS из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="2aa11-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2aa11-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2aa11-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2aa11-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="2aa11-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="2aa11-133">В поле поиска введите **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-133">In the search box, type **iLMS**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="2aa11-135">На панели результатов выберите **iLMS** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="2aa11-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2aa11-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aa11-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2aa11-138">В этом разделе описана настройка и проверка единого входа Azure AD в iLMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2aa11-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2aa11-139">Чтобы единый вход работал, в Azure AD необходимо указать, какой пользователь в iLMS соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aa11-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="2aa11-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="2aa11-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="2aa11-142">Чтобы настроить и проверить единый вход Azure AD в iLMS, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="2aa11-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2aa11-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="2aa11-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2aa11-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2aa11-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2aa11-145">**[Создание тестового пользователя iLMS](#creating-an-ilms-test-user)** требуется для создания в iLMS пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aa11-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2aa11-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aa11-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2aa11-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2aa11-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2aa11-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aa11-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2aa11-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="2aa11-150">**Чтобы настроить единый вход Azure AD в iLMS, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="2aa11-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="2aa11-151">На портале Azure на странице интеграции с приложением **iLMS** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="2aa11-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="2aa11-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="2aa11-155">Если вы хотите настроить приложение в режиме, инициированном **поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения iLMS** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2aa11-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="2aa11-157">а.</span><span class="sxs-lookup"><span data-stu-id="2aa11-157">a.</span></span> <span data-ttu-id="2aa11-158">В текстовое поле **Идентификатор** вставьте значение **идентификатора**, которое необходимо скопировать в разделе параметров SAML **Service Provider** (Поставщик услуг) на портале администрирования iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="2aa11-159">b.</span><span class="sxs-lookup"><span data-stu-id="2aa11-159">b.</span></span> <span data-ttu-id="2aa11-160">В текстовое поле **URL-адрес ответа** вставьте значение **URL-адреса конечной точки**, которое необходимо скопировать в разделе параметров SAML **Service Provider** (Поставщик услуг) на портале администрирования iLMS, в следующем виде `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="2aa11-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="2aa11-161">Значение "123456" указано в качестве примера идентификатора.</span><span class="sxs-lookup"><span data-stu-id="2aa11-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="2aa11-162">Установите флажок **Показать дополнительные параметры URL-адресов**, если вы хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="2aa11-164">В текстовое поле **URL-адрес входа** вставьте значение **URL-адреса конечной точки**, которое необходимо скопировать в разделе параметров SAML **Service Provider** (Поставщик услуг) на портале администрирования iLMS, в виде `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="2aa11-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="2aa11-165">Чтобы выполнить JIT-подготовку, приложение iLMS ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="2aa11-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2aa11-166">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="2aa11-166">Configure the following claims for this application.</span></span> <span data-ttu-id="2aa11-167">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="2aa11-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="2aa11-168">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="2aa11-168">The following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="2aa11-170">Создайте атрибуты **department, region** и **division** и добавьте их имена в iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="2aa11-171">Все указанные выше атрибуты являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="2aa11-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="2aa11-172">В iLMS необходимо установить флажок **Create Un-recognized User Account** (Создать учетную запись неопознанного пользователя) для сопоставления этих атрибутов.</span><span class="sxs-lookup"><span data-stu-id="2aa11-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="2aa11-173">Следуйте указаниям, приведенным [здесь](http://support.inspiredelearning.com/customer/portal/articles/2204526), чтобы получить представление о конфигурации атрибутов.</span><span class="sxs-lookup"><span data-stu-id="2aa11-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="2aa11-174">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2aa11-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="2aa11-175">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="2aa11-175">Attribute Name</span></span> | <span data-ttu-id="2aa11-176">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="2aa11-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="2aa11-177">division</span><span class="sxs-lookup"><span data-stu-id="2aa11-177">division</span></span> | <span data-ttu-id="2aa11-178">user.department</span><span class="sxs-lookup"><span data-stu-id="2aa11-178">user.department</span></span> |
    | <span data-ttu-id="2aa11-179">region</span><span class="sxs-lookup"><span data-stu-id="2aa11-179">region</span></span> | <span data-ttu-id="2aa11-180">user.state</span><span class="sxs-lookup"><span data-stu-id="2aa11-180">user.state</span></span> |
    | <span data-ttu-id="2aa11-181">department</span><span class="sxs-lookup"><span data-stu-id="2aa11-181">department</span></span> | <span data-ttu-id="2aa11-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="2aa11-182">user.jobtitle</span></span> |

    <span data-ttu-id="2aa11-183">а.</span><span class="sxs-lookup"><span data-stu-id="2aa11-183">a.</span></span> <span data-ttu-id="2aa11-184">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="2aa11-187">b.</span><span class="sxs-lookup"><span data-stu-id="2aa11-187">b.</span></span> <span data-ttu-id="2aa11-188">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="2aa11-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="2aa11-189">c.</span><span class="sxs-lookup"><span data-stu-id="2aa11-189">c.</span></span> <span data-ttu-id="2aa11-190">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="2aa11-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="2aa11-191">d.</span><span class="sxs-lookup"><span data-stu-id="2aa11-191">d.</span></span> <span data-ttu-id="2aa11-192">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-192">Click **Ok**</span></span>

7. <span data-ttu-id="2aa11-193">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2aa11-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="2aa11-195">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2aa11-195">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="2aa11-197">В другом окне браузера войдите на **портал администрирования iLMS** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="2aa11-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="2aa11-198">На вкладке **Settings** (Параметры) щелкните **SSO:SAML**, чтобы открыть параметры SAML, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2aa11-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="2aa11-200">а.</span><span class="sxs-lookup"><span data-stu-id="2aa11-200">a.</span></span> <span data-ttu-id="2aa11-201">Разверните раздел **Service Provider** (Поставщик услуг) и скопируйте значения **идентификатора** и **URL-адреса конечной точки**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="2aa11-203">b.</span><span class="sxs-lookup"><span data-stu-id="2aa11-203">b.</span></span> <span data-ttu-id="2aa11-204">В разделе **Identity Provider** (Поставщик удостоверений) установите переключатель **Import Metadata** (Импорт метаданных).</span><span class="sxs-lookup"><span data-stu-id="2aa11-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="2aa11-205">c.</span><span class="sxs-lookup"><span data-stu-id="2aa11-205">c.</span></span> <span data-ttu-id="2aa11-206">Выберите файл **метаданных**, скачанный с портала Azure в разделе **Сертификат подписи SAML**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="2aa11-208">d.</span><span class="sxs-lookup"><span data-stu-id="2aa11-208">d.</span></span> <span data-ttu-id="2aa11-209">Если вы хотите включить JIT-подготовку, чтобы создать учетные записи iLMS для неопознанных пользователей, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2aa11-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="2aa11-210">Установите флажок **Create Un-recognized User Account** (Создать учетную запись неопознанного пользователя) для сопоставления этих атрибутов.</span><span class="sxs-lookup"><span data-stu-id="2aa11-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="2aa11-212">Сопоставьте атрибуты в Azure AD с атрибутами в iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="2aa11-213">В столбце атрибутов укажите имена атрибутов или значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2aa11-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="2aa11-214">д.</span><span class="sxs-lookup"><span data-stu-id="2aa11-214">e.</span></span> <span data-ttu-id="2aa11-215">Перейдите на вкладку **Business Rules** (Бизнес-правила) и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2aa11-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="2aa11-217">Установите флажок **Create Un-recognized Regions, Divisions and Departments** (Создать неопознанные регионы, подразделения и отделы), чтобы создать регионы, подразделения и отделы, которые не существуют во время выполнения единого входа.</span><span class="sxs-lookup"><span data-stu-id="2aa11-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="2aa11-218">Установите флажок **Update User Profile During Sign-in** (Обновить профиль пользователя во время выполнения входа), чтобы профиль пользователя обновлялся во время каждого выполнения единого входа.</span><span class="sxs-lookup"><span data-stu-id="2aa11-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="2aa11-219">Если установлен флажок **Update Blank Values for Non Mandatory Fields in User Profile** (Обновить пустые значения в необязательных полях в профиле пользователя), необязательные поля профиля пользователя, пустые во время выполнения входа, будут также пустыми в профиле пользователя iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="2aa11-220">Установите флажок **Send Error Notification Email** (Отправить уведомление об ошибке по электронной почте) и введите адрес электронной почты пользователя, на который будет отправлено уведомление об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2aa11-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="2aa11-221">Нажмите кнопку **Сохранить**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="2aa11-221">Click **Save** button to save the settings.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="2aa11-223">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="2aa11-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2aa11-224">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="2aa11-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2aa11-225">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="2aa11-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2aa11-226">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aa11-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="2aa11-227">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2aa11-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="2aa11-229">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="2aa11-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2aa11-230">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2aa11-232">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="2aa11-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2aa11-234">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2aa11-236">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2aa11-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2aa11-238">а.</span><span class="sxs-lookup"><span data-stu-id="2aa11-238">a.</span></span> <span data-ttu-id="2aa11-239">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2aa11-240">b.</span><span class="sxs-lookup"><span data-stu-id="2aa11-240">b.</span></span> <span data-ttu-id="2aa11-241">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2aa11-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2aa11-242">c.</span><span class="sxs-lookup"><span data-stu-id="2aa11-242">c.</span></span> <span data-ttu-id="2aa11-243">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2aa11-244">d.</span><span class="sxs-lookup"><span data-stu-id="2aa11-244">d.</span></span> <span data-ttu-id="2aa11-245">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="2aa11-246">Создание тестового пользователя iLMS</span><span class="sxs-lookup"><span data-stu-id="2aa11-246">Creating an iLMS test user</span></span>

<span data-ttu-id="2aa11-247">Приложение поддерживает JIT-подготовку пользователей, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="2aa11-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="2aa11-248">Чтобы включить JIT-подготовку, установите флажок **Create Un-recognized User Account** (Создать учетную запись неопознанного пользователя) во время настройки конфигурации SAML на портале администрирования iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="2aa11-249">Если необходимо создать пользователя вручную, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2aa11-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="2aa11-250">Войдите на веб-сайт iLMS компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="2aa11-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="2aa11-251">На вкладке **Users** (Пользователи) щелкните **Register User** (Регистрация пользователя), чтобы открыть страницу **регистрации пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![Добавление сотрудника](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="2aa11-253">На странице **Register User** (Регистрация пользователя) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2aa11-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="2aa11-255">а.</span><span class="sxs-lookup"><span data-stu-id="2aa11-255">a.</span></span> <span data-ttu-id="2aa11-256">В текстовом поле **First Name** (Имя) введите имя Britta.</span><span class="sxs-lookup"><span data-stu-id="2aa11-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="2aa11-257">b.</span><span class="sxs-lookup"><span data-stu-id="2aa11-257">b.</span></span> <span data-ttu-id="2aa11-258">В текстовом поле **Last Name** (Фамилия) введите фамилию Simon.</span><span class="sxs-lookup"><span data-stu-id="2aa11-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="2aa11-259">c.</span><span class="sxs-lookup"><span data-stu-id="2aa11-259">c.</span></span> <span data-ttu-id="2aa11-260">В текстовом поле **Email ID** (Электронная почта) введите адрес электронной почты учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2aa11-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="2aa11-261">d.</span><span class="sxs-lookup"><span data-stu-id="2aa11-261">d.</span></span> <span data-ttu-id="2aa11-262">В раскрывающемся списке **Region** (Регион) выберите регион.</span><span class="sxs-lookup"><span data-stu-id="2aa11-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="2aa11-263">д.</span><span class="sxs-lookup"><span data-stu-id="2aa11-263">e.</span></span> <span data-ttu-id="2aa11-264">В раскрывающемся списке **Division** (Подразделение) выберите подразделение.</span><span class="sxs-lookup"><span data-stu-id="2aa11-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="2aa11-265">f.</span><span class="sxs-lookup"><span data-stu-id="2aa11-265">f.</span></span> <span data-ttu-id="2aa11-266">В раскрывающемся списке **Department** (Отдел) выберите отдел.</span><span class="sxs-lookup"><span data-stu-id="2aa11-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="2aa11-267">g.</span><span class="sxs-lookup"><span data-stu-id="2aa11-267">g.</span></span> <span data-ttu-id="2aa11-268">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2aa11-269">Вы можете отправить пользователю сообщение о регистрации, установив флажок **Send Registration Mail** (Отправить регистрационное сообщение).</span><span class="sxs-lookup"><span data-stu-id="2aa11-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2aa11-270">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aa11-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2aa11-271">В этом разделе описано, как предоставить пользователю Britta Simon доступ к iLMS, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa11-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="2aa11-273">**Чтобы назначить пользователя Britta Simon в iLMS, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="2aa11-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="2aa11-274">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2aa11-276">В списке приложений выберите **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-276">In the applications list, select **iLMS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="2aa11-278">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-278">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="2aa11-280">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-280">Click **Add** button.</span></span> <span data-ttu-id="2aa11-281">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="2aa11-283">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2aa11-284">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2aa11-285">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="2aa11-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2aa11-286">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2aa11-286">Testing single sign-on</span></span>

<span data-ttu-id="2aa11-287">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2aa11-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2aa11-288">Щелкнув плитку iLMS на панели доступа, вы автоматически войдете в приложение iLMS.</span><span class="sxs-lookup"><span data-stu-id="2aa11-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2aa11-289">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2aa11-289">Additional resources</span></span>

* [<span data-ttu-id="2aa11-290">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2aa11-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2aa11-291">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2aa11-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

