---
title: "Руководство по интеграции Azure Active Directory с ServiceNow | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в ServiceNow или ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="3e94c-103">Руководство: интеграция Azure Active Directory с ServiceNow</span><span class="sxs-lookup"><span data-stu-id="3e94c-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="3e94c-104">В этом руководстве описано, как интегрировать ServiceNow и ServiceNow Express с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e94c-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e94c-105">Интеграция Azure AD с ServiceNow и ServiceNow Express обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3e94c-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="3e94c-106">С помощью Azure AD вы можете контролировать доступ к ServiceNow и ServiceNow Express.</span><span class="sxs-lookup"><span data-stu-id="3e94c-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="3e94c-107">Вы можете включить автоматический вход пользователей в ServiceNow и ServiceNow Express (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e94c-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="3e94c-108">Вы можете управлять учетными записями централизованно — через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3e94c-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3e94c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e94c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e94c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3e94c-110">Prerequisites</span></span>
<span data-ttu-id="3e94c-111">Чтобы настроить интеграцию Azure AD с ServiceNow и ServiceNow Express, вам потребуется следующее.</span><span class="sxs-lookup"><span data-stu-id="3e94c-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="3e94c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3e94c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="3e94c-113">Экземпляр или клиент ServiceNow версии Calgary или выше (для ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="3e94c-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="3e94c-114">Экземпляр ServiceNow Express версии Helsinki или выше (для ServiceNow Express).</span><span class="sxs-lookup"><span data-stu-id="3e94c-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="3e94c-115">В клиенте ServiceNow должен быть включен [подключаемый модуль единого входа для нескольких поставщиков](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0).</span><span class="sxs-lookup"><span data-stu-id="3e94c-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="3e94c-116">Это можно сделать путем [отправки запроса на обслуживание](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="3e94c-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="3e94c-117">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3e94c-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="3e94c-118">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3e94c-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="3e94c-119">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="3e94c-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="3e94c-120">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e94c-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e94c-121">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3e94c-121">Scenario description</span></span>
<span data-ttu-id="3e94c-122">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3e94c-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e94c-123">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="3e94c-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e94c-124">Добавление ServiceNow из коллекции.</span><span class="sxs-lookup"><span data-stu-id="3e94c-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="3e94c-125">Настройка и проверка единого входа Azure AD в ServiceNow или ServiceNow Express.</span><span class="sxs-lookup"><span data-stu-id="3e94c-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="3e94c-126">Добавление ServiceNow из коллекции</span><span class="sxs-lookup"><span data-stu-id="3e94c-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="3e94c-127">Чтобы настроить интеграцию ServiceNow или ServiceNow Express с Azure AD, необходимо добавить ServiceNow из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3e94c-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="3e94c-128">**Чтобы добавить ServiceNow из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="3e94c-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e94c-129">На **классическом портале Azure**в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="3e94c-131">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="3e94c-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3e94c-132">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="3e94c-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Приложения][2]
4. <span data-ttu-id="3e94c-134">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="3e94c-134">Click **Add** at the bottom of the page.</span></span>
   
    ![Приложения][3]
5. <span data-ttu-id="3e94c-136">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Приложения][4]
6. <span data-ttu-id="3e94c-138">В поле поиска введите **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="3e94c-140">В области результатов выберите **ServiceNow** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="3e94c-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e94c-142">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e94c-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e94c-143">В этом разделе описано, как настроить и проверить единый вход Azure AD в ServiceNow или ServiceNow Express с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e94c-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e94c-144">Чтобы настроить единый вход в Azure AD, необходимо знать, какой пользователь в ServiceNow соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e94c-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="3e94c-145">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="3e94c-146">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="3e94c-147">Чтобы настроить и проверить единый вход Azure AD в ServiceNow, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="3e94c-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e94c-148">**[Настройка единого входа Azure AD в ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** необходима, чтобы позволить пользователям использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3e94c-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e94c-149">**[Настройка единого входа Azure AD в ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** необходима, чтобы позволить пользователям использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3e94c-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="3e94c-150">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e94c-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="3e94c-151">**[Создание тестового пользователя ServiceNow](#creating-a-servicenow-test-user)** требуется для создания пользователя Britta Simon в ServiceNow, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e94c-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="3e94c-152">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e94c-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="3e94c-153">**[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3e94c-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="3e94c-154">Чтобы настроить ServiceNow, пропустите шаг 2,</span><span class="sxs-lookup"><span data-stu-id="3e94c-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="3e94c-155">а чтобы настроить ServiceNow Express — шаг 1.</span><span class="sxs-lookup"><span data-stu-id="3e94c-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="3e94c-156">Настройка единого входа Azure AD в ServiceNow</span><span class="sxs-lookup"><span data-stu-id="3e94c-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="3e94c-157">На классическом портале Azure AD на странице интеграции с приложением **ServiceNow** нажмите кнопку **Настроить единый вход**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="3e94c-158">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="3e94c-159">На странице **Как пользователи должны входить в ServiceNow?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="3e94c-160">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="3e94c-161">На странице **Настройка параметров приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="3e94c-162">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="3e94c-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="3e94c-163">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-163">a.</span></span> <span data-ttu-id="3e94c-164">В текстовое поле **URL-адрес входа в ServiceNow** введите URL-адрес, используемый пользователями для входа в приложение ServiceNow, в следующем формате `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="3e94c-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="3e94c-165">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-165">b.</span></span> <span data-ttu-id="3e94c-166">В текстовое поле **Идентификатор** введите URL-адрес, используемый пользователями для входа в приложение ServiceNow, в следующем формате `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="3e94c-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="3e94c-167">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-167">c.</span></span> <span data-ttu-id="3e94c-168">Щелкните **Далее**</span><span class="sxs-lookup"><span data-stu-id="3e94c-168">Click **Next**</span></span>

4. <span data-ttu-id="3e94c-169">Чтобы в Azure AD была выполнена автоматическая настройка ServiceNow для аутентификации на основе SAML, введите имя вашего экземпляра ServiceNow, имя пользователя с правами администратора и пароль администратора в форму **Настроить единый вход автоматически** , после чего щелкните *Настроить*.</span><span class="sxs-lookup"><span data-stu-id="3e94c-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="3e94c-170">Обратите внимание, что для этого указываемому пользователю с правами администратора должна быть назначена роль **security_admin** в ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="3e94c-171">Вы также можете вручную настроить в ServiceNow использование Azure AD в качестве поставщика удостоверений SAML. Для этого щелкните **Вручную настроить это приложение для единого входа**, затем нажмите кнопку **Далее** и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="3e94c-172">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="3e94c-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="3e94c-173">На странице **Настройка единого входа в ServiceNow** щелкните **Скачать сертификат** и сохраните файл сертификата на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3e94c-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="3e94c-174">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="3e94c-175">Войдите в приложение ServiceNow с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3e94c-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="3e94c-176">Активируйте подключаемый модуль *Integration - Multiple Provider Single Sign-On Installer* (Интеграция — установщик единого входа для нескольких поставщиков), выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="3e94c-177">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-177">a.</span></span> <span data-ttu-id="3e94c-178">В левой области навигации выберите раздел **Определение системы** и щелкните **Подключаемые модули**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="3e94c-179">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Активация подключаемого модуля")</span><span class="sxs-lookup"><span data-stu-id="3e94c-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="3e94c-180">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-180">b.</span></span> <span data-ttu-id="3e94c-181">Найдите *Integration - Multiple Provider Single Sign-On Installer* (Интеграция — установщик единого входа для нескольких поставщиков).</span><span class="sxs-lookup"><span data-stu-id="3e94c-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="3e94c-182">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Активация подключаемого модуля")</span><span class="sxs-lookup"><span data-stu-id="3e94c-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="3e94c-183">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-183">c.</span></span> <span data-ttu-id="3e94c-184">Выберите подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="3e94c-184">Select the plugin.</span></span> <span data-ttu-id="3e94c-185">Щелкните правой кнопкой мыши и выберите **Activate/Upgrade** (Активировать или обновить).</span><span class="sxs-lookup"><span data-stu-id="3e94c-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="3e94c-186">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-186">d.</span></span> <span data-ttu-id="3e94c-187">Нажмите кнопку **Активировать**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="3e94c-188">На панели навигации слева щелкните **Properties**(Свойства).</span><span class="sxs-lookup"><span data-stu-id="3e94c-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="3e94c-189">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="3e94c-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="3e94c-190">В диалоговом окне **Multiple Provider SSO Properties** (Свойства единого входа для нескольких поставщиков) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="3e94c-191">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="3e94c-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="3e94c-192">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-192">a.</span></span> <span data-ttu-id="3e94c-193">Для параметра **Enable multiple provider SSO** (Включить единый вход для нескольких поставщиков) выберите значение **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="3e94c-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="3e94c-194">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-194">b.</span></span> <span data-ttu-id="3e94c-195">Для параметра **Enable debug logging got the multiple provider SSO integration** (Включить ведение журнала отладки для интеграции нескольких поставщиков единого входа) выберите **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="3e94c-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="3e94c-196">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-196">c.</span></span> <span data-ttu-id="3e94c-197">В текстовом поле **The field on the user table that...** (Поле в пользовательской таблице) введите значение **user_name**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="3e94c-198">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-198">d.</span></span> <span data-ttu-id="3e94c-199">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-199">Click **Save**.</span></span>

