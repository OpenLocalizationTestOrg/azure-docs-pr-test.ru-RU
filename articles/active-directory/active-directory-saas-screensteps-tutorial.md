---
title: "Руководство по интеграции Azure Active Directory с ScreenSteps | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: b6ded8ba1adf03fdccbdb7573c09fae1857c8b16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="1bac6-103">Учебник. Интеграция Azure Active Directory с ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="1bac6-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="1bac6-104">В этом учебнике описано, как интегрировать ScreenSteps с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1bac6-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1bac6-105">Интеграция Azure AD с приложением ScreenSteps обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="1bac6-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1bac6-106">C помощью Azure AD вы можете контролировать доступ к ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="1bac6-107">Вы можете включить автоматический вход пользователей в ScreenSteps (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bac6-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1bac6-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="1bac6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1bac6-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1bac6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bac6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1bac6-110">Prerequisites</span></span>

<span data-ttu-id="1bac6-111">Чтобы настроить интеграцию Azure AD с ScreenSteps, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="1bac6-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="1bac6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1bac6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1bac6-113">подписка ScreenSteps с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1bac6-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1bac6-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="1bac6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1bac6-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="1bac6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1bac6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1bac6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1bac6-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1bac6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1bac6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1bac6-118">Scenario description</span></span>
<span data-ttu-id="1bac6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1bac6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1bac6-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="1bac6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1bac6-121">Добавление ScreenSteps из коллекции</span><span class="sxs-lookup"><span data-stu-id="1bac6-121">Adding ScreenSteps from the gallery</span></span>
2. <span data-ttu-id="1bac6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bac6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="1bac6-123">Добавление ScreenSteps из коллекции</span><span class="sxs-lookup"><span data-stu-id="1bac6-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="1bac6-124">Чтобы настроить интеграцию ScreenSteps с Azure AD, необходимо добавить ScreenSteps из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1bac6-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1bac6-125">**Чтобы добавить ScreenSteps из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="1bac6-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1bac6-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="1bac6-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1bac6-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="1bac6-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="1bac6-133">В поле поиска введите **ScreenSteps**, выберите **ScreenSteps** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="1bac6-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![ScreenSteps в списке результатов](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1bac6-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bac6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1bac6-136">В этом разделе описана настройка и проверка единого входа Azure AD в ScreenSteps с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1bac6-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1bac6-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в ScreenSteps соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bac6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="1bac6-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="1bac6-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1bac6-140">Чтобы настроить и проверить единый вход Azure AD в ScreenSteps, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="1bac6-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1bac6-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="1bac6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1bac6-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1bac6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1bac6-143">**[Создание тестового пользователя ScreenSteps](#create-a-screensteps-test-user)** требуется для того, чтобы в ScreenSteps существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bac6-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1bac6-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bac6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1bac6-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1bac6-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1bac6-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bac6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1bac6-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="1bac6-148">**Чтобы настроить единый вход Azure AD в ScreenSteps, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="1bac6-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="1bac6-149">На портале Azure на странице интеграции с приложением **ScreenSteps** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="1bac6-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="1bac6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="1bac6-153">В разделе **Домены и URL-адреса приложения ScreenSteps** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="1bac6-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="1bac6-155">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="1bac6-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1bac6-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="1bac6-156">This value is not real.</span></span> <span data-ttu-id="1bac6-157">Замените его на фактический URL-адрес входа, как описано далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="1bac6-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="1bac6-158">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1bac6-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="1bac6-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1bac6-160">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1bac6-162">В разделе **Конфигурация ScreenSteps** щелкните **Настроить ScreenSteps**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1bac6-163">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="1bac6-165">В другом окне веб-браузера войдите на сайт ScreenSteps своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="1bac6-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="1bac6-166">Щелкните **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="1bac6-167">![Управление учетными записями](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Управление учетными записями")</span><span class="sxs-lookup"><span data-stu-id="1bac6-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="1bac6-168">Щелкните **Single Sign-on**(Единый вход).</span><span class="sxs-lookup"><span data-stu-id="1bac6-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="1bac6-169">![Удаленная аутентификация](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Удаленная аутентификация")</span><span class="sxs-lookup"><span data-stu-id="1bac6-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="1bac6-170">Щелкните **Create Single Sign-on Endpoint** (Создать конечную точку единого входа).</span><span class="sxs-lookup"><span data-stu-id="1bac6-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="1bac6-171">![Удаленная аутентификация](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Удаленная аутентификация")</span><span class="sxs-lookup"><span data-stu-id="1bac6-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="1bac6-172">В разделе **Create Single Sign-on Endpoint** (Создать конечную точку единого входа) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1bac6-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="1bac6-173">![Создание конечной точки аутентификации](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Создание конечной точки аутентификации")</span><span class="sxs-lookup"><span data-stu-id="1bac6-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="1bac6-174">а.</span><span class="sxs-lookup"><span data-stu-id="1bac6-174">a.</span></span> <span data-ttu-id="1bac6-175">В текстовом поле **Название** введите название.</span><span class="sxs-lookup"><span data-stu-id="1bac6-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="1bac6-176">b.</span><span class="sxs-lookup"><span data-stu-id="1bac6-176">b.</span></span> <span data-ttu-id="1bac6-177">Из списка **Mode** (Режим) выберите **SAML**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="1bac6-178">c.</span><span class="sxs-lookup"><span data-stu-id="1bac6-178">c.</span></span> <span data-ttu-id="1bac6-179">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-179">Click **Create**.</span></span>

12. <span data-ttu-id="1bac6-180">**Измените** новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="1bac6-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="1bac6-181">![Изменение конечной точки](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span><span class="sxs-lookup"><span data-stu-id="1bac6-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="1bac6-182">В разделе **Create Single Sign-on Endpoint** (Изменить конечную точку единого входа) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1bac6-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="1bac6-183">![Конечная точка удаленной аутентификации](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Конечная точка удаленной аутентификации")</span><span class="sxs-lookup"><span data-stu-id="1bac6-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="1bac6-184">а.</span><span class="sxs-lookup"><span data-stu-id="1bac6-184">a.</span></span> <span data-ttu-id="1bac6-185">Щелкните **Upload new SAML Certificate file** (Отправить новый файл сертификата SAML), а затем отправьте сертификат, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1bac6-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="1bac6-186">b.</span><span class="sxs-lookup"><span data-stu-id="1bac6-186">b.</span></span> <span data-ttu-id="1bac6-187">Вставьте **URL-адрес службы единого входа SAML**, скопированный на портале Azure, в текстовое поле **URL-адрес удаленного входа**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="1bac6-188">c.</span><span class="sxs-lookup"><span data-stu-id="1bac6-188">c.</span></span> <span data-ttu-id="1bac6-189">Вставьте **URL-адрес входа**, скопированный на портале Azure, в текстовое поле **URL-адрес выхода**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="1bac6-190">d.</span><span class="sxs-lookup"><span data-stu-id="1bac6-190">d.</span></span> <span data-ttu-id="1bac6-191">Выберите **группу** для назначения пользователей при их подготовке.</span><span class="sxs-lookup"><span data-stu-id="1bac6-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="1bac6-192">д.</span><span class="sxs-lookup"><span data-stu-id="1bac6-192">e.</span></span> <span data-ttu-id="1bac6-193">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-193">Click **Update**.</span></span>

    <span data-ttu-id="1bac6-194">f.</span><span class="sxs-lookup"><span data-stu-id="1bac6-194">f.</span></span> <span data-ttu-id="1bac6-195">Скопируйте **URL-адрес потребителя SAML** в буфер обмена и вставьте его в текстовое поле **URL-адрес входа** в разделе **Домены и URL-адреса приложения ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="1bac6-196">ж.</span><span class="sxs-lookup"><span data-stu-id="1bac6-196">g.</span></span> <span data-ttu-id="1bac6-197">Вернитесь в раздел **Edit Single Sign-on Endpoint** (Изменить конечную точку единого входа).</span><span class="sxs-lookup"><span data-stu-id="1bac6-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="1bac6-198">h.</span><span class="sxs-lookup"><span data-stu-id="1bac6-198">h.</span></span> <span data-ttu-id="1bac6-199">Нажмите кнопку **Make default for account** (Сделать значением по умолчанию для учетной записи), чтобы использовать эту конечную точку для всех пользователей, осуществляющих вход в ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="1bac6-200">Кроме того, можно нажать кнопку **Add to Site** (Добавить на сайт), чтобы использовать эту конечную точку для определенных сайтов в **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="1bac6-201">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="1bac6-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1bac6-202">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="1bac6-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1bac6-203">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="1bac6-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1bac6-204">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bac6-204">Create an Azure AD test user</span></span>

<span data-ttu-id="1bac6-205">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1bac6-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="1bac6-207">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="1bac6-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1bac6-208">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1bac6-210">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1bac6-212">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1bac6-214">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="1bac6-214">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1bac6-216">а.</span><span class="sxs-lookup"><span data-stu-id="1bac6-216">a.</span></span> <span data-ttu-id="1bac6-217">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1bac6-218">b.</span><span class="sxs-lookup"><span data-stu-id="1bac6-218">b.</span></span> <span data-ttu-id="1bac6-219">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1bac6-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1bac6-220">c.</span><span class="sxs-lookup"><span data-stu-id="1bac6-220">c.</span></span> <span data-ttu-id="1bac6-221">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1bac6-222">г)</span><span class="sxs-lookup"><span data-stu-id="1bac6-222">d.</span></span> <span data-ttu-id="1bac6-223">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="1bac6-224">Создание тестового пользователя ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="1bac6-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="1bac6-225">В этом разделе описано, как создать пользователя Britta Simon в ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="1bac6-226">Обратитесь в [службу поддержки ScreenSteps](https://www.screensteps.com/contact), чтобы добавить пользователей на платформу ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="1bac6-227">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="1bac6-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1bac6-228">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bac6-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="1bac6-229">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="1bac6-231">**Чтобы назначить пользователя Britta Simon приложению ScreenSteps, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="1bac6-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="1bac6-232">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1bac6-234">В списке приложений выберите **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-234">In the applications list, select **ScreenSteps**.</span></span>

    ![Ссылка на ScreenSteps в списке "Приложения"](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="1bac6-236">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="1bac6-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-238">Click **Add** button.</span></span> <span data-ttu-id="1bac6-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="1bac6-241">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1bac6-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1bac6-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1bac6-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1bac6-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1bac6-244">Test single sign-on</span></span>

<span data-ttu-id="1bac6-245">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="1bac6-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1bac6-246">Щелкнув элемент ScreenSteps на панели доступа, вы автоматически войдете в приложение ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="1bac6-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="1bac6-247">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1bac6-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1bac6-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1bac6-248">Additional resources</span></span>

* [<span data-ttu-id="1bac6-249">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1bac6-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1bac6-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1bac6-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

