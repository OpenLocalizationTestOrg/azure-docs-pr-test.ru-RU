---
title: "Руководство по интеграции Azure Active Directory с Moxtra | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="ae76c-103">Учебник. Интеграция Azure Active Directory с Moxtra</span><span class="sxs-lookup"><span data-stu-id="ae76c-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="ae76c-104">В этом руководстве описано, как интегрировать Moxtra с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae76c-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae76c-105">Интеграция Azure AD с приложением Moxtra обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="ae76c-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae76c-106">С помощью Azure AD вы можете контролировать доступ к Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ae76c-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="ae76c-107">Вы можете включить автоматический вход пользователей в Moxtra (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae76c-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae76c-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ae76c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae76c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae76c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae76c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ae76c-110">Prerequisites</span></span>

<span data-ttu-id="ae76c-111">Чтобы настроить интеграцию Azure AD с Moxtra, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ae76c-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="ae76c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ae76c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae76c-113">подписка Moxtra с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ae76c-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae76c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ae76c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae76c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ae76c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae76c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ae76c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae76c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae76c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae76c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ae76c-118">Scenario description</span></span>
<span data-ttu-id="ae76c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ae76c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae76c-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ae76c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae76c-121">Добавление Moxtra из коллекции</span><span class="sxs-lookup"><span data-stu-id="ae76c-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="ae76c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae76c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="ae76c-123">Добавление Moxtra из коллекции</span><span class="sxs-lookup"><span data-stu-id="ae76c-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="ae76c-124">Чтобы настроить интеграцию Moxtra с Azure AD, необходимо добавить Moxtra из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ae76c-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae76c-125">**Чтобы добавить Moxtra из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ae76c-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae76c-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae76c-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae76c-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ae76c-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ae76c-133">В поле поиска введите **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-133">In the search box, type **Moxtra**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="ae76c-135">На панели результатов выберите **Moxtra** и щелкните **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ae76c-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae76c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae76c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae76c-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение Moxtra с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae76c-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae76c-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Moxtra соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae76c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="ae76c-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ae76c-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="ae76c-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ae76c-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae76c-142">Чтобы настроить и проверить единый вход Azure AD в Moxtra, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ae76c-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae76c-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ae76c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae76c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae76c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae76c-145">**[Создание тестового пользователя Moxtra](#creating-a-moxtra-test-user)** требуется для создания в Moxtra пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae76c-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae76c-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae76c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae76c-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ae76c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae76c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae76c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae76c-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ae76c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="ae76c-150">**Чтобы настроить единый вход Azure AD в Moxtra, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ae76c-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="ae76c-151">На портале Azure на странице интеграции с приложением **Moxtra** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ae76c-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ae76c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="ae76c-155">В разделе **Домены и URL-адреса приложения Moxtra** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ae76c-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="ae76c-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в формате `https://www.moxtra.com/service/#login`.</span><span class="sxs-lookup"><span data-stu-id="ae76c-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="ae76c-158">Приложение Moxtra ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="ae76c-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ae76c-159">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="ae76c-159">Configure the following claims for this application.</span></span> <span data-ttu-id="ae76c-160">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="ae76c-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ae76c-161">На следующем снимке экрана приведен пример конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ae76c-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="ae76c-163">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae76c-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="ae76c-164">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="ae76c-164">Attribute Name</span></span> | <span data-ttu-id="ae76c-165">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="ae76c-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ae76c-166">firstname</span><span class="sxs-lookup"><span data-stu-id="ae76c-166">firstname</span></span> | <span data-ttu-id="ae76c-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ae76c-167">user.givenname</span></span> |
    | <span data-ttu-id="ae76c-168">lastname</span><span class="sxs-lookup"><span data-stu-id="ae76c-168">lastname</span></span> | <span data-ttu-id="ae76c-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="ae76c-169">user.surname</span></span> |
    | <span data-ttu-id="ae76c-170">idpid</span><span class="sxs-lookup"><span data-stu-id="ae76c-170">idpid</span></span>    | <span data-ttu-id="ae76c-171">< идентификатор сущности SAML ></span><span class="sxs-lookup"><span data-stu-id="ae76c-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="ae76c-172">Значение атрибута **idpid** приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="ae76c-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="ae76c-173">Фактическое значение можно получить из раздела **Краткий справочник** в подразделе **Настройка Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="ae76c-174">а.</span><span class="sxs-lookup"><span data-stu-id="ae76c-174">a.</span></span> <span data-ttu-id="ae76c-175">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="ae76c-177">b.</span><span class="sxs-lookup"><span data-stu-id="ae76c-177">b.</span></span> <span data-ttu-id="ae76c-178">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ae76c-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ae76c-180">c.</span><span class="sxs-lookup"><span data-stu-id="ae76c-180">c.</span></span> <span data-ttu-id="ae76c-181">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ae76c-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="ae76c-182">г)</span><span class="sxs-lookup"><span data-stu-id="ae76c-182">d.</span></span> <span data-ttu-id="ae76c-183">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="ae76c-184">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ae76c-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="ae76c-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ae76c-186">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ae76c-188">В разделе **Настройка Moxtra** щелкните **Настроить Moxtra**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ae76c-189">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="ae76c-191">В другом окне браузера войдите на корпоративный веб-сайт Moxtra с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ae76c-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="ae76c-192">На панели инструментов слева щелкните **Консоль администрирования > Единый вход SAML**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="ae76c-194">На странице **SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae76c-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="ae76c-196">а.</span><span class="sxs-lookup"><span data-stu-id="ae76c-196">a.</span></span> <span data-ttu-id="ae76c-197">В текстовом поле **Имя** введите имя конфигурации (например, *SAML*).</span><span class="sxs-lookup"><span data-stu-id="ae76c-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="ae76c-198">b.</span><span class="sxs-lookup"><span data-stu-id="ae76c-198">b.</span></span> <span data-ttu-id="ae76c-199">В текстовое поле **Идентификатор сущности поставщика удостоверений** вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ae76c-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ae76c-200">c.</span><span class="sxs-lookup"><span data-stu-id="ae76c-200">c.</span></span> <span data-ttu-id="ae76c-201">В текстовое поле **URL-адрес входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ae76c-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ae76c-202">г)</span><span class="sxs-lookup"><span data-stu-id="ae76c-202">d.</span></span> <span data-ttu-id="ae76c-203">В текстовом поле **AuthnContextClassRef** введите **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="ae76c-204">д.</span><span class="sxs-lookup"><span data-stu-id="ae76c-204">e.</span></span> <span data-ttu-id="ae76c-205">В текстовом поле **NameID format** (Формат идентификатора имени) введите **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="ae76c-206">f.</span><span class="sxs-lookup"><span data-stu-id="ae76c-206">f.</span></span> <span data-ttu-id="ae76c-207">Откройте сертификат, который вы скачали на портале Azure, в блокноте, скопируйте содержимое и вставьте его в текстовое поле **Сертификат**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="ae76c-208">ж.</span><span class="sxs-lookup"><span data-stu-id="ae76c-208">g.</span></span> <span data-ttu-id="ae76c-209">В текстовом поле домена электронной почты SAML введите адрес вашего домена электронной почты SAML.</span><span class="sxs-lookup"><span data-stu-id="ae76c-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="ae76c-210">Чтобы просмотреть процедуру по проверке домена, щелкните пункт "**i**" ниже.</span><span class="sxs-lookup"><span data-stu-id="ae76c-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="ae76c-211">h.</span><span class="sxs-lookup"><span data-stu-id="ae76c-211">h.</span></span> <span data-ttu-id="ae76c-212">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="ae76c-213">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ae76c-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae76c-214">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ae76c-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae76c-215">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ae76c-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae76c-216">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae76c-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae76c-217">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae76c-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ae76c-219">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ae76c-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae76c-220">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae76c-222">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae76c-224">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae76c-226">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae76c-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae76c-228">а.</span><span class="sxs-lookup"><span data-stu-id="ae76c-228">a.</span></span> <span data-ttu-id="ae76c-229">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae76c-230">b.</span><span class="sxs-lookup"><span data-stu-id="ae76c-230">b.</span></span> <span data-ttu-id="ae76c-231">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae76c-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae76c-232">c.</span><span class="sxs-lookup"><span data-stu-id="ae76c-232">c.</span></span> <span data-ttu-id="ae76c-233">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae76c-234">d.</span><span class="sxs-lookup"><span data-stu-id="ae76c-234">d.</span></span> <span data-ttu-id="ae76c-235">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="ae76c-236">Создание тестового пользователя Moxtra</span><span class="sxs-lookup"><span data-stu-id="ae76c-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="ae76c-237">Цель этого раздела — создать пользователя с именем Britta Simon в Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ae76c-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="ae76c-238">**Чтобы создать пользователя с именем Britta Simon в Moxtra, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ae76c-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="ae76c-239">Выполните вход на веб-сайт компании Moxtra в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ae76c-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="ae76c-240">На панели инструментов слева щелкните **Admin Console (Консоль администрирования) > User Management (Управление пользователями)**, а затем нажмите кнопку **Add User** (Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="ae76c-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="ae76c-242">На странице **Добавление пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae76c-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="ae76c-243">а.</span><span class="sxs-lookup"><span data-stu-id="ae76c-243">a.</span></span> <span data-ttu-id="ae76c-244">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="ae76c-245">b.</span><span class="sxs-lookup"><span data-stu-id="ae76c-245">b.</span></span> <span data-ttu-id="ae76c-246">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="ae76c-247">c.</span><span class="sxs-lookup"><span data-stu-id="ae76c-247">c.</span></span> <span data-ttu-id="ae76c-248">В текстовом поле **Email** (Адрес электронной почты) введите адрес электронной почты пользователя Britta Simon, такой же как на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ae76c-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="ae76c-249">г)</span><span class="sxs-lookup"><span data-stu-id="ae76c-249">d.</span></span> <span data-ttu-id="ae76c-250">В текстовом поле **Подразделение** введите **Dev**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="ae76c-251">д.</span><span class="sxs-lookup"><span data-stu-id="ae76c-251">e.</span></span> <span data-ttu-id="ae76c-252">В поле **Отдел** введите **IT**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="ae76c-253">f.</span><span class="sxs-lookup"><span data-stu-id="ae76c-253">f.</span></span> <span data-ttu-id="ae76c-254">Выберите **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="ae76c-255">ж.</span><span class="sxs-lookup"><span data-stu-id="ae76c-255">g.</span></span> <span data-ttu-id="ae76c-256">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae76c-257">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae76c-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae76c-258">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ae76c-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ae76c-260">**Чтобы назначить пользователя Britta Simon в Moxtra, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ae76c-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="ae76c-261">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ae76c-263">В списке приложений выберите **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-263">In the applications list, select **Moxtra**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="ae76c-265">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ae76c-267">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-267">Click **Add** button.</span></span> <span data-ttu-id="ae76c-268">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ae76c-270">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae76c-271">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae76c-272">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ae76c-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae76c-273">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ae76c-273">Testing single sign-on</span></span>

<span data-ttu-id="ae76c-274">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ae76c-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae76c-275">Щелкнув плитку Moxtra на панели доступа, вы автоматически войдете в приложение Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ae76c-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="ae76c-276">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae76c-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae76c-277">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ae76c-277">Additional resources</span></span>

* [<span data-ttu-id="ae76c-278">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae76c-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae76c-279">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae76c-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

