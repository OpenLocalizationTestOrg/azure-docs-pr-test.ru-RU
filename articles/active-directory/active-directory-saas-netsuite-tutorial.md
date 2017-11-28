---
title: "Руководство по интеграции Azure Active Directory с NetSuite | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="a7a29-103">Руководство по интеграции Azure Active Directory с NetSuite</span><span class="sxs-lookup"><span data-stu-id="a7a29-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="a7a29-104">В этом руководстве описано, как интегрировать Netsuite с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7a29-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7a29-105">Интеграция Azure AD с приложением Netsuite обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a7a29-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7a29-106">С помощью Azure AD вы можете контролировать доступ к Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="a7a29-107">Вы можете включить автоматический вход пользователей в Netsuite (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a29-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7a29-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a7a29-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7a29-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7a29-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7a29-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7a29-110">Prerequisites</span></span>

<span data-ttu-id="a7a29-111">Чтобы настроить интеграцию Azure AD с Netsuite, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a7a29-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="a7a29-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a7a29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7a29-113">подписка Netsuite с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7a29-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7a29-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a7a29-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7a29-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a7a29-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7a29-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a7a29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7a29-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7a29-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7a29-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a7a29-118">Scenario description</span></span>
<span data-ttu-id="a7a29-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a7a29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7a29-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a7a29-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7a29-121">Добавление Workrite из коллекции.</span><span class="sxs-lookup"><span data-stu-id="a7a29-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="a7a29-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="a7a29-123">Добавление Workrite из коллекции</span><span class="sxs-lookup"><span data-stu-id="a7a29-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="a7a29-124">Чтобы настроить интеграцию Netsuite с Azure AD, необходимо добавить Netsuite из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a7a29-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7a29-125">**Чтобы добавить Netsuite из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a7a29-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7a29-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7a29-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7a29-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a7a29-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a7a29-133">В поле поиска введите **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-133">In the search box, type **Netsuite**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="a7a29-135">На панели результатов выберите **Netsuite** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="a7a29-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7a29-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7a29-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Netsuite с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7a29-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a7a29-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Netsuite соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a29-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="a7a29-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="a7a29-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="a7a29-142">Чтобы настроить и проверить единый вход Azure AD в Netsuite, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="a7a29-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7a29-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a7a29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7a29-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7a29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7a29-145">**[Создание тестового пользователя Netsuite](#creating-a-netsuite-test-user)** требуется для того, чтобы в Netsuite существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a29-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7a29-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a29-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7a29-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a7a29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7a29-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7a29-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="a7a29-150">**Чтобы настроить единый вход Azure AD в Netsuite, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a7a29-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="a7a29-151">На портале Azure на странице интеграции с приложением **Netsuite** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a7a29-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7a29-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="a7a29-155">В разделе **Домены и URL-адреса приложения Netsuite** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="a7a29-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="a7a29-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`.</span><span class="sxs-lookup"><span data-stu-id="a7a29-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7a29-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="a7a29-158">This value is not real value.</span></span> <span data-ttu-id="a7a29-159">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="a7a29-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="a7a29-160">Чтобы получить это значение, обратитесь к [группе поддержки Netsuite](http://www.netsuite.com/portal/services/support.shtml).</span><span class="sxs-lookup"><span data-stu-id="a7a29-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="a7a29-161">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a7a29-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="a7a29-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a7a29-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7a29-165">В разделе **Конфигурация Netsuite** щелкните **Настроить Netsuite**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a7a29-166">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="a7a29-168">Откройте новую вкладку в браузере и войдите как администратор корпоративного сайта NetSuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="a7a29-169">На панели инструментов в верхней части страницы щелкните **Setup** (Настройка) и выберите **Setup Manager** (Диспетчер настройки).</span><span class="sxs-lookup"><span data-stu-id="a7a29-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="a7a29-171">Из списка **Setup Tasks** (Задачи настройки) выберите пункт **Integration** (Интеграция).</span><span class="sxs-lookup"><span data-stu-id="a7a29-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="a7a29-173">В разделе **Manage Authentication** (Управление аутентификацией) щелкните **SAML Single Sign-on** (Единый вход на основе SAML).</span><span class="sxs-lookup"><span data-stu-id="a7a29-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="a7a29-175">На странице **Настройка SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a7a29-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="a7a29-176">а.</span><span class="sxs-lookup"><span data-stu-id="a7a29-176">a.</span></span> <span data-ttu-id="a7a29-177">Скопируйте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML) из раздела **Краткий справочник** на странице **Настройка единого входа** и вставьте его в поле **Identity Provider Login Page** (Страница входа поставщика удостоверений) в Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="a7a29-179">b.</span><span class="sxs-lookup"><span data-stu-id="a7a29-179">b.</span></span> <span data-ttu-id="a7a29-180">В NetSuite выберите раздел **Primary Authentication Method** (Основной метод проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="a7a29-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="a7a29-181">c.</span><span class="sxs-lookup"><span data-stu-id="a7a29-181">c.</span></span> <span data-ttu-id="a7a29-182">В поле **SAMLV2 Identity Provider Metadata** (Метаданные поставщика удостоверений на основе SAMLv2) выберите **Upload IDP Metadata File** (Передать файл метаданных поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="a7a29-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="a7a29-183">Затем нажмите кнопку **Обзор**, чтобы добавить файл метаданных, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a7a29-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="a7a29-185">г)</span><span class="sxs-lookup"><span data-stu-id="a7a29-185">d.</span></span> <span data-ttu-id="a7a29-186">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="a7a29-186">Click **Submit**.</span></span>

