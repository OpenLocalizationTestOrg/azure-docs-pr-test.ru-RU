---
title: "Руководство по интеграции Azure Active Directory с ServiceChannel | Документы Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="f60c6-103">Руководство: интеграция Azure Active Directory с ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="f60c6-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="f60c6-104">В этом руководстве описано, как интегрировать ServiceChannel с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f60c6-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f60c6-105">Интеграция ServiceChannel с Azure AD дает приведенные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="f60c6-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f60c6-106">С помощью Azure AD вы можете контролировать доступ пользователей к ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="f60c6-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="f60c6-107">Вы можете включить автоматический вход пользователей в ServiceChannel (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f60c6-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f60c6-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="f60c6-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="f60c6-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f60c6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f60c6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f60c6-110">Prerequisites</span></span>

<span data-ttu-id="f60c6-111">Чтобы настроить интеграцию Azure AD с ServiceChannel, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f60c6-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="f60c6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f60c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f60c6-113">подписка ServiceChannel с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f60c6-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f60c6-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f60c6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f60c6-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="f60c6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f60c6-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="f60c6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f60c6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f60c6-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f60c6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f60c6-118">Scenario description</span></span>
<span data-ttu-id="f60c6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f60c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f60c6-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="f60c6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f60c6-121">Добавление ServiceChannel из коллекции</span><span class="sxs-lookup"><span data-stu-id="f60c6-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="f60c6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f60c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="f60c6-123">Добавление ServiceChannel из коллекции</span><span class="sxs-lookup"><span data-stu-id="f60c6-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="f60c6-124">Чтобы настроить интеграцию ServiceChannel с Azure AD, необходимо добавить ServiceChannel из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f60c6-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f60c6-125">**Чтобы добавить ServiceChannel из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="f60c6-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f60c6-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f60c6-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f60c6-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f60c6-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f60c6-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f60c6-133">В поле поиска введите **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-133">In the search box, type **ServiceChannel**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="f60c6-135">На панели результатов выберите **ServiceChannel** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="f60c6-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f60c6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f60c6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f60c6-138">В этом разделе описана настройка и проверка единого входа Azure AD в ServiceChannel с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f60c6-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f60c6-139">Чтобы настроить единый вход в Azure AD, необходимо знать, какой пользователь в ServiceChannel соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f60c6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="f60c6-140">То есть необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="f60c6-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="f60c6-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="f60c6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="f60c6-142">Чтобы настроить и проверить единый вход Azure AD в ServiceChannel, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="f60c6-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f60c6-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="f60c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f60c6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f60c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f60c6-145">**[Создание тестового пользователя ServiceChannel](#creating-a-servicechannel-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f60c6-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="f60c6-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f60c6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f60c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f60c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f60c6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f60c6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f60c6-149">В этом разделе описано, как включить единый вход в Azure AD на портале управления Azure и настроить его в приложении ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="f60c6-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="f60c6-150">**Чтобы настроить единый вход Azure AD в ServiceChannel, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f60c6-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="f60c6-151">На портале управления Azure на странице интеграции с приложением **ServiceChannel** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f60c6-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="f60c6-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="f60c6-155">В разделе **Домены и URL-адреса приложения ServiceChannel** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f60c6-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="f60c6-157">а.</span><span class="sxs-lookup"><span data-stu-id="f60c6-157">a.</span></span> <span data-ttu-id="f60c6-158">В текстовом поле **Идентификатор** введите значение `http://adfs.<domain>.com/adfs/service/trust`.</span><span class="sxs-lookup"><span data-stu-id="f60c6-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="f60c6-159">b.</span><span class="sxs-lookup"><span data-stu-id="f60c6-159">b.</span></span> <span data-ttu-id="f60c6-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<customer domain>.servicechannel.com/saml/acs`.</span><span class="sxs-lookup"><span data-stu-id="f60c6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f60c6-161">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f60c6-161">Please note that these are not the real values.</span></span> <span data-ttu-id="f60c6-162">Необходимо указать фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="f60c6-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="f60c6-163">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="f60c6-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="f60c6-164">Чтобы получить эти значения, обратитесь в [службу поддержки ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="f60c6-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="f60c6-165">Приложение ServiceChannel ожидает проверочные утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="f60c6-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="f60c6-166">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="f60c6-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="f60c6-167">**NameIdentifier(идентификатор пользователя)** — это единственное обязательное утверждение, а значение по умолчанию — **user.userprincipalname**, однако ServiceChannel ожидает его сопоставления с **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="f60c6-168">Если вы планируете включить JIT-подготовку пользователей, следует добавить следующие утверждения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f60c6-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="f60c6-169">Утверждение **Роль** должно быть сопоставлено с **user.assignedroles**, содержащим роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="f60c6-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="f60c6-170">Дополнительные инструкции по работе с утверждениями можно найти в руководстве по ServiceChannel [здесь](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example).</span><span class="sxs-lookup"><span data-stu-id="f60c6-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="f60c6-172">Перейдите по [этой ссылке](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/), чтобы прочитать о настройке **роли** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f60c6-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="f60c6-173">В разделе **Атрибуты пользователя** установите флажок **Просмотреть и изменить все другие атрибуты пользователей** и задайте эти атрибуты.</span><span class="sxs-lookup"><span data-stu-id="f60c6-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="f60c6-174">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="f60c6-174">Attribute Name</span></span> | <span data-ttu-id="f60c6-175">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="f60c6-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="f60c6-176">Роль</span><span class="sxs-lookup"><span data-stu-id="f60c6-176">Role</span></span>| <span data-ttu-id="f60c6-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="f60c6-177">user.assignedroles</span></span> |

    <span data-ttu-id="f60c6-178">а.</span><span class="sxs-lookup"><span data-stu-id="f60c6-178">a.</span></span> <span data-ttu-id="f60c6-179">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="f60c6-182">b.</span><span class="sxs-lookup"><span data-stu-id="f60c6-182">b.</span></span> <span data-ttu-id="f60c6-183">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f60c6-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f60c6-184">c.</span><span class="sxs-lookup"><span data-stu-id="f60c6-184">c.</span></span> <span data-ttu-id="f60c6-185">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f60c6-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f60c6-186">d.</span><span class="sxs-lookup"><span data-stu-id="f60c6-186">d.</span></span> <span data-ttu-id="f60c6-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="f60c6-188">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f60c6-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="f60c6-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-190">Click **Save**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f60c6-192">В разделе **Настройка ServiceChannel** щелкните **Настроить ServiceChannel**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f60c6-193">Запишите **идентификатор сущности SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="f60c6-194">Для настройки единого входа на стороне **ServiceChannel** необходимо отправить загруженный **сертификат (Base64)** и **идентификатор сущности SAML** в [службу поддержки ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="f60c6-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="f60c6-195">Это позволит службе поддержки правильно настроить подключение единого входа SAML на обоих сторонах.</span><span class="sxs-lookup"><span data-stu-id="f60c6-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f60c6-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f60c6-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="f60c6-197">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f60c6-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f60c6-199">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f60c6-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f60c6-200">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f60c6-202">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="f60c6-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f60c6-204">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f60c6-206">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f60c6-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f60c6-208">а.</span><span class="sxs-lookup"><span data-stu-id="f60c6-208">a.</span></span> <span data-ttu-id="f60c6-209">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f60c6-210">b.</span><span class="sxs-lookup"><span data-stu-id="f60c6-210">b.</span></span> <span data-ttu-id="f60c6-211">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f60c6-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f60c6-212">c.</span><span class="sxs-lookup"><span data-stu-id="f60c6-212">c.</span></span> <span data-ttu-id="f60c6-213">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f60c6-214">d.</span><span class="sxs-lookup"><span data-stu-id="f60c6-214">d.</span></span> <span data-ttu-id="f60c6-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="f60c6-216">Создание тестового пользователя ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="f60c6-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="f60c6-217">Приложение поддерживает JIT-подготовку пользователей, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="f60c6-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="f60c6-218">Для настройки полной подготовки пользователей обратитесь в [службу поддержки ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="f60c6-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f60c6-219">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f60c6-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f60c6-220">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="f60c6-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f60c6-222">**Чтобы назначить пользователя Britta Simon в ServiceChannel, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="f60c6-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="f60c6-223">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f60c6-225">В списке приложений выберите **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="f60c6-227">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f60c6-229">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-229">Click **Add** button.</span></span> <span data-ttu-id="f60c6-230">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f60c6-232">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f60c6-233">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f60c6-234">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f60c6-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f60c6-235">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f60c6-235">Testing single sign-on</span></span>

<span data-ttu-id="f60c6-236">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f60c6-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f60c6-237">Щелкнув элемент ServiceChannel на панели доступа, вы автоматически войдете в приложение ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="f60c6-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f60c6-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f60c6-238">Additional resources</span></span>

* [<span data-ttu-id="f60c6-239">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f60c6-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f60c6-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f60c6-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png