---
title: "Руководство по интеграции Azure Active Directory с Perception United States (Non-UltiPro) | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Perception United States (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 8e2f9f979f8b94e0c043d4db6e93bd7a53c3dd27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="79dd8-103">Руководство по интеграции Azure Active Directory с Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="79dd8-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="79dd8-104">В этом руководстве вы узнаете, как интегрировать Perception United States (Non-UltiPro) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79dd8-104">In this tutorial, you learn how to integrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79dd8-105">Интеграция Perception United States (Non-UltiPro) с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="79dd8-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79dd8-106">С помощью Azure AD вы можете контролировать доступ к Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79dd8-106">You can control in Azure AD who has access to Perception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="79dd8-107">Вы можете включить автоматический вход пользователей в Perception United States (Non-UltiPro) (единый вход) с использованием их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79dd8-107">You can enable your users to automatically get signed-on to Perception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="79dd8-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="79dd8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="79dd8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79dd8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79dd8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="79dd8-110">Prerequisites</span></span>

<span data-ttu-id="79dd8-111">Чтобы настроить интеграцию Azure AD с United States (Non-UltiPro) необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="79dd8-111">To configure Azure AD integration with Perception United States (Non-UltiPro), you need the following items:</span></span>

- <span data-ttu-id="79dd8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="79dd8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79dd8-113">подписка Perception United States (Non-UltiPro) с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="79dd8-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79dd8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="79dd8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79dd8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="79dd8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79dd8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="79dd8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79dd8-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79dd8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79dd8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="79dd8-118">Scenario description</span></span>
<span data-ttu-id="79dd8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="79dd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79dd8-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="79dd8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79dd8-121">Добавление Perception United States (Non-UltiPro) из коллекции.</span><span class="sxs-lookup"><span data-stu-id="79dd8-121">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
2. <span data-ttu-id="79dd8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="79dd8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a><span data-ttu-id="79dd8-123">Добавление Perception United States (Non-UltiPro) из коллекции</span><span class="sxs-lookup"><span data-stu-id="79dd8-123">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
<span data-ttu-id="79dd8-124">Чтобы настроить интеграцию Perception United States (Non-UltiPro) с Azure AD, необходимо добавить Perception United States (Non-UltiPro) из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="79dd8-124">To configure the integration of Perception United States (Non-UltiPro) into Azure AD, you need to add Perception United States (Non-UltiPro) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79dd8-125">**Чтобы добавить Perception United States (Non-UltiPro) из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="79dd8-125">**To add Perception United States (Non-UltiPro) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79dd8-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="79dd8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79dd8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="79dd8-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="79dd8-133">В поле поиска введите **Perception United States (Non-UltiPro)**, выберите **Perception United States (Non-UltiPro)** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="79dd8-133">In the search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button to add the application.</span></span>

    ![Perception United States (Non-UltiPro) в списке результатов](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="79dd8-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="79dd8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="79dd8-136">В этом разделе описана настройка и проверка единого входа Azure AD в Perception United States (Non-UltiPro) с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79dd8-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79dd8-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Perception United States (Non-UltiPro) соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79dd8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Perception United States (Non-UltiPro) is to a user in Azure AD.</span></span> <span data-ttu-id="79dd8-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79dd8-138">In other words, a link relationship between an Azure AD user and the related user in Perception United States (Non-UltiPro) needs to be established.</span></span>

<span data-ttu-id="79dd8-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79dd8-139">In Perception United States (Non-UltiPro), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79dd8-140">Чтобы настроить и проверить единый вход Azure AD в Perception United States (Non-UltiPro), вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="79dd8-140">To configure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79dd8-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="79dd8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79dd8-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79dd8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79dd8-143">**[Создание тестового пользователя Perception United States (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)** требуется для создания пользователя Britta Simon в Perception United States (Non-UltiPro), связанного с соответствующим представлением пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79dd8-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - to have a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79dd8-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79dd8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79dd8-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="79dd8-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="79dd8-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="79dd8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="79dd8-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79dd8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="79dd8-148">**Чтобы настроить единый вход Azure AD в Perception United States (Non-UltiPro), выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="79dd8-148">**To configure Azure AD single sign-on with Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="79dd8-149">На портале Azure на странице интеграции с приложением **Perception United States (Non-UltiPro)** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-149">In the Azure portal, on the **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="79dd8-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="79dd8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="79dd8-153">В разделе **Домены и URL-адреса приложения Perception United States (Non-UltiPro)** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="79dd8-153">On the **Perception United States (Non-UltiPro) Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="79dd8-155">а.</span><span class="sxs-lookup"><span data-stu-id="79dd8-155">a.</span></span> <span data-ttu-id="79dd8-156">В текстовом поле **Идентификатор** введите URL-адрес `https://perception.kanjoya.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="79dd8-156">In the **Identifier** textbox, type the URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="79dd8-157">b.</span><span class="sxs-lookup"><span data-stu-id="79dd8-157">b.</span></span> <span data-ttu-id="79dd8-158">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://perception.kanjoya.com/sso?idp=<entity_id>`.</span><span class="sxs-lookup"><span data-stu-id="79dd8-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79dd8-159">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="79dd8-159">The value is not real.</span></span> <span data-ttu-id="79dd8-160">Вы замените это значение на фактический URL-адрес ответа, который описывается далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="79dd8-160">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="79dd8-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="79dd8-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="79dd8-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="79dd8-163">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79dd8-165">В разделе **Настройка Perception United States (Non-UltiPro)** щелкните **Настроить Perception United States (Non-UltiPro)**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-165">On the **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="79dd8-166">Скопируйте значение **SAML Entity ID** (Идентификатор сущности SAML) из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="79dd8-167">а.</span><span class="sxs-lookup"><span data-stu-id="79dd8-167">a.</span></span> <span data-ttu-id="79dd8-168">Приложению **Perception United States (Non-UltiPro)** необходимо значение **идентификатора сущности SAML**, которое вы скопировали, чтобы закодировать в формате URI.</span><span class="sxs-lookup"><span data-stu-id="79dd8-168">The **Perception United States (Non-UltiPro)** application requires the **SAML Entity ID** value, which you have copied, to be uri encoded.</span></span> <span data-ttu-id="79dd8-169">Для получения значения, закодированного в формате URI, перейдите по следующей ссылке: **http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-169">To get the uri encoded value, use the following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="79dd8-170">b.</span><span class="sxs-lookup"><span data-stu-id="79dd8-170">b.</span></span> <span data-ttu-id="79dd8-171">Получив это значение, объедините его с **URL-адресом ответа**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="79dd8-171">After getting the uri encoded value combine it with the **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="79dd8-172">c.</span><span class="sxs-lookup"><span data-stu-id="79dd8-172">c.</span></span> <span data-ttu-id="79dd8-173">Вставьте значение выше в текстовое поле **URL-адрес ответа** в разделе **Домены и URL-адреса приложения Perception United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-173">Paste the above value in the **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Настройка Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="79dd8-175">В другом окне браузера войдите на корпоративный веб-сайт Perception United States (Non-UltiPro) с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="79dd8-175">In another browser window, sign on to your Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="79dd8-176">На главной панели инструментов щелкните **Account Settings** (Параметры учетной записи).</span><span class="sxs-lookup"><span data-stu-id="79dd8-176">In the main toolbar, click **Account Settings**.</span></span>

    ![Пользователь Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="79dd8-178">На странице **Account Settings** (Параметры учетной записи) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="79dd8-178">On the **Account Settings** page, perform the following steps:</span></span>

    ![Пользователь Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="79dd8-180">а.</span><span class="sxs-lookup"><span data-stu-id="79dd8-180">a.</span></span> <span data-ttu-id="79dd8-181">В текстовом поле **Company Name** (Название компании) введите название **компании**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-181">In the **Company Name** textbox, type the name of the **Company**.</span></span>
    
    <span data-ttu-id="79dd8-182">b.</span><span class="sxs-lookup"><span data-stu-id="79dd8-182">b.</span></span> <span data-ttu-id="79dd8-183">В текстовом поле **Account Name** (Имя учетной записи) введите имя **учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-183">In the **Account Name** textbox, type the name of the **Account**.</span></span>

    <span data-ttu-id="79dd8-184">c.</span><span class="sxs-lookup"><span data-stu-id="79dd8-184">c.</span></span> <span data-ttu-id="79dd8-185">В текстовом поле **Default Reply-To Email** (Электронная почта ответа по умолчанию) введите допустимый адрес **электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-185">In **Default Reply-To Email** text box, type the valid **Email**.</span></span>

    <span data-ttu-id="79dd8-186">d.</span><span class="sxs-lookup"><span data-stu-id="79dd8-186">d.</span></span> <span data-ttu-id="79dd8-187">Выберите для параметра **SSO Identity Provider** (Поставщик удостоверений единого входа) значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="79dd8-188">На странице **настройки единого входа** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="79dd8-188">On the **SSO Configuration** page, perform the following steps:</span></span>

    ![Настройка единого входа Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="79dd8-190">а.</span><span class="sxs-lookup"><span data-stu-id="79dd8-190">a.</span></span> <span data-ttu-id="79dd8-191">Выберите для параметра **SAML NameID Type** (Тип NameID SAML) значение **EMAIL** (Электронная почта).</span><span class="sxs-lookup"><span data-stu-id="79dd8-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="79dd8-192">b.</span><span class="sxs-lookup"><span data-stu-id="79dd8-192">b.</span></span> <span data-ttu-id="79dd8-193">В текстовом поле **SSO Configuration Name** (Имя конфигурации единого входа) введите имя своей **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-193">In the **SSO Configuration Name** textbox, type the name of your **Configuration**.</span></span>
    
    <span data-ttu-id="79dd8-194">c.</span><span class="sxs-lookup"><span data-stu-id="79dd8-194">c.</span></span> <span data-ttu-id="79dd8-195">В текстовое поле **Identity Provider Name** (Имя поставщика удостоверений) вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="79dd8-195">In **Identity Provider Name** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="79dd8-196">d.</span><span class="sxs-lookup"><span data-stu-id="79dd8-196">d.</span></span> <span data-ttu-id="79dd8-197">В **текстовое поле домена SAML** введите домен, например **@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-197">In **SAML Domain textbox**, enter the domain like **@contoso.com**.</span></span>

    <span data-ttu-id="79dd8-198">д.</span><span class="sxs-lookup"><span data-stu-id="79dd8-198">e.</span></span> <span data-ttu-id="79dd8-199">Нажмите кнопку **Upload Again** (Отправить еще раз), чтобы передать **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-199">Click on **Upload Again** to upload the **Metadata XML** file.</span></span>

    <span data-ttu-id="79dd8-200">f.</span><span class="sxs-lookup"><span data-stu-id="79dd8-200">f.</span></span> <span data-ttu-id="79dd8-201">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="79dd8-202">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="79dd8-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79dd8-203">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="79dd8-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79dd8-204">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="79dd8-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="79dd8-205">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="79dd8-205">Create an Azure AD test user</span></span>

<span data-ttu-id="79dd8-206">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79dd8-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="79dd8-208">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="79dd8-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79dd8-209">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="79dd8-211">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="79dd8-213">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="79dd8-215">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="79dd8-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="79dd8-217">а.</span><span class="sxs-lookup"><span data-stu-id="79dd8-217">a.</span></span> <span data-ttu-id="79dd8-218">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79dd8-219">b.</span><span class="sxs-lookup"><span data-stu-id="79dd8-219">b.</span></span> <span data-ttu-id="79dd8-220">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79dd8-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="79dd8-221">c.</span><span class="sxs-lookup"><span data-stu-id="79dd8-221">c.</span></span> <span data-ttu-id="79dd8-222">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="79dd8-223">г)</span><span class="sxs-lookup"><span data-stu-id="79dd8-223">d.</span></span> <span data-ttu-id="79dd8-224">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="79dd8-225">Создание тестового пользователя Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="79dd8-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="79dd8-226">В этом разделе описано, как создать пользователя Britta Simon в приложении Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79dd8-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="79dd8-227">Обратитесь в [службу поддержки Perception United States (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs), чтобы добавить пользователей на платформу Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79dd8-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) to add the users in the Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="79dd8-228">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="79dd8-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="79dd8-229">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79dd8-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Perception United States (Non-UltiPro).</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="79dd8-231">**Чтобы назначить пользователя Britta Simon в приложении Perception United States (Non-UltiPro), выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="79dd8-231">**To assign Britta Simon to Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="79dd8-232">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="79dd8-234">В списке приложений выберите **Perception United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-234">In the applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![Ссылка на Perception United States (Non-UltiPro) в списке "Приложения"](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="79dd8-236">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="79dd8-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-238">Click **Add** button.</span></span> <span data-ttu-id="79dd8-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="79dd8-241">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79dd8-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79dd8-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="79dd8-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="79dd8-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="79dd8-244">Test single sign-on</span></span>

<span data-ttu-id="79dd8-245">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="79dd8-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79dd8-246">Щелкнув плитку Perception United States (Non-UltiPro) на панели доступа, вы автоматически войдете в приложение Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79dd8-246">When you click the Perception United States (Non-UltiPro) tile in the Access Panel, you should get automatically signed-on to your Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="79dd8-247">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79dd8-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="79dd8-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="79dd8-248">Additional resources</span></span>

* [<span data-ttu-id="79dd8-249">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79dd8-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79dd8-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79dd8-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