12. <span data-ttu-id="a7a29-187">В Azure AD установите флажок **Просмотреть и изменить все другие атрибуты пользователей** и добавьте атрибут.</span><span class="sxs-lookup"><span data-stu-id="a7a29-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="a7a29-189">В поле **Имя атрибута** введите `account`.</span><span class="sxs-lookup"><span data-stu-id="a7a29-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="a7a29-190">В поле **Attribute Value** (Значение атрибута) введите идентификатор учетной записи Netsuite. Это значение является константой, которая изменяется вместе с учетной записью.</span><span class="sxs-lookup"><span data-stu-id="a7a29-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="a7a29-191">Инструкции по поиску идентификатора учетной записи приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="a7a29-191">Instructions on how to find your account ID are included below:</span></span>

      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="a7a29-193">а.</span><span class="sxs-lookup"><span data-stu-id="a7a29-193">a.</span></span> <span data-ttu-id="a7a29-194">В верхнем меню навигации NetSuite щелкните **Setup** (Настройка).</span><span class="sxs-lookup"><span data-stu-id="a7a29-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="a7a29-195">b.</span><span class="sxs-lookup"><span data-stu-id="a7a29-195">b.</span></span> <span data-ttu-id="a7a29-196">Щелкните **Setup Tasks** (Задачи настройки) в меню навигации слева, выберите раздел **Integration** (Интеграция), а затем щелкните **Web Services Preferences** (Параметры веб-служб).</span><span class="sxs-lookup"><span data-stu-id="a7a29-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="a7a29-197">c.</span><span class="sxs-lookup"><span data-stu-id="a7a29-197">c.</span></span> <span data-ttu-id="a7a29-198">Скопируйте идентификатор своей учетной записи NetSuite и вставьте его в поле **Значение атрибута** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a29-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="a7a29-200">Прежде чем пользователи смогут выполнять единый вход в NetSuite, необходимо назначить им соответствующие разрешения в NetSuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="a7a29-201">Чтобы предоставить необходимые разрешения, выполните следующие инструкции.</span><span class="sxs-lookup"><span data-stu-id="a7a29-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="a7a29-202">а.</span><span class="sxs-lookup"><span data-stu-id="a7a29-202">a.</span></span> <span data-ttu-id="a7a29-203">В верхнем меню навигации выберите **Setup** (Настройка) и щелкните **Setup Manager** (Диспетчер настройки).</span><span class="sxs-lookup"><span data-stu-id="a7a29-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="a7a29-205">b.</span><span class="sxs-lookup"><span data-stu-id="a7a29-205">b.</span></span> <span data-ttu-id="a7a29-206">В меню навигации слева выберите **Users/Roles** (Пользователи и роли), а затем — **Manage Roles** (Управление ролями).</span><span class="sxs-lookup"><span data-stu-id="a7a29-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="a7a29-208">c.</span><span class="sxs-lookup"><span data-stu-id="a7a29-208">c.</span></span> <span data-ttu-id="a7a29-209">Нажмите кнопку **Создать роль**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-209">Click **New Role**.</span></span>

    <span data-ttu-id="a7a29-210">г)</span><span class="sxs-lookup"><span data-stu-id="a7a29-210">d.</span></span> <span data-ttu-id="a7a29-211">Введите **имя** новой роли и установите флажок **Single Sign-On Only** (Только единый вход).</span><span class="sxs-lookup"><span data-stu-id="a7a29-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="a7a29-213">д.</span><span class="sxs-lookup"><span data-stu-id="a7a29-213">e.</span></span> <span data-ttu-id="a7a29-214">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-214">Click **Save**.</span></span>

    <span data-ttu-id="a7a29-215">f.</span><span class="sxs-lookup"><span data-stu-id="a7a29-215">f.</span></span> <span data-ttu-id="a7a29-216">В верхнем меню щелкните **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="a7a29-217">Затем щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-217">Then click **Setup**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="a7a29-219">g.</span><span class="sxs-lookup"><span data-stu-id="a7a29-219">g.</span></span> <span data-ttu-id="a7a29-220">Выберите **Set Up SAM Single Sign-on** (Настройка единого входа управления лицензиями) и нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="a7a29-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="a7a29-221">h.</span><span class="sxs-lookup"><span data-stu-id="a7a29-221">h.</span></span> <span data-ttu-id="a7a29-222">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-222">Click **Save**.</span></span>

    <span data-ttu-id="a7a29-223">i.</span><span class="sxs-lookup"><span data-stu-id="a7a29-223">i.</span></span> <span data-ttu-id="a7a29-224">В верхнем меню навигации выберите **Setup** (Настройка) и щелкните **Setup Manager** (Диспетчер настройки).</span><span class="sxs-lookup"><span data-stu-id="a7a29-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="a7a29-226">j.</span><span class="sxs-lookup"><span data-stu-id="a7a29-226">j.</span></span> <span data-ttu-id="a7a29-227">В меню навигации слева выберите **Users/Roles** (Пользователи и роли), а затем — **Manage Users** (Управление пользователями).</span><span class="sxs-lookup"><span data-stu-id="a7a29-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="a7a29-229">k.</span><span class="sxs-lookup"><span data-stu-id="a7a29-229">k.</span></span> <span data-ttu-id="a7a29-230">Выберите тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="a7a29-230">Select a test user.</span></span> <span data-ttu-id="a7a29-231">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-231">Then click **Edit**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="a7a29-233">l.</span><span class="sxs-lookup"><span data-stu-id="a7a29-233">l.</span></span> <span data-ttu-id="a7a29-234">В диалоговом окне "Роли" выберите роль, которую вы создали, и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Настройка единого входа](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="a7a29-236">m.</span><span class="sxs-lookup"><span data-stu-id="a7a29-236">m.</span></span> <span data-ttu-id="a7a29-237">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="a7a29-238">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a7a29-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7a29-239">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a7a29-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7a29-240">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a7a29-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7a29-241">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a29-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7a29-242">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7a29-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a7a29-244">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a7a29-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7a29-245">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="a7a29-247">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7a29-249">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7a29-251">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a7a29-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7a29-253">а.</span><span class="sxs-lookup"><span data-stu-id="a7a29-253">a.</span></span> <span data-ttu-id="a7a29-254">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7a29-255">b.</span><span class="sxs-lookup"><span data-stu-id="a7a29-255">b.</span></span> <span data-ttu-id="a7a29-256">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7a29-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7a29-257">c.</span><span class="sxs-lookup"><span data-stu-id="a7a29-257">c.</span></span> <span data-ttu-id="a7a29-258">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7a29-259">d.</span><span class="sxs-lookup"><span data-stu-id="a7a29-259">d.</span></span> <span data-ttu-id="a7a29-260">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="a7a29-261">Создание тестового пользователя Netsuite</span><span class="sxs-lookup"><span data-stu-id="a7a29-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="a7a29-262">В этом разделе вы создадите в Netsuite пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7a29-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="a7a29-263">Netsuite поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a7a29-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="a7a29-264">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="a7a29-264">There is no action item for you in this section.</span></span> <span data-ttu-id="a7a29-265">Если пользователь еще не существует в Netsuite, то он создается при попытке доступа к приложению Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7a29-266">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a29-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7a29-267">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Netsuite.</span><span class="sxs-lookup"><span data-stu-id="a7a29-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a7a29-269">**Чтобы назначить пользователя Britta Simon в Netsuite, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a7a29-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="a7a29-270">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a7a29-272">Из списка приложений выберите **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-272">In the applications list, select **Netsuite**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="a7a29-274">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a7a29-276">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-276">Click **Add** button.</span></span> <span data-ttu-id="a7a29-277">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a7a29-279">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7a29-280">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7a29-281">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7a29-282">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a7a29-282">Testing single sign-on</span></span>

<span data-ttu-id="a7a29-283">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a7a29-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7a29-284">Чтобы проверить параметры единого входа, откройте панель доступа по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com/), выполните вход с тестовой учетной записью и щелкните **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="a7a29-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7a29-285">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a7a29-285">Additional resources</span></span>

* [<span data-ttu-id="a7a29-286">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7a29-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7a29-287">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7a29-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a7a29-288">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="a7a29-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

