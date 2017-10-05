---
title: "Руководство по интеграции Azure Active Directory с Citrix GoToMeeting | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="d3667-103">Учебник. Интеграция Azure Active Directory с Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="d3667-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="d3667-104">В этом руководстве описано, как интегрировать Citrix GoToMeeting с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3667-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3667-105">Интеграция Azure AD с Citrix GoToMeeting обеспечивает перечисленные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="d3667-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3667-106">С помощью Azure AD вы можете контролировать доступ к Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d3667-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="d3667-107">Вы можете включить автоматический вход пользователей в Citrix GoToMeeting (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3667-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3667-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d3667-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3667-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3667-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3667-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3667-110">Prerequisites</span></span>

<span data-ttu-id="d3667-111">Чтобы настроить интеграцию Azure AD с Citrix GoToMeeting, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d3667-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="d3667-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d3667-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3667-113">подписка Citrix GoToMeeting с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d3667-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3667-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d3667-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3667-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="d3667-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3667-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d3667-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3667-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3667-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3667-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d3667-118">Scenario description</span></span>
<span data-ttu-id="d3667-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d3667-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3667-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="d3667-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3667-121">Добавление Citrix GoToMeeting из коллекции</span><span class="sxs-lookup"><span data-stu-id="d3667-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="d3667-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3667-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="d3667-123">Добавление Citrix GoToMeeting из коллекции</span><span class="sxs-lookup"><span data-stu-id="d3667-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="d3667-124">Чтобы настроить интеграцию Citrix GoToMeeting с Azure AD, вам нужно добавить Citrix GoToMeeting из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d3667-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3667-125">**Чтобы добавить Citrix GoToMeeting из коллекции, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="d3667-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3667-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d3667-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3667-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d3667-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3667-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d3667-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d3667-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="d3667-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d3667-133">В поле поиска введите **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="d3667-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="d3667-135">На панели результатов выберите **Citrix GoToMeeting** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="d3667-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3667-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3667-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3667-138">В этом разделе описана настройка и проверка единого входа Azure AD в Citrix GoToMeeting с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3667-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d3667-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Citrix GoToMeeting соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3667-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="d3667-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d3667-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="d3667-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d3667-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="d3667-142">Чтобы настроить и проверить единый вход Azure AD в Citrix GoToMeeting, вам нужно выполнить действия в перечисленных ниже стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="d3667-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3667-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d3667-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3667-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3667-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3667-145">**[Создание тестового пользователя Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)** требуется для создания в Citrix GoToMeeting пользователя Britta Simon, связанного с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3667-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3667-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3667-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3667-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d3667-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3667-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3667-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3667-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d3667-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="d3667-150">**Чтобы настроить единый вход Azure AD в Citrix GoToMeeting, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="d3667-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="d3667-151">На портале Azure на странице интеграции с приложением **Citrix GoToMeeting** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d3667-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d3667-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="d3667-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="d3667-155">В разделе **Домены и URL-адреса приложения Citrix GoToMeeting** не нужно выполнять никаких действий.</span><span class="sxs-lookup"><span data-stu-id="d3667-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="d3667-157">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d3667-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="d3667-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d3667-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="d3667-161">В разделе "Настройка SAML Citrix GoToMeeting" щелкните "Настроить SAML Citrix GoToMeeting", чтобы открыть окно "Настройка единого входа".</span><span class="sxs-lookup"><span data-stu-id="d3667-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="d3667-162">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="d3667-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="d3667-163">В другом окне браузера войдите в [центр организации Citrix](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="d3667-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="d3667-164">Щелкните вкладку **Конфигурация поставщика удостоверений** и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d3667-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="d3667-165">![Настройка SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="d3667-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="d3667-166">а.</span><span class="sxs-lookup"><span data-stu-id="d3667-166">a.</span></span> <span data-ttu-id="d3667-167">Выберите **Вручную**</span><span class="sxs-lookup"><span data-stu-id="d3667-167">Select **Manual**</span></span>

    <span data-ttu-id="d3667-168">b.</span><span class="sxs-lookup"><span data-stu-id="d3667-168">b.</span></span> <span data-ttu-id="d3667-169">На диалоговой странице **Настройка единого входа в Citrix GoToMeeting** портала Azure скопируйте значение поля **URL-адрес службы единого входа SAML** и вставьте его в текстовое поле **Sign-in page URL** (URL-адрес страницы входа).</span><span class="sxs-lookup"><span data-stu-id="d3667-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="d3667-170">c.</span><span class="sxs-lookup"><span data-stu-id="d3667-170">c.</span></span> <span data-ttu-id="d3667-171">На диалоговой странице **Настройка единого входа в Citrix GoToMeeting** портала Azure скопируйте значение поля **URL-адрес выхода** и вставьте его в текстовое поле **Sign-out page URL** (URL-адрес страницы выхода).</span><span class="sxs-lookup"><span data-stu-id="d3667-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="d3667-172">г)</span><span class="sxs-lookup"><span data-stu-id="d3667-172">d.</span></span> <span data-ttu-id="d3667-173">На диалоговой странице **Настройка единого входа в Citrix GoToMeeting** портала Azure скопируйте значение поля **Идентификатор сущности SAML** и вставьте его в текстовое поле **Identity Provider Entity ID** (Идентификатор сущности поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="d3667-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="d3667-174">д.</span><span class="sxs-lookup"><span data-stu-id="d3667-174">e.</span></span> <span data-ttu-id="d3667-175">Для передачи загруженного сертификата нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="d3667-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="d3667-176">Е.</span><span class="sxs-lookup"><span data-stu-id="d3667-176">f.</span></span> <span data-ttu-id="d3667-177">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d3667-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d3667-178">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d3667-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3667-179">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d3667-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3667-180">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d3667-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3667-181">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3667-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3667-182">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3667-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d3667-184">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d3667-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3667-185">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d3667-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3667-187">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d3667-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3667-189">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d3667-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3667-191">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d3667-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3667-193">а.</span><span class="sxs-lookup"><span data-stu-id="d3667-193">a.</span></span> <span data-ttu-id="d3667-194">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3667-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3667-195">b.</span><span class="sxs-lookup"><span data-stu-id="d3667-195">b.</span></span> <span data-ttu-id="d3667-196">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3667-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3667-197">c.</span><span class="sxs-lookup"><span data-stu-id="d3667-197">c.</span></span> <span data-ttu-id="d3667-198">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="d3667-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3667-199">d.</span><span class="sxs-lookup"><span data-stu-id="d3667-199">d.</span></span> <span data-ttu-id="d3667-200">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d3667-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="d3667-201">Создание тестового пользователя Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="d3667-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="d3667-202">В этом разделе вы создадите в Citrix GoToMeeting пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3667-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="d3667-203">Приложение Citrix GoToMeeting поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d3667-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="d3667-204">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="d3667-204">There is no action item for you in this section.</span></span> <span data-ttu-id="d3667-205">Если пользователь в Citrix GoToMeeting еще не существует, он создается при попытке доступа к приложению Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d3667-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="d3667-206">Чтобы создать пользователя вручную, обратитесь в [службу поддержки Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting).</span><span class="sxs-lookup"><span data-stu-id="d3667-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d3667-207">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3667-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d3667-208">В этом разделе описано, как настроить для пользователя Britta Simon единый вход Azure, предоставив доступ к Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d3667-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d3667-210">**Чтобы назначить пользователя Britta Simon в Citrix GoToMeeting, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="d3667-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="d3667-211">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d3667-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d3667-213">В списке приложений выберите **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="d3667-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="d3667-215">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d3667-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d3667-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d3667-217">Click **Add** button.</span></span> <span data-ttu-id="d3667-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d3667-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d3667-220">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d3667-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3667-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d3667-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3667-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d3667-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3667-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d3667-223">Testing single sign-on</span></span>

<span data-ttu-id="d3667-224">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d3667-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3667-225">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="d3667-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d3667-226">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3667-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3667-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d3667-227">Additional resources</span></span>

* [<span data-ttu-id="d3667-228">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3667-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3667-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3667-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d3667-230">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="d3667-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

