---
title: "Учебник. Интеграция Azure Active Directory с Egnyte | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d01333b61e73c83588d2d1701c0c300df4ab1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="00039-103">Руководство. Интеграция Azure Active Directory с Egnyte</span><span class="sxs-lookup"><span data-stu-id="00039-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="00039-104">В этом руководстве описано, как интегрировать Egnyte с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="00039-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00039-105">Интеграция Egnyte c Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="00039-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="00039-106">Вы можете контролировать доступ к Egnyte с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="00039-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="00039-107">Вы можете включить автоматический вход пользователей в Egnyte (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00039-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="00039-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="00039-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="00039-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00039-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00039-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="00039-110">Prerequisites</span></span>

<span data-ttu-id="00039-111">Чтобы настроить интеграцию Azure AD с Egnyte, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="00039-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="00039-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="00039-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00039-113">Подписка с поддержкой единого входа Egnyte</span><span class="sxs-lookup"><span data-stu-id="00039-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00039-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="00039-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00039-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="00039-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00039-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="00039-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00039-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00039-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00039-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="00039-118">Scenario description</span></span>
<span data-ttu-id="00039-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="00039-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00039-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="00039-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00039-121">Добавление Egnyte из коллекции</span><span class="sxs-lookup"><span data-stu-id="00039-121">Adding Egnyte from the gallery</span></span>
2. <span data-ttu-id="00039-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00039-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="00039-123">Добавление Egnyte из коллекции</span><span class="sxs-lookup"><span data-stu-id="00039-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="00039-124">Чтобы настроить интеграцию Egnyte с Azure AD, необходимо добавить Egnyte из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="00039-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="00039-125">**Чтобы добавить Egnyte из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="00039-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="00039-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00039-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="00039-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="00039-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="00039-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00039-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="00039-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="00039-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="00039-133">В поле поиска введите **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="00039-133">In the search box, type **Egnyte**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="00039-135">На панели результатов выберите **Egnyte** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="00039-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="00039-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00039-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="00039-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Egnyte для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00039-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="00039-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Egnyte соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00039-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="00039-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Egnyte.</span><span class="sxs-lookup"><span data-stu-id="00039-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="00039-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Egnyte.</span><span class="sxs-lookup"><span data-stu-id="00039-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="00039-142">Чтобы настроить и проверить единый вход Azure AD в Egnyte, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="00039-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="00039-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="00039-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="00039-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00039-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00039-145">**[Создание тестового пользователя Egnyte](#creating-an-egnyte-test-user)** требуется для создания пользователя Britta Simon в Egnyte, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00039-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="00039-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00039-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00039-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="00039-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="00039-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00039-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="00039-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Egnyte.</span><span class="sxs-lookup"><span data-stu-id="00039-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="00039-150">**Чтобы настроить единый вход Azure AD в Egnyte, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="00039-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="00039-151">На портале Azure на странице интеграции с приложением **Egnyte** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="00039-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="00039-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="00039-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="00039-155">В разделе **Домены и URL-адреса Egnyte** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="00039-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="00039-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="00039-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="00039-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="00039-158">This value is not real.</span></span> <span data-ttu-id="00039-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="00039-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="00039-160">Для получения этого значения обратитесь в [службу поддержки клиентов Egnyte](https://www.egnyte.com/corp/contact_egnyte.html).</span><span class="sxs-lookup"><span data-stu-id="00039-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
4. <span data-ttu-id="00039-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="00039-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="00039-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="00039-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="00039-165">В разделе **Настройка Egnyte** щелкните **Настроить Egnyte**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="00039-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="00039-166">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="00039-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="00039-168">В другом окне браузера войдите на корпоративный веб-сайт Egnyte в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="00039-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="00039-169">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="00039-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="00039-170">![Параметры](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="00039-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="00039-171">В меню выберите пункт **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="00039-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="00039-172">![Параметры](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="00039-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="00039-173">Откройте вкладку **Configuration** (Конфигурация) и нажмите элемент **Security** (Безопасность).</span><span class="sxs-lookup"><span data-stu-id="00039-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="00039-174">![Безопасность](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="00039-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="00039-175">В разделе **Проверка подлинности единого входа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="00039-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="00039-176">![Аутентификация единого входа](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Аутентификация единого входа")</span><span class="sxs-lookup"><span data-stu-id="00039-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="00039-177">а.</span><span class="sxs-lookup"><span data-stu-id="00039-177">a.</span></span> <span data-ttu-id="00039-178">Выберите для параметра **Single sign-on authentication** (Аутентификация единого входа) значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="00039-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="00039-179">b.</span><span class="sxs-lookup"><span data-stu-id="00039-179">b.</span></span> <span data-ttu-id="00039-180">Выберите для параметра **Identity provider** (Поставщик удостоверений) значение **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="00039-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="00039-181">c.</span><span class="sxs-lookup"><span data-stu-id="00039-181">c.</span></span> <span data-ttu-id="00039-182">Вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure, в поле **URL-адрес входа поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="00039-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="00039-183">г)</span><span class="sxs-lookup"><span data-stu-id="00039-183">d.</span></span> <span data-ttu-id="00039-184">Вставьте значение **Идентификатора сущности SAML**, скопированное на портале Azure, в поле **Идентификатор сущности поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="00039-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="00039-185">д.</span><span class="sxs-lookup"><span data-stu-id="00039-185">e.</span></span> <span data-ttu-id="00039-186">Откройте в блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Сертификат поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="00039-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="00039-187">f.</span><span class="sxs-lookup"><span data-stu-id="00039-187">f.</span></span> <span data-ttu-id="00039-188">Выберите для параметра **Default user mapping** (Сопоставление пользователя по умолчанию) значение **Email address** (Адрес электронной почты).</span><span class="sxs-lookup"><span data-stu-id="00039-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="00039-189">ж.</span><span class="sxs-lookup"><span data-stu-id="00039-189">g.</span></span> <span data-ttu-id="00039-190">Выберите для параметра **Use domain-specific issuer value** (Использовать значение издателя домена) значение **disabled** (отключено).</span><span class="sxs-lookup"><span data-stu-id="00039-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="00039-191">h.</span><span class="sxs-lookup"><span data-stu-id="00039-191">h.</span></span> <span data-ttu-id="00039-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="00039-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="00039-193">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="00039-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="00039-194">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="00039-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="00039-195">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="00039-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="00039-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="00039-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="00039-197">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00039-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="00039-199">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="00039-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="00039-200">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00039-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00039-202">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="00039-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00039-204">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00039-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00039-206">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="00039-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="00039-208">а.</span><span class="sxs-lookup"><span data-stu-id="00039-208">a.</span></span> <span data-ttu-id="00039-209">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="00039-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00039-210">b.</span><span class="sxs-lookup"><span data-stu-id="00039-210">b.</span></span> <span data-ttu-id="00039-211">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="00039-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="00039-212">c.</span><span class="sxs-lookup"><span data-stu-id="00039-212">c.</span></span> <span data-ttu-id="00039-213">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="00039-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="00039-214">d.</span><span class="sxs-lookup"><span data-stu-id="00039-214">d.</span></span> <span data-ttu-id="00039-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="00039-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="00039-216">Создание тестового пользователя Egnyte</span><span class="sxs-lookup"><span data-stu-id="00039-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="00039-217">Чтобы пользователи Azure AD могли выполнять вход в Egnyte, они должны быть подготовлены для Egnyte.</span><span class="sxs-lookup"><span data-stu-id="00039-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="00039-218">В случае с Egnyte подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="00039-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="00039-219">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="00039-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="00039-220">Войдите на корпоративный веб-сайт **Egnyte** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="00039-220">Log in to your **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="00039-221">Последовательно выберите пункты **Settings \> Users & Groups** (Параметры > Пользователи и группы).</span><span class="sxs-lookup"><span data-stu-id="00039-221">Go to **Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="00039-222">Нажмите **Добавить пользователя**, а затем выберите тип для пользователя, которого желаете добавить.</span><span class="sxs-lookup"><span data-stu-id="00039-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="00039-223">![Пользователи](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="00039-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="00039-224">В разделе **Новый обычный пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="00039-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="00039-225">![Новый обычный пользователь](./media/active-directory-saas-egnyte-tutorial/ic787825.png "Новый обычный пользователь")</span><span class="sxs-lookup"><span data-stu-id="00039-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="00039-226">а.</span><span class="sxs-lookup"><span data-stu-id="00039-226">a.</span></span> <span data-ttu-id="00039-227">Введите значения **Адрес электронной почты**, **Имя пользователя** и другие данные действительной учетной записи Azure Active Directory, которую хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="00039-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="00039-228">b.</span><span class="sxs-lookup"><span data-stu-id="00039-228">b.</span></span> <span data-ttu-id="00039-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="00039-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="00039-230">Владелец учетной записи Azure Active Directory получит уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="00039-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="00039-231">Вы можете использовать любые другие средства создания учетной записи пользователя Egnyte или API, предоставляемые Egnyte для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="00039-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="00039-232">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="00039-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="00039-233">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к Egnyte.</span><span class="sxs-lookup"><span data-stu-id="00039-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="00039-235">**Чтобы назначить пользователя Britta Simon для приложения Egnyte, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="00039-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="00039-236">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00039-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="00039-238">В списке приложений выберите **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="00039-238">In the applications list, select **Egnyte**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="00039-240">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="00039-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="00039-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00039-242">Click **Add** button.</span></span> <span data-ttu-id="00039-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="00039-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="00039-245">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="00039-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="00039-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="00039-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00039-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="00039-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="00039-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="00039-248">Testing single sign-on</span></span>

<span data-ttu-id="00039-249">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="00039-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="00039-250">Щелкнув элемент Egnyte на панели доступа, вы автоматически войдете в приложение Egnyte.</span><span class="sxs-lookup"><span data-stu-id="00039-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="00039-251">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00039-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="00039-252">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="00039-252">Additional resources</span></span>

* [<span data-ttu-id="00039-253">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00039-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00039-254">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="00039-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