10. <span data-ttu-id="3e94c-200">На панели навигации слева щелкните **x509 Certificates**(Сертификаты x509).</span><span class="sxs-lookup"><span data-stu-id="3e94c-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="3e94c-201">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="3e94c-202">В диалоговом окне **X.509 Certificates** (Сертификаты X.509) нажмите кнопку **New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="3e94c-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="3e94c-203">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="3e94c-204">В диалоговом окне **X.509 Certificates** (Сертификаты X.509) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="3e94c-205">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="3e94c-206">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-206">a.</span></span> <span data-ttu-id="3e94c-207">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-207">Click **New**.</span></span>
    
     <span data-ttu-id="3e94c-208">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-208">b.</span></span> <span data-ttu-id="3e94c-209">В текстовом поле **Name** (Имя) введите имя конфигурации (например, **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="3e94c-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="3e94c-210">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-210">c.</span></span> <span data-ttu-id="3e94c-211">Установите флажок **Активно**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-211">Select **Active**.</span></span>
    
     <span data-ttu-id="3e94c-212">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-212">d.</span></span> <span data-ttu-id="3e94c-213">В поле **Format** (Формат) выберите **PEM**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="3e94c-214">д.</span><span class="sxs-lookup"><span data-stu-id="3e94c-214">e.</span></span> <span data-ttu-id="3e94c-215">В поле **Type** (Тип) выберите **Trust Store Cert** (Сертификат хранилища доверия).</span><span class="sxs-lookup"><span data-stu-id="3e94c-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="3e94c-216">Е.</span><span class="sxs-lookup"><span data-stu-id="3e94c-216">f.</span></span> <span data-ttu-id="3e94c-217">Откройте сертификат в кодировке Base 64 в блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **PEM Certificate** (Сертификат PEM).</span><span class="sxs-lookup"><span data-stu-id="3e94c-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="3e94c-218">ж.</span><span class="sxs-lookup"><span data-stu-id="3e94c-218">g.</span></span> <span data-ttu-id="3e94c-219">Нажмите кнопку **Update**(Обновить).</span><span class="sxs-lookup"><span data-stu-id="3e94c-219">Click **Update**.</span></span>

