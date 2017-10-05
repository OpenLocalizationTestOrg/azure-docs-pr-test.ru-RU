---
title: "Руководство. Интеграция Azure Active Directory с Absorb LMS | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Absorb LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="bbd52-103">Руководство. Интеграция Azure Active Directory с Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="bbd52-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="bbd52-104">В этом руководстве описано, как интегрировать приложение Absorb LMS с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbd52-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbd52-105">Интеграция Absorb LMS с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bbd52-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bbd52-106">С помощью Azure AD вы можете контролировать доступ к Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbd52-106">You can control in Azure AD who has access to Absorb LMS</span></span>
- <span data-ttu-id="bbd52-107">Вы можете включить автоматический вход пользователей в Absorb LMS (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd52-107">You can enable your users to automatically get signed-on to Absorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbd52-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd52-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bbd52-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье</span><span class="sxs-lookup"><span data-stu-id="bbd52-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="bbd52-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbd52-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbd52-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bbd52-111">Prerequisites</span></span>

<span data-ttu-id="bbd52-112">Чтобы настроить интеграцию Azure AD с Absorb LMS, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="bbd52-112">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="bbd52-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bbd52-113">An Azure AD subscription</span></span>
- <span data-ttu-id="bbd52-114">подписка Absorb LMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bbd52-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbd52-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="bbd52-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbd52-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="bbd52-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbd52-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bbd52-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbd52-118">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbd52-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbd52-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bbd52-119">Scenario description</span></span>
<span data-ttu-id="bbd52-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bbd52-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbd52-121">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="bbd52-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbd52-122">Добавление Absorb LMS из коллекции</span><span class="sxs-lookup"><span data-stu-id="bbd52-122">Adding Absorb LMS from the gallery</span></span>
2. <span data-ttu-id="bbd52-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd52-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-the-gallery"></a><span data-ttu-id="bbd52-124">Добавление Absorb LMS из коллекции</span><span class="sxs-lookup"><span data-stu-id="bbd52-124">Adding Absorb LMS from the gallery</span></span>
<span data-ttu-id="bbd52-125">Чтобы настроить интеграцию Absorb LMS с Azure AD, нужно добавить Absorb LMS из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bbd52-125">To configure the integration of Absorb LMS in to Azure AD, you need to add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bbd52-126">**Чтобы добавить Absorb LMS из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bbd52-126">**To add Absorb LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd52-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="bbd52-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bbd52-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-130">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="bbd52-132">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="bbd52-134">В поле поиска введите **Absorb LMS**, выберите **Absorb LMS** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="bbd52-134">In the search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button to add the application.</span></span>

    ![Absorb LMS в списке результатов](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bbd52-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd52-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bbd52-137">В этом разделе описана настройка и проверка единого входа Azure AD в Absorb LMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd52-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bbd52-138">Для работы единого входа в Azure AD нужно знать, какой пользователь в Absorb LMS соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd52-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Absorb LMS is to a user in Azure AD.</span></span> <span data-ttu-id="bbd52-139">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbd52-139">In other words, a link relationship between an Azure AD user and the related user in Absorb LMS needs to be established.</span></span>

<span data-ttu-id="bbd52-140">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве **имени пользователя** в Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbd52-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Absorb LMS.</span></span>

<span data-ttu-id="bbd52-141">Чтобы настроить и проверить единый вход Azure AD в Absorb LMS, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="bbd52-141">To configure and test Azure AD single sign-on with Absorb LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bbd52-142">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="bbd52-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bbd52-143">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd52-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbd52-144">**[Создание тестового пользователя Absorb LMS](#create-an-absorb-lms-test-user)** требуется для того, чтобы в Absorb LMS существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd52-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - to have a counterpart of Britta Simon in Absorb LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbd52-145">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd52-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbd52-146">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bbd52-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bbd52-147">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd52-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bbd52-148">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbd52-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="bbd52-149">**Чтобы настроить единый вход Azure AD в Absorb LMS, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bbd52-149">**To configure Azure AD single sign-on with Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd52-150">На портале Azure на странице интеграции с приложением **Absorb LMS** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-150">In the Azure portal, on the **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="bbd52-152">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="bbd52-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="bbd52-154">В разделе **Домены и URL-адреса приложения Absorb LMS** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="bbd52-154">On the **Absorb LMS Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="bbd52-156">а.</span><span class="sxs-lookup"><span data-stu-id="bbd52-156">a.</span></span> <span data-ttu-id="bbd52-157">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="bbd52-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="bbd52-158">b.</span><span class="sxs-lookup"><span data-stu-id="bbd52-158">b.</span></span> <span data-ttu-id="bbd52-159">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<subdomain>.myabsorb.com/Account/SAML`.</span><span class="sxs-lookup"><span data-stu-id="bbd52-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bbd52-160">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="bbd52-160">These values are not the real.</span></span> <span data-ttu-id="bbd52-161">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="bbd52-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="bbd52-162">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Absorb LMS](https://www.absorblms.com/support).</span><span class="sxs-lookup"><span data-stu-id="bbd52-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) to get these values.</span></span> 

4. <span data-ttu-id="bbd52-163">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="bbd52-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="bbd52-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bbd52-165">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bbd52-167">В разделе **Настройка Absorb LMS** щелкните **Настроить Absorb LMS**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-167">On the **Absorb LMS Configuration** section, click **Configure Absorb LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bbd52-168">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-168">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="bbd52-170">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Absorb LMS в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="bbd52-170">In a different web browser window, log in to your Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="bbd52-171">Щелкните **значок учетной записи** в интерфейсе администратора.</span><span class="sxs-lookup"><span data-stu-id="bbd52-171">Click the **Account Icon** on the admin interface.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="bbd52-173">Щелкните **Параметры портала**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-173">Click **Portal Settings**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="bbd52-175">Откройте вкладку **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="bbd52-175">Click the **Users** tab.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="bbd52-177">Для доступа к полям конфигурации единого входа выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bbd52-177">Perform the following steps to access the Single Sign-On configuration fields:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="bbd52-179">а.</span><span class="sxs-lookup"><span data-stu-id="bbd52-179">a.</span></span> <span data-ttu-id="bbd52-180">Выберите необходимый **Режим**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-180">Select the appropriate **Mode**.</span></span>

    <span data-ttu-id="bbd52-181">b.</span><span class="sxs-lookup"><span data-stu-id="bbd52-181">b.</span></span> <span data-ttu-id="bbd52-182">Откройте сертификат, скачанный с портала Azure, в Блокноте. Удалите тег **---BEGIN CERTIFICATE---** и **---END CERTIFICATE---**, а затем вставьте остальное содержимое в текстовое поле **Ключ**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-182">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Key** textbox.</span></span>
    
    <span data-ttu-id="bbd52-183">c.</span><span class="sxs-lookup"><span data-stu-id="bbd52-183">c.</span></span> <span data-ttu-id="bbd52-184">В поле **Id Property** (Свойство идентификатора) выберите подходящий атрибут, настроенный в качестве идентификатора пользователя в Azure AD (например, если в Azure AD выбран userprinciplename, здесь будет выбрано имя пользователя).</span><span class="sxs-lookup"><span data-stu-id="bbd52-184">In the **Id Property**, select the appropriate attribute which you have configured as the user identifier in the Azure AD (For example, If the userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="bbd52-185">d.</span><span class="sxs-lookup"><span data-stu-id="bbd52-185">d.</span></span> <span data-ttu-id="bbd52-186">В поле **URL-адрес для входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное из окна **Настройка единого входа** портала Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd52-186">In the **Login URL**, paste the **“SAML Single Sign-On Service URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="bbd52-187">д.</span><span class="sxs-lookup"><span data-stu-id="bbd52-187">e.</span></span> <span data-ttu-id="bbd52-188">В поле **URL-адрес выхода** вставьте значение **URL-адреса выхода**, скопированное из окна **Настройка единого входа** портала Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd52-188">In the **Logout URL**, paste the **“Sign-Out URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

13. <span data-ttu-id="bbd52-189">Включите параметр **Only Allow SSO Login** (Разрешить только единый вход).</span><span class="sxs-lookup"><span data-stu-id="bbd52-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="bbd52-191">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="bbd52-192">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="bbd52-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bbd52-193">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="bbd52-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bbd52-194">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="bbd52-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bbd52-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd52-195">Create an Azure AD test user</span></span>

<span data-ttu-id="bbd52-196">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd52-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="bbd52-198">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bbd52-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd52-199">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbd52-201">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbd52-203">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbd52-205">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bbd52-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbd52-207">а.</span><span class="sxs-lookup"><span data-stu-id="bbd52-207">a.</span></span> <span data-ttu-id="bbd52-208">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbd52-209">b.</span><span class="sxs-lookup"><span data-stu-id="bbd52-209">b.</span></span> <span data-ttu-id="bbd52-210">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bbd52-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbd52-211">c.</span><span class="sxs-lookup"><span data-stu-id="bbd52-211">c.</span></span> <span data-ttu-id="bbd52-212">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bbd52-213">d.</span><span class="sxs-lookup"><span data-stu-id="bbd52-213">d.</span></span> <span data-ttu-id="bbd52-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="bbd52-215">Создание тестового пользователя Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="bbd52-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="bbd52-216">Чтобы пользователи Azure AD могли входить в Absorb LMS, их нужно подготовить для Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbd52-216">To enable Azure AD users to log in to Absorb LMS, they must be provisioned in to Absorb LMS.</span></span>  
<span data-ttu-id="bbd52-217">Эта подготовка для Absorb LMS выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="bbd52-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="bbd52-218">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="bbd52-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd52-219">Войдите на веб-сайт организации Absorb LMS в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="bbd52-219">Log in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="bbd52-220">Откройте вкладку **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-220">Click **Users** tab.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="bbd52-222">На вкладке **Пользователи** щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-222">Click **Users** under the **Users** tab.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="bbd52-224">Выберите **Пользователя** в раскрывающемся списке **Добавить новый**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-224">Select **User** from **Add New** drop-down.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="bbd52-226">На странице **Добавление пользователя** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="bbd52-226">On the **Add User** page, perform the following steps:</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="bbd52-228">а.</span><span class="sxs-lookup"><span data-stu-id="bbd52-228">a.</span></span> <span data-ttu-id="bbd52-229">В текстовом поле **Имя** введите имя, например Britta.</span><span class="sxs-lookup"><span data-stu-id="bbd52-229">In the **First Name** textbox, type the first name like Britta.</span></span>

    <span data-ttu-id="bbd52-230">b.</span><span class="sxs-lookup"><span data-stu-id="bbd52-230">b.</span></span> <span data-ttu-id="bbd52-231">В текстовом поле **Фамилия** введите фамилию, например Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd52-231">In the **Last Name** textbox, type the last name like Simon.</span></span>
    
    <span data-ttu-id="bbd52-232">c.</span><span class="sxs-lookup"><span data-stu-id="bbd52-232">c.</span></span> <span data-ttu-id="bbd52-233">В текстовом поле **Имя пользователя** введите имя пользователя, например Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd52-233">In the **Username** textbox, type the user name like Britta Simon.</span></span>

    <span data-ttu-id="bbd52-234">г)</span><span class="sxs-lookup"><span data-stu-id="bbd52-234">d.</span></span> <span data-ttu-id="bbd52-235">В текстовом поле **Пароль** введите пароль пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd52-235">In the **Password** textbox, type the password of Britta Simon.</span></span>

    <span data-ttu-id="bbd52-236">д.</span><span class="sxs-lookup"><span data-stu-id="bbd52-236">e.</span></span> <span data-ttu-id="bbd52-237">В текстовом поле **Подтверждение пароля** введите пароль еще раз.</span><span class="sxs-lookup"><span data-stu-id="bbd52-237">In the **Confirm Password** textbox, type the same password.</span></span>
    
    <span data-ttu-id="bbd52-238">f.</span><span class="sxs-lookup"><span data-stu-id="bbd52-238">f.</span></span> <span data-ttu-id="bbd52-239">Выберите значение **Активно**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="bbd52-240">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-240">Click **"Save."**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bbd52-241">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd52-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="bbd52-242">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbd52-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![Назначение роли пользователя][200]

<span data-ttu-id="bbd52-244">**Чтобы назначить пользователя Britta Simon в Absorb LMS, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bbd52-244">**To assign Britta Simon to Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd52-245">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bbd52-247">В списке приложений выберите **Absorb LMS**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-247">In the applications list, select **Absorb LMS**.</span></span>

    ![Ссылка на Absorb LMS в списке "Приложения"](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="bbd52-249">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="bbd52-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-251">Click **Add** button.</span></span> <span data-ttu-id="bbd52-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="bbd52-254">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bbd52-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbd52-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bbd52-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bbd52-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bbd52-257">Test single sign-on</span></span>

<span data-ttu-id="bbd52-258">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="bbd52-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bbd52-259">Щелкнув элемент Absorb LMS на панели доступа, вы автоматически войдете в приложение Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbd52-259">Click the Absorb LMS tile in the Access Panel, you will get automatically signed-on to your Absorb LMS application.</span></span> <span data-ttu-id="bbd52-260">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="bbd52-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bbd52-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bbd52-261">Additional resources</span></span>

* [<span data-ttu-id="bbd52-262">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbd52-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbd52-263">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbd52-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

