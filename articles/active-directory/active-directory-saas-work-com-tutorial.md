---
title: "Руководство. Интеграция Azure Active Directory с Work.com | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="3f083-103">Руководство. Интеграция Azure Active Directory с Work.com</span><span class="sxs-lookup"><span data-stu-id="3f083-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="3f083-104">В этом руководстве описано, как интегрировать Work.com с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f083-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f083-105">Интеграция Azure AD с приложением Work.com обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="3f083-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f083-106">С помощью Azure AD вы можете контролировать доступ к Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="3f083-107">Вы можете включить автоматический вход пользователей в Work.com (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f083-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f083-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3f083-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3f083-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f083-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f083-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3f083-110">Prerequisites</span></span>

<span data-ttu-id="3f083-111">Чтобы настроить интеграцию Azure AD с Work.com, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3f083-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="3f083-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3f083-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f083-113">Подписка Work.com с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3f083-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f083-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3f083-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f083-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3f083-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f083-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3f083-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f083-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f083-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f083-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3f083-118">Scenario description</span></span>
<span data-ttu-id="3f083-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3f083-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f083-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3f083-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f083-121">Добавление Work.com из коллекции</span><span class="sxs-lookup"><span data-stu-id="3f083-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="3f083-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f083-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="3f083-123">Добавление Work.com из коллекции</span><span class="sxs-lookup"><span data-stu-id="3f083-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="3f083-124">Чтобы настроить интеграцию Work.com с Azure AD, необходимо добавить Work.com из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3f083-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3f083-125">**Чтобы добавить Work.com из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="3f083-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3f083-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3f083-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f083-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3f083-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3f083-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3f083-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3f083-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3f083-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3f083-133">В поле поиска введите **Work.com**, выберите **Work.com** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="3f083-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Добавление из коллекции](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3f083-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f083-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3f083-136">В этом разделе описана настройка и проверка единого входа Azure AD в Work.com с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f083-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3f083-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Work.com соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f083-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="3f083-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="3f083-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3f083-140">Чтобы настроить и проверить единый вход Azure AD в Work.com, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="3f083-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3f083-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3f083-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3f083-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f083-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f083-143">**[Создание тестового пользователя Work.com](#create-a-workcom-test-user)** требуется для того, чтобы в Work.com существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f083-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f083-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f083-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f083-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3f083-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3f083-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f083-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3f083-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="3f083-148">Чтобы настроить единый вход, также необходимо пользовательское имя домена Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="3f083-149">Вам требуется определить по крайней мере одно имя домена, а также проверить и развернуть его для всей организации.</span><span class="sxs-lookup"><span data-stu-id="3f083-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="3f083-150">**Чтобы настроить единый вход Azure AD в Work.com, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="3f083-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="3f083-151">На портале Azure на странице интеграции с приложением **Work.com** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3f083-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3f083-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3f083-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="3f083-155">В разделе **Домены и URL-адреса приложения Work.com** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3f083-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Раздел "Домены и URL-адреса приложения Work.com"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="3f083-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="3f083-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3f083-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="3f083-158">This value is not real.</span></span> <span data-ttu-id="3f083-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="3f083-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3f083-160">Чтобы получить это значение, обратитесь к [группе поддержки клиентов Work.com](https://help.salesforce.com/articleView?id=000159855&type=3).</span><span class="sxs-lookup"><span data-stu-id="3f083-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="3f083-161">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3f083-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="3f083-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3f083-163">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3f083-165">В разделе **Настройка Work.com** щелкните **Настроить Work.com**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3f083-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3f083-166">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="3f083-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Раздел "Настройка Work.com"](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="3f083-168">Войдите в клиент Work.com от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="3f083-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="3f083-169">Перейдите в раздел **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="3f083-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="3f083-170">![Настройка](./media/active-directory-saas-work-com-tutorial/ic794108.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="3f083-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="3f083-171">В области навигации слева в разделе **Administer** (Администрирование) щелкните **Domain Management** (Управление доменами), чтобы развернуть соответствующий раздел, а затем щелкните **My Domain** (Мой домен), чтобы открыть страницу **My Domain** (Мой домен).</span><span class="sxs-lookup"><span data-stu-id="3f083-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="3f083-172">![Мой домен](./media/active-directory-saas-work-com-tutorial/ic767825.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="3f083-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="3f083-173">Чтобы проверить правильность настройки домена, убедитесь, что он находится на этапе **Step 4 Deployed to Users** (Шаг 4. Развернут для пользователей), и просмотрите раздел **My Domain Settings** (Параметры моего домена).</span><span class="sxs-lookup"><span data-stu-id="3f083-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="3f083-174">![Домен, развернутый для пользователя](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span><span class="sxs-lookup"><span data-stu-id="3f083-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="3f083-175">Войдите в клиент Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="3f083-176">Перейдите в раздел **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="3f083-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="3f083-177">![Настройка](./media/active-directory-saas-work-com-tutorial/ic794108.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="3f083-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="3f083-178">Разверните меню **Управление безопасностью**, а затем щелкните **Параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3f083-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="3f083-179">![Параметры единого входа](./media/active-directory-saas-work-com-tutorial/ic794113.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="3f083-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="3f083-180">На странице диалогового окна **Параметры единого входа** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3f083-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="3f083-181">![Включение SAML](./media/active-directory-saas-work-com-tutorial/ic781026.png "Включение SAML")</span><span class="sxs-lookup"><span data-stu-id="3f083-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="3f083-182">а.</span><span class="sxs-lookup"><span data-stu-id="3f083-182">a.</span></span> <span data-ttu-id="3f083-183">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="3f083-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="3f083-184">b.</span><span class="sxs-lookup"><span data-stu-id="3f083-184">b.</span></span> <span data-ttu-id="3f083-185">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3f083-185">Click **New**.</span></span>

15. <span data-ttu-id="3f083-186">В разделе **Параметры единого входа SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3f083-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="3f083-187">![Параметры единого входа SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="3f083-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="3f083-188">а.</span><span class="sxs-lookup"><span data-stu-id="3f083-188">a.</span></span> <span data-ttu-id="3f083-189">В текстовом поле **Имя** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3f083-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="3f083-190">При вводе значения в поле **Имя** текстовое поле **Имя API** заполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="3f083-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="3f083-191">b.</span><span class="sxs-lookup"><span data-stu-id="3f083-191">b.</span></span> <span data-ttu-id="3f083-192">В текстовое поле **Issuer** (Издатель) вставьте **идентификатор сущности SAML**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3f083-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="3f083-193">c.</span><span class="sxs-lookup"><span data-stu-id="3f083-193">c.</span></span> <span data-ttu-id="3f083-194">Чтобы отправить сертификат, скачанный с Azure AD, нажмите кнопку **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="3f083-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="3f083-195">d.</span><span class="sxs-lookup"><span data-stu-id="3f083-195">d.</span></span> <span data-ttu-id="3f083-196">В текстовое поле **Entity id** (Идентификатор сущности) введите `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="3f083-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="3f083-197">д.</span><span class="sxs-lookup"><span data-stu-id="3f083-197">e.</span></span> <span data-ttu-id="3f083-198">В поле **SAML Identity Type** (Тип удостоверения SAML) выберите значение **Assertion contains the Federation ID from the User object** (Проверочное утверждение содержит идентификатор федерации из объекта User).</span><span class="sxs-lookup"><span data-stu-id="3f083-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="3f083-199">Е.</span><span class="sxs-lookup"><span data-stu-id="3f083-199">f.</span></span> <span data-ttu-id="3f083-200">В поле **SAML Identity Location** (Расположение удостоверения SAML) выберите значение **Identity is in the NameIdentfier element of the Subject statement** (Удостоверение находится в элементе NameIdentifier оператора Subject).</span><span class="sxs-lookup"><span data-stu-id="3f083-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="3f083-201">g.</span><span class="sxs-lookup"><span data-stu-id="3f083-201">g.</span></span> <span data-ttu-id="3f083-202">В текстовое поле **Identity Provider Login URL** (URL-адрес входа IdP) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3f083-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3f083-203">h.</span><span class="sxs-lookup"><span data-stu-id="3f083-203">h.</span></span> <span data-ttu-id="3f083-204">В текстовое поле **Identity Provider Logout URL** (URL-адрес выхода IdP) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3f083-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="3f083-205">i.</span><span class="sxs-lookup"><span data-stu-id="3f083-205">i.</span></span> <span data-ttu-id="3f083-206">В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="3f083-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="3f083-207">j.</span><span class="sxs-lookup"><span data-stu-id="3f083-207">j.</span></span> <span data-ttu-id="3f083-208">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3f083-208">Click **Save**.</span></span>

16. <span data-ttu-id="3f083-209">В левой области навигации классического портала Work.com щелкните **Domain Management** (Управление доменами), чтобы развернуть соответствующий раздел, и щелкните **My Domain** (Мой домен), чтобы открыть страницу **My Domain** (Мой домен).</span><span class="sxs-lookup"><span data-stu-id="3f083-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="3f083-210">![Мой домен](./media/active-directory-saas-work-com-tutorial/ic794115.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="3f083-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="3f083-211">На странице **My Domain** (Мой домен) в разделе **Login Page Branding** (Фирменная символика страницы входа) нажмите кнопку **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="3f083-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="3f083-212">![Фирменная символика страницы входа](./media/active-directory-saas-work-com-tutorial/ic767826.png "Фирменная символика страницы входа")</span><span class="sxs-lookup"><span data-stu-id="3f083-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="3f083-213">На странице **Login Page Branding** (Фирменная символика страницы входа) в разделе **Authentication Service** (Служба аутентификации) отображается имя **SAML SSO Settings** (Параметры единого входа SAML).</span><span class="sxs-lookup"><span data-stu-id="3f083-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="3f083-214">Выберите его, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3f083-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="3f083-215">![Фирменная символика страницы входа](./media/active-directory-saas-work-com-tutorial/ic784366.png "Фирменная символика страницы входа")</span><span class="sxs-lookup"><span data-stu-id="3f083-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="3f083-216">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3f083-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3f083-217">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3f083-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3f083-218">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3f083-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3f083-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f083-219">Create an Azure AD test user</span></span>
<span data-ttu-id="3f083-220">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f083-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3f083-222">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3f083-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3f083-223">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3f083-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f083-225">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3f083-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Выберите "Пользователи и группы" > "Все пользователи".](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f083-227">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3f083-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Добавить](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f083-229">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3f083-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f083-231">а.</span><span class="sxs-lookup"><span data-stu-id="3f083-231">a.</span></span> <span data-ttu-id="3f083-232">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f083-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f083-233">b.</span><span class="sxs-lookup"><span data-stu-id="3f083-233">b.</span></span> <span data-ttu-id="3f083-234">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3f083-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f083-235">c.</span><span class="sxs-lookup"><span data-stu-id="3f083-235">c.</span></span> <span data-ttu-id="3f083-236">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3f083-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3f083-237">d.</span><span class="sxs-lookup"><span data-stu-id="3f083-237">d.</span></span> <span data-ttu-id="3f083-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3f083-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="3f083-239">Создание тестового пользователя Work.com</span><span class="sxs-lookup"><span data-stu-id="3f083-239">Create a Work.com test user</span></span>
<span data-ttu-id="3f083-240">Чтобы пользователи Azure Active Directory могли входить систему, их необходимо подготовить для Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="3f083-241">В случае с Work.com подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="3f083-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="3f083-242">Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3f083-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="3f083-243">Выполните вход на сайт компании Work.com в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="3f083-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="3f083-244">Перейдите в раздел **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="3f083-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="3f083-245">![Настройка](./media/active-directory-saas-work-com-tutorial/IC794108.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="3f083-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="3f083-246">Выберите **Manage Users \> Users** (Управление пользователями > Пользователи).</span><span class="sxs-lookup"><span data-stu-id="3f083-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="3f083-247">![Управление пользователями](./media/active-directory-saas-work-com-tutorial/IC784369.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="3f083-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="3f083-248">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="3f083-248">Click **New User**.</span></span>
   
    <span data-ttu-id="3f083-249">![Все пользователи](./media/active-directory-saas-work-com-tutorial/IC794117.png "Все пользователи")</span><span class="sxs-lookup"><span data-stu-id="3f083-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="3f083-250">В разделе "User Edit" (Изменение пользователя) выполните следующие действия, разместив в текстовые поля атрибуты действующей учетной записи Azure AD, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="3f083-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="3f083-251">![Изменение пользователя](./media/active-directory-saas-work-com-tutorial/ic794118.png "Изменение пользователя")</span><span class="sxs-lookup"><span data-stu-id="3f083-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="3f083-252">а.</span><span class="sxs-lookup"><span data-stu-id="3f083-252">a.</span></span> <span data-ttu-id="3f083-253">В текстовое поле **First Name** (Имя) введите **имя пользователя** (**Britta**).</span><span class="sxs-lookup"><span data-stu-id="3f083-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="3f083-254">b.</span><span class="sxs-lookup"><span data-stu-id="3f083-254">b.</span></span> <span data-ttu-id="3f083-255">В текстовое поле **Last Name** (Фамилия) введите **фамилию** (**Simon**).</span><span class="sxs-lookup"><span data-stu-id="3f083-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="3f083-256">c.</span><span class="sxs-lookup"><span data-stu-id="3f083-256">c.</span></span> <span data-ttu-id="3f083-257">В текстовое поле **Alias** (Альтернативное имя) введите **имя** пользователя (**BrittaS**).</span><span class="sxs-lookup"><span data-stu-id="3f083-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="3f083-258">d.</span><span class="sxs-lookup"><span data-stu-id="3f083-258">d.</span></span> <span data-ttu-id="3f083-259">В текстовое поле **Email** (Адрес электронной почты) введите **адрес электронной почты пользователя** (**Brittasimon@contoso.com**).</span><span class="sxs-lookup"><span data-stu-id="3f083-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="3f083-260">д.</span><span class="sxs-lookup"><span data-stu-id="3f083-260">e.</span></span> <span data-ttu-id="3f083-261">В текстовое поле **User Name** (Имя пользователя) введите имя пользователя (**Brittasimon@contoso.com**).</span><span class="sxs-lookup"><span data-stu-id="3f083-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="3f083-262">f.</span><span class="sxs-lookup"><span data-stu-id="3f083-262">f.</span></span> <span data-ttu-id="3f083-263">В текстовое поле **Nick Name** (Псевдоним) укажите **псевдоним** пользователя (**Simon**).</span><span class="sxs-lookup"><span data-stu-id="3f083-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="3f083-264">g.</span><span class="sxs-lookup"><span data-stu-id="3f083-264">g.</span></span> <span data-ttu-id="3f083-265">Выберите значения параметров **Role** (Роль), **User License** (Пользовательская лицензия) и **Profile** (Профиль).</span><span class="sxs-lookup"><span data-stu-id="3f083-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="3f083-266">h.</span><span class="sxs-lookup"><span data-stu-id="3f083-266">h.</span></span> <span data-ttu-id="3f083-267">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3f083-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="3f083-268">Владелец этой учетной записи Azure AD получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3f083-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3f083-269">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f083-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="3f083-270">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3f083-272">**Чтобы назначить пользователя Britta Simon в Work.com, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="3f083-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="3f083-273">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3f083-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3f083-275">В списке приложений выберите **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="3f083-275">In the applications list, select **Work.com**.</span></span>

    ![Work.com в списке приложений](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="3f083-277">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3f083-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3f083-279">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3f083-279">Click **Add** button.</span></span> <span data-ttu-id="3f083-280">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3f083-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3f083-282">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3f083-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3f083-283">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3f083-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f083-284">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3f083-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3f083-285">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3f083-285">Test single sign-on</span></span>

<span data-ttu-id="3f083-286">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3f083-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3f083-287">Щелкнув плитку Work.com на панели доступа, вы автоматически войдете в приложение Work.com.</span><span class="sxs-lookup"><span data-stu-id="3f083-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="3f083-288">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3f083-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f083-289">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3f083-289">Additional resources</span></span>

* [<span data-ttu-id="3f083-290">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f083-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f083-291">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f083-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