13. <span data-ttu-id="3e94c-220">На панели навигации слева щелкните **Identity Providers**(Поставщики удостоверений).</span><span class="sxs-lookup"><span data-stu-id="3e94c-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="3e94c-221">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="3e94c-222">В диалоговом окне **Identity Providers** (Поставщики удостоверений) нажмите кнопку **New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="3e94c-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="3e94c-223">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="3e94c-224">В диалоговом окне **Identity Providers** (Поставщики удостоверений) щелкните **SAML2 Update1?**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="3e94c-225">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="3e94c-226">В диалоговом окне SAML2 Update1 Properties (Свойства SAML2 Update1) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="3e94c-227">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="3e94c-228">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-228">a.</span></span> <span data-ttu-id="3e94c-229">В текстовом поле **Name** (Имя) введите имя конфигурации (например, **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="3e94c-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="3e94c-230">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-230">b.</span></span> <span data-ttu-id="3e94c-231">В текстовом поле **User Field** (Поле пользователя) введите значение **email** или **user_name**, в зависимости от того, какое поле используется для уникальной идентификации пользователей в развернутой службе ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="3e94c-232">В Azure AD можно настроить, чтобы в качестве уникального идентификатора в токене SAML выдавался идентификатор пользователя Azure AD (имя участника-пользователя) или его электронный адрес. Для этого перейдите в раздел **ServiceNow > Атрибуты > Единый вход** на классическом портале Azure и сопоставьте нужное поле с атрибутом **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="3e94c-233">Значение, хранящееся для выбранного атрибута в Azure AD (например, имя участника-пользователя) должно соответствовать значению, хранящемуся в ServiceNow для заполненного поля (например, user_name).</span><span class="sxs-lookup"><span data-stu-id="3e94c-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="3e94c-234">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-234">c.</span></span> <span data-ttu-id="3e94c-235">На классическом портале Azure AD скопируйте значение поля **Идентификатор поставщика удостоверений**, а затем вставьте его в текстовое поле **Identity provider URL** (URL-адрес поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="3e94c-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="3e94c-236">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-236">d.</span></span> <span data-ttu-id="3e94c-237">На классическом портале Azure AD скопируйте значение поля **URL-адрес запроса проверки подлинности**, а затем вставьте его в текстовое поле **Identity Provider's AuthnRequest** (Запрос аутентификации поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="3e94c-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="3e94c-238">д.</span><span class="sxs-lookup"><span data-stu-id="3e94c-238">e.</span></span> <span data-ttu-id="3e94c-239">На классическом портале Azure AD скопируйте значение поля **URL-адрес службы единого входа**, а затем вставьте его в текстовое поле **Identity Provider's SingleLogoutRequest** (Запрос на единый выход поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="3e94c-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="3e94c-240">Е.</span><span class="sxs-lookup"><span data-stu-id="3e94c-240">f.</span></span> <span data-ttu-id="3e94c-241">В текстовое поле **ServiceNow Homepage** (Домашняя страница ServiceNow) введите URL-адрес домашней страницы экземпляра ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e94c-242">URL-адрес домашней страницы экземпляра ServiceNow состоит из **URL-адреса клиента ServiceNow** и **/navpage.do** (например, `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="3e94c-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="3e94c-243">ж.</span><span class="sxs-lookup"><span data-stu-id="3e94c-243">g.</span></span> <span data-ttu-id="3e94c-244">В текстовое поле **Entity ID / Issuer** (Идентификатор сущности или издатель) введите URL-адрес клиента ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="3e94c-245">h.</span><span class="sxs-lookup"><span data-stu-id="3e94c-245">h.</span></span> <span data-ttu-id="3e94c-246">В текстовое поле **Audience URL** (URL-адрес аудитории) введите URL-адрес клиента ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="3e94c-247">i.</span><span class="sxs-lookup"><span data-stu-id="3e94c-247">i.</span></span> <span data-ttu-id="3e94c-248">В текстовом поле **Protocol Binding for the IDP's SingleLogoutRequest** (Привязка протокола для запроса на единый выход поставщика удостоверений) введите **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="3e94c-249">j.</span><span class="sxs-lookup"><span data-stu-id="3e94c-249">j.</span></span> <span data-ttu-id="3e94c-250">В текстовое поле NameID Policy (Политика идентификатора имени) введите **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="3e94c-251">k.</span><span class="sxs-lookup"><span data-stu-id="3e94c-251">k.</span></span> <span data-ttu-id="3e94c-252">Снимите флажок **Create an AuthnContextClass**(Создать класс контекста проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="3e94c-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="3e94c-253">l.</span><span class="sxs-lookup"><span data-stu-id="3e94c-253">l.</span></span> <span data-ttu-id="3e94c-254">В поле **AuthnContextClassRef Method** (Метод AuthnContextClassRef) введите `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="3e94c-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="3e94c-255">Это действие требуется только для организаций на основе облака.</span><span class="sxs-lookup"><span data-stu-id="3e94c-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="3e94c-256">Если используется локальная аутентификация AD FS или MFA, это значение указывать не нужно.</span><span class="sxs-lookup"><span data-stu-id="3e94c-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="3e94c-257">m.</span><span class="sxs-lookup"><span data-stu-id="3e94c-257">m.</span></span> <span data-ttu-id="3e94c-258">В текстовое поле **Clock Skew** (Разница в показаниях часов) введите **60**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="3e94c-259">n.</span><span class="sxs-lookup"><span data-stu-id="3e94c-259">n.</span></span> <span data-ttu-id="3e94c-260">В поле **Single Sign On Script** (Сценарий единого входа) выберите **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="3e94c-261">o.</span><span class="sxs-lookup"><span data-stu-id="3e94c-261">o.</span></span> <span data-ttu-id="3e94c-262">В поле **x509 Certificate**(Сертификат x509) выберите сертификат, созданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="3e94c-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="3e94c-263">p.</span><span class="sxs-lookup"><span data-stu-id="3e94c-263">p.</span></span> <span data-ttu-id="3e94c-264">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="3e94c-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="3e94c-265">На классическом портале Azure выберите подтверждение конфигурации единого входа и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="3e94c-266">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="3e94c-267">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="3e94c-268">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="3e94c-269">Настройка единого входа в Azure AD для ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="3e94c-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="3e94c-270">На классическом портале Azure AD на странице интеграции с приложением **ServiceNow** нажмите кнопку **Настроить единый вход**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="3e94c-271">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="3e94c-272">На странице **Как пользователи должны входить в ServiceNow?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="3e94c-273">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="3e94c-274">На странице **Настройка параметров приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="3e94c-275">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="3e94c-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="3e94c-276">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-276">a.</span></span> <span data-ttu-id="3e94c-277">В текстовое поле **URL-адрес входа в ServiceNow** введите URL-адрес, используемый пользователями для входа в приложение ServiceNow, в следующем формате `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="3e94c-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="3e94c-278">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-278">b.</span></span> <span data-ttu-id="3e94c-279">В текстовое поле **URL-адрес издателя** введите URL-адрес, используемый пользователями для входа в приложение ServiceNow, в следующем формате `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="3e94c-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="3e94c-280">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-280">c.</span></span> <span data-ttu-id="3e94c-281">Щелкните **Далее**</span><span class="sxs-lookup"><span data-stu-id="3e94c-281">Click **Next**</span></span>

4. <span data-ttu-id="3e94c-282">Установите флажок **Вручную настроить это приложение для единого входа**, а затем нажмите кнопку **Далее** и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="3e94c-283">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="3e94c-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="3e94c-284">На странице **Настройка единого входа в ServiceNow** щелкните **Скачать сертификат**, сохраните файл сертификата на локальном компьютере, затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="3e94c-285">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="3e94c-286">Войдите в приложение ServiceNow Express с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3e94c-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="3e94c-287">В расположенной слева области навигации щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="3e94c-288">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="3e94c-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="3e94c-289">В диалоговом окне **Единый вход** щелкните значок конфигурации в правом верхнем углу и настройте следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="3e94c-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="3e94c-290">![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="3e94c-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="3e94c-291">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-291">a.</span></span> <span data-ttu-id="3e94c-292">Передвиньте переключатель **Enable multiple provider SSO** (Включить единый вход для нескольких поставщиков) вправо.</span><span class="sxs-lookup"><span data-stu-id="3e94c-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="3e94c-293">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-293">b.</span></span> <span data-ttu-id="3e94c-294">Передвиньте переключатель **Enable debug logging for the multiple provider SSO integration** (Включить ведение журнала отладки для интеграции нескольких поставщиков единого входа) вправо.</span><span class="sxs-lookup"><span data-stu-id="3e94c-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="3e94c-295">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-295">c.</span></span> <span data-ttu-id="3e94c-296">В текстовом поле **The field on the user table that...** (Поле в пользовательской таблице) введите значение **user_name**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="3e94c-297">В диалоговом окне **Единый вход** щелкните **Добавить новый сертификат**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="3e94c-298">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="3e94c-299">В диалоговом окне **X.509 Certificates** (Сертификаты X.509) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="3e94c-300">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="3e94c-301">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-301">a.</span></span> <span data-ttu-id="3e94c-302">В текстовом поле **Name** (Имя) введите имя конфигурации (например, **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="3e94c-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="3e94c-303">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-303">b.</span></span> <span data-ttu-id="3e94c-304">Установите флажок **Активно**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-304">Select **Active**.</span></span>
    
    <span data-ttu-id="3e94c-305">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-305">c.</span></span> <span data-ttu-id="3e94c-306">В поле **Format** (Формат) выберите **PEM**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="3e94c-307">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-307">d.</span></span> <span data-ttu-id="3e94c-308">В поле **Type** (Тип) выберите **Trust Store Cert** (Сертификат хранилища доверия).</span><span class="sxs-lookup"><span data-stu-id="3e94c-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="3e94c-309">д.</span><span class="sxs-lookup"><span data-stu-id="3e94c-309">e.</span></span> <span data-ttu-id="3e94c-310">Создайте файл в кодировке Base 64 из скачанного сертификата.</span><span class="sxs-lookup"><span data-stu-id="3e94c-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3e94c-311">Дополнительные сведения можно узнать в видео [Преобразование двоичного сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="3e94c-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="3e94c-312">Е.</span><span class="sxs-lookup"><span data-stu-id="3e94c-312">f.</span></span> <span data-ttu-id="3e94c-313">Откройте сертификат в кодировке Base 64 в блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **PEM Certificate** (Сертификат PEM).</span><span class="sxs-lookup"><span data-stu-id="3e94c-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="3e94c-314">ж.</span><span class="sxs-lookup"><span data-stu-id="3e94c-314">g.</span></span> <span data-ttu-id="3e94c-315">Нажмите кнопку **Update**(Обновить).</span><span class="sxs-lookup"><span data-stu-id="3e94c-315">Click **Update**.</span></span>
11. <span data-ttu-id="3e94c-316">В диалоговом окне **Единый вход** щелкните **Add New IdP** (Добавить нового поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="3e94c-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="3e94c-317">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="3e94c-318">В диалоговом окне **Add New Identity Provider** (Добавление нового поставщика удостоверений) в разделе **Configure Identity Provider** (Настройка поставщика удостоверений) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="3e94c-319">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="3e94c-320">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-320">a.</span></span> <span data-ttu-id="3e94c-321">В текстовом поле **Имя** введите имя конфигурации (например, **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="3e94c-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="3e94c-322">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-322">b.</span></span> <span data-ttu-id="3e94c-323">На классическом портале Azure AD скопируйте значение поля **Идентификатор поставщика удостоверений**, а затем вставьте его в текстовое поле **Identity provider URL** (URL-адрес поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="3e94c-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="3e94c-324">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-324">c.</span></span> <span data-ttu-id="3e94c-325">На классическом портале Azure AD скопируйте значение поля **URL-адрес запроса проверки подлинности**, а затем вставьте его в текстовое поле **Identity Provider's AuthnRequest** (Запрос аутентификации поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="3e94c-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="3e94c-326">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-326">d.</span></span> <span data-ttu-id="3e94c-327">На классическом портале Azure AD скопируйте значение поля **URL-адрес службы единого входа**, а затем вставьте его в текстовое поле **Identity Provider's SingleLogoutRequest** (Запрос на единый выход поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="3e94c-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="3e94c-328">д.</span><span class="sxs-lookup"><span data-stu-id="3e94c-328">e.</span></span> <span data-ttu-id="3e94c-329">В поле **Identity Provider Certificate** (Сертификат поставщика удостоверений) выберите сертификат, созданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="3e94c-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="3e94c-330">Щелкните **Дополнительные параметры** и в разделе **Additional Identity Provider Properties** (Дополнительные свойства поставщика удостоверений) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="3e94c-331">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="3e94c-332">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-332">a.</span></span> <span data-ttu-id="3e94c-333">В текстовом поле **Protocol Binding for the IDP's SingleLogoutRequest** (Привязка протокола для запроса на единый выход поставщика удостоверений) введите **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="3e94c-334">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-334">b.</span></span> <span data-ttu-id="3e94c-335">В текстовое поле **NameID Policy** (Политика идентификатора имени) введите **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="3e94c-336">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-336">c.</span></span> <span data-ttu-id="3e94c-337">В поле **AuthnContextClassRef Method** (Метод AuthnContextClassRef) введите **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="3e94c-338">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-338">d.</span></span> <span data-ttu-id="3e94c-339">Снимите флажок **Create an AuthnContextClass**(Создать класс контекста проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="3e94c-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="3e94c-340">В разделе **Additional Service Provider Properties** (Дополнительные свойства поставщика услуг) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="3e94c-341">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="3e94c-342">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-342">a.</span></span> <span data-ttu-id="3e94c-343">В текстовое поле **ServiceNow Homepage** (Домашняя страница ServiceNow) введите URL-адрес домашней страницы экземпляра ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="3e94c-344">URL-адрес домашней страницы экземпляра ServiceNow состоит из **URL-адреса клиента ServiceNow** и **/navpage.do** (например, `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="3e94c-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="3e94c-345">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-345">b.</span></span> <span data-ttu-id="3e94c-346">В текстовое поле **Entity ID / Issuer** (Идентификатор сущности или издатель) введите URL-адрес клиента ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="3e94c-347">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-347">c.</span></span> <span data-ttu-id="3e94c-348">В текстовое поле **Audience URI** (URI аудитории) введите URL-адрес клиента ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="3e94c-349">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-349">d.</span></span> <span data-ttu-id="3e94c-350">В текстовое поле **Clock Skew** (Разница в показаниях часов) введите **60**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="3e94c-351">д.</span><span class="sxs-lookup"><span data-stu-id="3e94c-351">e.</span></span> <span data-ttu-id="3e94c-352">В текстовом поле **User Field** (Поле пользователя) введите значение **email** или **user_name**, в зависимости от того, какое поле используется для уникальной идентификации пользователей в развернутой службе ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="3e94c-353">В Azure AD можно настроить, чтобы в качестве уникального идентификатора в токене SAML выдавался идентификатор пользователя Azure AD (имя участника-пользователя) или его электронный адрес. Для этого перейдите в раздел **ServiceNow > Атрибуты > Единый вход** на классическом портале Azure и сопоставьте нужное поле с атрибутом **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="3e94c-354">Значение, хранящееся для выбранного атрибута в Azure AD (например, имя участника-пользователя) должно соответствовать значению, хранящемуся в ServiceNow для заполненного поля (например, user_name).</span><span class="sxs-lookup"><span data-stu-id="3e94c-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="3e94c-355">Е.</span><span class="sxs-lookup"><span data-stu-id="3e94c-355">f.</span></span> <span data-ttu-id="3e94c-356">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-356">Click **Save**.</span></span> 

3. <span data-ttu-id="3e94c-357">На классическом портале Azure выберите подтверждение конфигурации единого входа и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="3e94c-358">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="3e94c-359">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="3e94c-360">![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="3e94c-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="3e94c-361">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="3e94c-361">Configuring user provisioning</span></span>
<span data-ttu-id="3e94c-362">В этом разделе показано, как включить подготовку учетных записей пользователей Active Directory для ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="3e94c-363">Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="3e94c-364">На классическом портале Azure на странице интеграции с приложением **ServiceNow** щелкните **Настроить подготовку учетных записей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="3e94c-365">![Подготовка учетных записей пользователей](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Подготовка учетных записей пользователей")</span><span class="sxs-lookup"><span data-stu-id="3e94c-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="3e94c-366">На странице **Введите учетные данные ServiceNow, чтобы включить автоматическую подготовку учетных записей пользователей** укажите следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="3e94c-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="3e94c-367">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-367">a.</span></span> <span data-ttu-id="3e94c-368">В текстовое поле **Имя экземпляра ServiceNow** введите имя экземпляра ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="3e94c-369">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-369">b.</span></span> <span data-ttu-id="3e94c-370">В текстовом поле **Имя пользователя администратора ServiceNow** введите имя учетной записи администратора ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="3e94c-371">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-371">c.</span></span> <span data-ttu-id="3e94c-372">В текстовое поле **Пароль администратора ServiceNow** введите пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3e94c-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="3e94c-373">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-373">d.</span></span> <span data-ttu-id="3e94c-374">Нажмите **проверить** для проверки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3e94c-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="3e94c-375">д.</span><span class="sxs-lookup"><span data-stu-id="3e94c-375">e.</span></span> <span data-ttu-id="3e94c-376">Нажмите кнопку **Далее**, чтобы открыть страницу **Дальнейшие действия**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="3e94c-377">Е.</span><span class="sxs-lookup"><span data-stu-id="3e94c-377">f.</span></span> <span data-ttu-id="3e94c-378">Если вы хотите подготовить всех пользователей для этого приложения, установите флажок**Автоматически настраивать все учетные записи пользователей из каталога в этом приложении**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="3e94c-379">![Дальнейшие действия](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Дальнейшие действия")</span><span class="sxs-lookup"><span data-stu-id="3e94c-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="3e94c-380">g.</span><span class="sxs-lookup"><span data-stu-id="3e94c-380">g.</span></span> <span data-ttu-id="3e94c-381">На странице **Дальнейшие действия** нажмите кнопку **Завершить**, чтобы сохранить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="3e94c-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e94c-382">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e94c-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e94c-383">В этом разделе описано, как создать на классическом портале тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e94c-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="3e94c-385">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3e94c-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e94c-386">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="3e94c-388">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="3e94c-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3e94c-389">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e94c-391">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="3e94c-393">На странице диалогового окна **Тип учетной записи пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="3e94c-395">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-395">a.</span></span> <span data-ttu-id="3e94c-396">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="3e94c-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="3e94c-397">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-397">b.</span></span> <span data-ttu-id="3e94c-398">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="3e94c-399">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-399">c.</span></span> <span data-ttu-id="3e94c-400">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-400">Click **Next**.</span></span>

6. <span data-ttu-id="3e94c-401">На странице диалогового окна **Профиль пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="3e94c-403">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-403">a.</span></span> <span data-ttu-id="3e94c-404">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="3e94c-405">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-405">b.</span></span> <span data-ttu-id="3e94c-406">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="3e94c-407">c.</span><span class="sxs-lookup"><span data-stu-id="3e94c-407">c.</span></span> <span data-ttu-id="3e94c-408">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="3e94c-409">d.</span><span class="sxs-lookup"><span data-stu-id="3e94c-409">d.</span></span> <span data-ttu-id="3e94c-410">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="3e94c-411">д.</span><span class="sxs-lookup"><span data-stu-id="3e94c-411">e.</span></span> <span data-ttu-id="3e94c-412">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-412">Click **Next**.</span></span>

7. <span data-ttu-id="3e94c-413">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="3e94c-415">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3e94c-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="3e94c-417">а.</span><span class="sxs-lookup"><span data-stu-id="3e94c-417">a.</span></span> <span data-ttu-id="3e94c-418">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="3e94c-419">b.</span><span class="sxs-lookup"><span data-stu-id="3e94c-419">b.</span></span> <span data-ttu-id="3e94c-420">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="3e94c-421">Создание тестового пользователя ServiceNow</span><span class="sxs-lookup"><span data-stu-id="3e94c-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="3e94c-422">В этом разделе описано, как создать пользователя Britta Simon в ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="3e94c-423">В этом разделе описано, как создать пользователя Britta Simon в ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="3e94c-424">Если вы не знаете, как добавить пользователя в свою учетную запись ServiceNow или ServiceNow Express, обратитесь в службу поддержки ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3e94c-425">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e94c-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="3e94c-426">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3e94c-428">**Чтобы назначить пользователя Britta Simon в ServiceNow, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="3e94c-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="3e94c-429">Чтобы открыть представление приложений, в представлении каталога на классическом портале щелкните **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="3e94c-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Назначение пользователя][201] 

2. <span data-ttu-id="3e94c-431">В списке приложений выберите **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="3e94c-433">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-433">In the menu on the top, click **Users**.</span></span>
   
    ![Назначение пользователя][203] 

4. <span data-ttu-id="3e94c-435">В списке "Все пользователи" выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="3e94c-436">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3e94c-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="3e94c-438">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3e94c-438">Testing single sign-on</span></span>
<span data-ttu-id="3e94c-439">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3e94c-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3e94c-440">Щелкнув плитку ServiceNow на панели доступа, вы автоматически войдете в приложение ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="3e94c-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e94c-441">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3e94c-441">Additional resources</span></span>
* [<span data-ttu-id="3e94c-442">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e94c-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e94c-443">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e94c-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
