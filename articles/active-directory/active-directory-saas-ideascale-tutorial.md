---
title: "Учебник. Интеграция Azure Active Directory с IdeaScale | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="ffea5-103">Руководство. Интеграция Azure Active Directory с IdeaScale</span><span class="sxs-lookup"><span data-stu-id="ffea5-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="ffea5-104">В этом руководстве описано, как интегрировать IdeaScale с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ffea5-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ffea5-105">Интеграция Azure AD с приложением IdeaScale обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ffea5-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ffea5-106">С помощью Azure AD вы можете контролировать доступ к IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="ffea5-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="ffea5-107">Вы можете включить автоматический вход пользователей в IdeaScale (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffea5-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ffea5-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ffea5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ffea5-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ffea5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffea5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ffea5-110">Prerequisites</span></span>

<span data-ttu-id="ffea5-111">Чтобы настроить интеграцию Azure AD с IdeaScale, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ffea5-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="ffea5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ffea5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ffea5-113">подписка IdeaScale с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ffea5-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ffea5-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ffea5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ffea5-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ffea5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ffea5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ffea5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ffea5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffea5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ffea5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ffea5-118">Scenario description</span></span>
<span data-ttu-id="ffea5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ffea5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ffea5-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ffea5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ffea5-121">Добавление IdeaScale из коллекции</span><span class="sxs-lookup"><span data-stu-id="ffea5-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="ffea5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffea5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="ffea5-123">Добавление IdeaScale из коллекции</span><span class="sxs-lookup"><span data-stu-id="ffea5-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="ffea5-124">Чтобы настроить интеграцию IdeaScale с Azure AD, необходимо добавить IdeaScale из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ffea5-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ffea5-125">**Чтобы добавить IdeaScale из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ffea5-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ffea5-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ffea5-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ffea5-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ffea5-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ffea5-133">В поле поиска введите **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-133">In the search box, type **IdeaScale**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="ffea5-135">На панели результатов выберите **IdeaScale** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ffea5-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ffea5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffea5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ffea5-138">В этом разделе описана настройка и проверка единого входа Azure AD в IdeaScale с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffea5-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ffea5-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в IdeaScale соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffea5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="ffea5-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="ffea5-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="ffea5-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="ffea5-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ffea5-142">Чтобы настроить и проверить единый вход Azure AD в IdeaScale, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="ffea5-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ffea5-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ffea5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ffea5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffea5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ffea5-145">**[Создание тестового пользователя IdeaScale](#creating-an-ideascale-test-user)** требуется для создания в IdeaScale пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffea5-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ffea5-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffea5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ffea5-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ffea5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ffea5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffea5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ffea5-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="ffea5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="ffea5-150">**Чтобы настроить единый вход Azure AD в IdeaScale, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ffea5-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="ffea5-151">На портале Azure на странице интеграции с приложением **IdeaScale** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ffea5-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ffea5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="ffea5-155">В разделе **Домены и URL-адреса приложения IdeaScale** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ffea5-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="ffea5-157">а.</span><span class="sxs-lookup"><span data-stu-id="ffea5-157">a.</span></span> <span data-ttu-id="ffea5-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="ffea5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="ffea5-159">b.</span><span class="sxs-lookup"><span data-stu-id="ffea5-159">b.</span></span> <span data-ttu-id="ffea5-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="ffea5-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="ffea5-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ffea5-161">These values are not real.</span></span> <span data-ttu-id="ffea5-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="ffea5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ffea5-163">Чтобы получить их, обратитесь в [службу поддержки клиентов IdeaScale](http://support.ideascale.com/).</span><span class="sxs-lookup"><span data-stu-id="ffea5-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="ffea5-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ffea5-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="ffea5-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ffea5-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ffea5-168">В разделе **Конфигурация IdeaScale** щелкните **Настроить IdeaScale**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ffea5-169">Скопируйте **URL-адрес выхода и идентификатор сущности SAM** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="ffea5-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт IdeaScale в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ffea5-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="ffea5-172">Выберите **Параметры сообщества**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="ffea5-173">![Параметры сообщества](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Параметры сообщества")</span><span class="sxs-lookup"><span data-stu-id="ffea5-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="ffea5-174">Последовательно выберите **Security \> Single Signon Settings** (Безопасность > Параметры единого входа).</span><span class="sxs-lookup"><span data-stu-id="ffea5-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="ffea5-175">![Параметры единого входа](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="ffea5-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="ffea5-176">Выберите для параметра **Single-Signon Type** (Тип единого входа) значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="ffea5-177">![Тип единого входа](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Тип единого входа")</span><span class="sxs-lookup"><span data-stu-id="ffea5-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="ffea5-178">В диалоговом окне **Параметры единого входа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ffea5-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="ffea5-179">![Параметры единого входа](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="ffea5-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="ffea5-180">а.</span><span class="sxs-lookup"><span data-stu-id="ffea5-180">a.</span></span> <span data-ttu-id="ffea5-181">В текстовое поле **Идентификатор сущности IdP SAML** вставьте значение **идентификатора SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ffea5-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ffea5-182">b.</span><span class="sxs-lookup"><span data-stu-id="ffea5-182">b.</span></span> <span data-ttu-id="ffea5-183">Скопируйте содержимое скачанного на портале Azure файла метаданных и вставьте его в текстовое поле **Метаданные поставщика удостоверений SAML**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="ffea5-184">c.</span><span class="sxs-lookup"><span data-stu-id="ffea5-184">c.</span></span> <span data-ttu-id="ffea5-185">В текстовое поле **URL-адрес успешного выхода** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ffea5-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ffea5-186">г)</span><span class="sxs-lookup"><span data-stu-id="ffea5-186">d.</span></span> <span data-ttu-id="ffea5-187">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ffea5-188">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ffea5-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ffea5-189">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ffea5-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ffea5-190">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ffea5-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ffea5-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffea5-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="ffea5-192">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffea5-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ffea5-194">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ffea5-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ffea5-195">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ffea5-197">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ffea5-199">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ffea5-201">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ffea5-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ffea5-203">а.</span><span class="sxs-lookup"><span data-stu-id="ffea5-203">a.</span></span> <span data-ttu-id="ffea5-204">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ffea5-205">b.</span><span class="sxs-lookup"><span data-stu-id="ffea5-205">b.</span></span> <span data-ttu-id="ffea5-206">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ffea5-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ffea5-207">c.</span><span class="sxs-lookup"><span data-stu-id="ffea5-207">c.</span></span> <span data-ttu-id="ffea5-208">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ffea5-209">d.</span><span class="sxs-lookup"><span data-stu-id="ffea5-209">d.</span></span> <span data-ttu-id="ffea5-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="ffea5-211">Создание тестового пользователя IdeaScale</span><span class="sxs-lookup"><span data-stu-id="ffea5-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="ffea5-212">Чтобы пользователи Azure AD могли выполнять вход в IdeaScale, они должны быть подготовлены для IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="ffea5-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="ffea5-213">В случае с IdeaScale подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="ffea5-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="ffea5-214">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ffea5-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ffea5-215">Выполните вход на корпоративном сайте службы **IdeaScale** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ffea5-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="ffea5-216">Выберите **Параметры сообщества**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="ffea5-217">![Параметры сообщества](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Параметры сообщества")</span><span class="sxs-lookup"><span data-stu-id="ffea5-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="ffea5-218">Последовательно выберите **Basic Settings \> Member Management** (Основные параметры > Управление участниками).</span><span class="sxs-lookup"><span data-stu-id="ffea5-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="ffea5-219">Щелкните **Добавить участника**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="ffea5-220">![Управление участниками](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Управление участниками")</span><span class="sxs-lookup"><span data-stu-id="ffea5-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="ffea5-221">В разделе "Добавление участника" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ffea5-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="ffea5-222">![Добавление новой записи](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Добавление новой записи")</span><span class="sxs-lookup"><span data-stu-id="ffea5-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="ffea5-223">а.</span><span class="sxs-lookup"><span data-stu-id="ffea5-223">a.</span></span> <span data-ttu-id="ffea5-224">В текстовое поле **Адреса электронной почты** введите адрес действующей учетной записи AAD, которую желаете подготовить.</span><span class="sxs-lookup"><span data-stu-id="ffea5-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="ffea5-225">b.</span><span class="sxs-lookup"><span data-stu-id="ffea5-225">b.</span></span> <span data-ttu-id="ffea5-226">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="ffea5-227">Владелец учетной записи Azure Active Directory получит электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="ffea5-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="ffea5-228">Вы можете использовать любые другие средства создания учетной записи пользователя IdeaScale или API, предоставляемые IdeaScale для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="ffea5-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ffea5-229">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffea5-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ffea5-230">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="ffea5-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ffea5-232">**Чтобы назначить пользователя Britta Simon в приложении IdeaScale, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="ffea5-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="ffea5-233">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ffea5-235">В списке приложений выберите **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-235">In the applications list, select **IdeaScale**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="ffea5-237">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ffea5-239">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-239">Click **Add** button.</span></span> <span data-ttu-id="ffea5-240">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ffea5-242">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ffea5-243">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ffea5-244">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ffea5-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ffea5-245">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ffea5-245">Testing single sign-on</span></span>


<span data-ttu-id="ffea5-246">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ffea5-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ffea5-247">Щелкнув элемент IdeaScale на панели доступа, вы автоматически войдете в приложение IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="ffea5-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ffea5-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ffea5-248">Additional resources</span></span>

* [<span data-ttu-id="ffea5-249">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffea5-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffea5-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ffea5-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

