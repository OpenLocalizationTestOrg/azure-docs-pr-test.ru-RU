---
title: "Руководство. Интеграция Azure Active Directory с приложением Wdesk | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 37660b80cfb01d6a3105aea5ce248f1e03c46695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="7446f-103">Руководство. Интеграция Azure Active Directory с Wdesk</span><span class="sxs-lookup"><span data-stu-id="7446f-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="7446f-104">В этом руководстве описано, как интегрировать Wdesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7446f-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7446f-105">Интеграция приложения Wdesk с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="7446f-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7446f-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению Wdesk.</span><span class="sxs-lookup"><span data-stu-id="7446f-106">You can control in Azure AD who has access to Wdesk</span></span>
- <span data-ttu-id="7446f-107">Вы можете включить автоматический вход пользователей в Wdesk (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7446f-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7446f-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7446f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7446f-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье</span><span class="sxs-lookup"><span data-stu-id="7446f-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="7446f-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7446f-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7446f-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7446f-111">Prerequisites</span></span>

<span data-ttu-id="7446f-112">Чтобы настроить интеграцию Azure AD с Wdesk, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="7446f-112">To configure Azure AD integration with Wdesk, you need the following items:</span></span>

- <span data-ttu-id="7446f-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7446f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="7446f-114">подписка Wdesk с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7446f-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7446f-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7446f-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7446f-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7446f-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7446f-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7446f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7446f-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7446f-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7446f-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7446f-119">Scenario description</span></span>
<span data-ttu-id="7446f-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7446f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7446f-121">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="7446f-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7446f-122">Добавление Wdesk из коллекции</span><span class="sxs-lookup"><span data-stu-id="7446f-122">Adding Wdesk from the gallery</span></span>
2. <span data-ttu-id="7446f-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7446f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-the-gallery"></a><span data-ttu-id="7446f-124">Добавление Wdesk из коллекции</span><span class="sxs-lookup"><span data-stu-id="7446f-124">Adding Wdesk from the gallery</span></span>
<span data-ttu-id="7446f-125">Чтобы настроить интеграцию приложения Wdesk с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7446f-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7446f-126">**Добавление приложения Wdesk из коллекции**</span><span class="sxs-lookup"><span data-stu-id="7446f-126">**To add Wdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7446f-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7446f-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7446f-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="7446f-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7446f-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7446f-130">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7446f-132">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="7446f-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7446f-134">В поле поиска введите **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="7446f-134">In the search box, type **Wdesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="7446f-136">На панели результатов выберите **Wdesk** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="7446f-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7446f-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7446f-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7446f-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Wdesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7446f-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7446f-140">Для работы единого входа службе Azure AD нужно знать, какой пользователь в Wdesk соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7446f-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span></span> <span data-ttu-id="7446f-141">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Wdesk.</span><span class="sxs-lookup"><span data-stu-id="7446f-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span></span>

<span data-ttu-id="7446f-142">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Wdesk.</span><span class="sxs-lookup"><span data-stu-id="7446f-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span></span>

<span data-ttu-id="7446f-143">Чтобы настроить и проверить единый вход Azure AD в Wdesk, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7446f-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7446f-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7446f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7446f-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7446f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7446f-146">**[Создание тестового пользователя Wdesk](#creating-a-wdesk-test-user)** требуется для создания в Wdesk пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7446f-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7446f-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7446f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7446f-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7446f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7446f-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7446f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7446f-150">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Wdesk.</span><span class="sxs-lookup"><span data-stu-id="7446f-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="7446f-151">**Настройка единого входа Azure AD в Wdesk**</span><span class="sxs-lookup"><span data-stu-id="7446f-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="7446f-152">На портале Azure на странице интеграции с приложением **Wdesk** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7446f-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7446f-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="7446f-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="7446f-156">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Wdesk** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="7446f-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="7446f-158">а.</span><span class="sxs-lookup"><span data-stu-id="7446f-158">a.</span></span> <span data-ttu-id="7446f-159">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="7446f-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="7446f-160">b.</span><span class="sxs-lookup"><span data-stu-id="7446f-160">b.</span></span> <span data-ttu-id="7446f-161">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="7446f-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="7446f-162">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="7446f-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="7446f-163">Если вы хотите настроить приложение в **режиме, инициированном поставщиком услуг**, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7446f-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="7446f-165">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="7446f-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7446f-166">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7446f-166">These values are not real.</span></span> <span data-ttu-id="7446f-167">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="7446f-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7446f-168">Эти значения вы можете получить на портале Wdesk при настройке единого входа.</span><span class="sxs-lookup"><span data-stu-id="7446f-168">You get these values from WDesk portal when you configure the SSO.</span></span> 
  
5. <span data-ttu-id="7446f-169">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7446f-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="7446f-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7446f-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7446f-173">В другом окне браузера войдите в приложение Wdesk с правами администратора безопасности.</span><span class="sxs-lookup"><span data-stu-id="7446f-173">In a different web browser window, login to Wdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="7446f-174">В нижнем левом углу щелкните **Admin** (Администрирование) и выберите **Account Admin** (Администрирование учетных записей):</span><span class="sxs-lookup"><span data-stu-id="7446f-174">In the bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="7446f-176">В разделе администрирования Wdesk откройте **Security** (Безопасность), затем **SAML** > **SAML Settings** (Параметры SAML):</span><span class="sxs-lookup"><span data-stu-id="7446f-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="7446f-178">В разделе **General Settings** (Общие параметры) установите флажок **Enable SAML Single Sign On** (Включить единый вход SAML):</span><span class="sxs-lookup"><span data-stu-id="7446f-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="7446f-180">В разделе **Service Provider Details** (Сведения о поставщике SAML) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7446f-180">Under **Service Provider Details**, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="7446f-182">а.</span><span class="sxs-lookup"><span data-stu-id="7446f-182">a.</span></span> <span data-ttu-id="7446f-183">Скопируйте значение **Login URL** (URL-адрес входа) и вставьте его в текстовое поле **URL-адрес входа** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7446f-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="7446f-184">b.</span><span class="sxs-lookup"><span data-stu-id="7446f-184">b.</span></span> <span data-ttu-id="7446f-185">Скопируйте значение **Metadata Url** (URL-адрес метаданных) и вставьте его в текстовое поле **Идентификатор** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7446f-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="7446f-186">c.</span><span class="sxs-lookup"><span data-stu-id="7446f-186">c.</span></span> <span data-ttu-id="7446f-187">Скопируйте значение **Consumer URL** (URL-адрес потребителя) и вставьте его в текстовое поле **URL-адрес ответа** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7446f-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="7446f-188">г)</span><span class="sxs-lookup"><span data-stu-id="7446f-188">d.</span></span> <span data-ttu-id="7446f-189">На портале Azure нажмите кнопку **Сохранить**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="7446f-189">Click **Save** on Azure portal to save the changes.</span></span>      

12. <span data-ttu-id="7446f-190">Щелкните **Configure IdP Settings** (Настройка параметров поставщика удостоверений), чтобы открыть диалоговое окно **изменения параметров поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="7446f-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="7446f-191">Щелкните **Choose File** (Выбрать файл) и найдите файл **Metadata.xml**, который вы сохранили с портала Azure, а затем отправьте его.</span><span class="sxs-lookup"><span data-stu-id="7446f-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="7446f-193">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="7446f-193">Click **Save changes**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="7446f-195">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="7446f-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7446f-196">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="7446f-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7446f-197">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="7446f-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7446f-198">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7446f-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="7446f-199">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7446f-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7446f-201">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7446f-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7446f-202">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7446f-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7446f-204">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7446f-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7446f-206">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7446f-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7446f-208">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7446f-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7446f-210">а.</span><span class="sxs-lookup"><span data-stu-id="7446f-210">a.</span></span> <span data-ttu-id="7446f-211">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7446f-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7446f-212">b.</span><span class="sxs-lookup"><span data-stu-id="7446f-212">b.</span></span> <span data-ttu-id="7446f-213">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7446f-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7446f-214">c.</span><span class="sxs-lookup"><span data-stu-id="7446f-214">c.</span></span> <span data-ttu-id="7446f-215">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="7446f-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7446f-216">d.</span><span class="sxs-lookup"><span data-stu-id="7446f-216">d.</span></span> <span data-ttu-id="7446f-217">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7446f-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="7446f-218">Создание тестового пользователя Wdesk</span><span class="sxs-lookup"><span data-stu-id="7446f-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="7446f-219">Чтобы пользователи Azure AD могли выполнять вход в Wdesk, их следует подготовить в Wdesk.</span><span class="sxs-lookup"><span data-stu-id="7446f-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="7446f-220">В Wdesk подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="7446f-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="7446f-221">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="7446f-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7446f-222">Войдите в Wdesk с правами администратора безопасности.</span><span class="sxs-lookup"><span data-stu-id="7446f-222">Log in to Wdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="7446f-223">Последовательно выберите **Admin** (Администрирование)  > **Account Admin** (Администрирование учетных записей).</span><span class="sxs-lookup"><span data-stu-id="7446f-223">Navigate to **Admin** > **Account Admin**.</span></span>

     ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="7446f-225">Щелкните элемент **Members** (Участники) в разделе **People** (Люди).</span><span class="sxs-lookup"><span data-stu-id="7446f-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="7446f-226">Теперь щелкните **Add Member** (Добавить участника), чтобы открыть диалоговое окно **Add Member** (Добавление участника).</span><span class="sxs-lookup"><span data-stu-id="7446f-226">Now click **Add Member** to open **Add Member** dialog box.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="7446f-228">В текстовое поле **User** (Пользователь) введите имя пользователя, например **brittasimon@contoso.com**, и нажмите кнопку **Continue** (Продолжить).</span><span class="sxs-lookup"><span data-stu-id="7446f-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="7446f-230">Введите необходимые данные, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="7446f-230">Enter the details as shown below:</span></span>
  
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="7446f-232">а.</span><span class="sxs-lookup"><span data-stu-id="7446f-232">a.</span></span> <span data-ttu-id="7446f-233">В текстовое поле **E-mail** (Адрес электронной почты) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="7446f-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="7446f-234">b.</span><span class="sxs-lookup"><span data-stu-id="7446f-234">b.</span></span> <span data-ttu-id="7446f-235">В текстовое поле **First Name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7446f-235">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="7446f-236">c.</span><span class="sxs-lookup"><span data-stu-id="7446f-236">c.</span></span> <span data-ttu-id="7446f-237">В текстовое поле **Last Name** (Фамилия) введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7446f-237">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

7. <span data-ttu-id="7446f-238">Щелкните кнопку **Save Member** (Сохранить участника).</span><span class="sxs-lookup"><span data-stu-id="7446f-238">Click **Save Member** button.</span></span>  

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7446f-240">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7446f-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7446f-241">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Wdesk.</span><span class="sxs-lookup"><span data-stu-id="7446f-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7446f-243">**Назначение пользователя Britta Simon приложению Wdesk**</span><span class="sxs-lookup"><span data-stu-id="7446f-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="7446f-244">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7446f-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7446f-246">В списке приложений выберите **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="7446f-246">In the applications list, select **Wdesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="7446f-248">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7446f-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7446f-250">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7446f-250">Click **Add** button.</span></span> <span data-ttu-id="7446f-251">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7446f-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7446f-253">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7446f-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7446f-254">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7446f-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7446f-255">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7446f-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7446f-256">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7446f-256">Testing single sign-on</span></span>

<span data-ttu-id="7446f-257">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7446f-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7446f-258">Щелкнув плитку Wdesk на панели доступа, вы автоматически войдете в приложение Wdesk.</span><span class="sxs-lookup"><span data-stu-id="7446f-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span></span>
<span data-ttu-id="7446f-259">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7446f-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7446f-260">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7446f-260">Additional resources</span></span>

* [<span data-ttu-id="7446f-261">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7446f-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7446f-262">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7446f-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

