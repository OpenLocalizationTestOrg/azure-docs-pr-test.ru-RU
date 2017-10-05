---
title: "Учебник. Интеграция Azure Active Directory с Front | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Front."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="ce1c3-103">Учебник. Интеграция Azure Active Directory с Front</span><span class="sxs-lookup"><span data-stu-id="ce1c3-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="ce1c3-104">В этом руководстве описано, как интегрировать Front с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce1c3-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce1c3-105">Интеграция Azure AD с приложением Front обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ce1c3-106">С помощью Azure AD вы можете контролировать доступ к Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="ce1c3-107">Вы можете включить автоматический вход пользователей в Front (единый вход) с учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ce1c3-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ce1c3-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce1c3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce1c3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ce1c3-110">Prerequisites</span></span>

<span data-ttu-id="ce1c3-111">Чтобы настроить интеграцию Azure AD с Front, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ce1c3-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="ce1c3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ce1c3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce1c3-113">подписка с поддержкой единого входа Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce1c3-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce1c3-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ce1c3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce1c3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce1c3-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce1c3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce1c3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ce1c3-118">Scenario description</span></span>
<span data-ttu-id="ce1c3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce1c3-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ce1c3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce1c3-121">Добавление Front из коллекции</span><span class="sxs-lookup"><span data-stu-id="ce1c3-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="ce1c3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce1c3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="ce1c3-123">Добавление Front из коллекции</span><span class="sxs-lookup"><span data-stu-id="ce1c3-123">Adding Front from the gallery</span></span>
<span data-ttu-id="ce1c3-124">Чтобы настроить интеграцию Front с Azure AD, необходимо добавить Front из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ce1c3-125">**Чтобы добавить Front из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ce1c3-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ce1c3-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="ce1c3-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ce1c3-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="ce1c3-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="ce1c3-133">В поле поиска введите **Front**, выберите **Front** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Front в списке результатов](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ce1c3-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce1c3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ce1c3-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Front с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ce1c3-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Front соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="ce1c3-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="ce1c3-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ce1c3-140">Чтобы настроить и проверить единый вход Azure AD в Front, вам потребуется выполнить действия в указанных далее стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ce1c3-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ce1c3-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce1c3-143">**[Создание тестового пользователя Front](#create-a-front-test-user)** требуется для того, чтобы во Front существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce1c3-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce1c3-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ce1c3-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce1c3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ce1c3-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="ce1c3-148">**Чтобы настроить единый вход Azure AD в Front, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ce1c3-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="ce1c3-149">На портале Azure на странице интеграции с приложением **Front** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="ce1c3-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="ce1c3-153">Если требуется настроить приложение в режиме, инициируемом **IDP**, то в разделе **Домены и URL-адреса приложения Front** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ce1c3-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="ce1c3-155">а.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-155">a.</span></span> <span data-ttu-id="ce1c3-156">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="ce1c3-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="ce1c3-157">b.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-157">b.</span></span> <span data-ttu-id="ce1c3-158">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.frontapp.com/sso/saml/callback`.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="ce1c3-159">Установите флажок **Показать дополнительные параметры URL-адресов**, если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="ce1c3-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="ce1c3-161">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="ce1c3-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ce1c3-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-162">These values are not real.</span></span> <span data-ttu-id="ce1c3-163">Вместо этих значений укажите фактические идентификатор, URL-адрес ответа и URL-адрес входа, к которым мы вернемся позже в этом руководстве, или обратитесь в [службу поддержки клиентов Front](mailto:support@frontapp.com), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="ce1c3-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="ce1c3-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ce1c3-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="ce1c3-168">В разделе **Конфигурация Front** щелкните **Настроить Front**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ce1c3-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="ce1c3-171">Войдите в клиент Front с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="ce1c3-172">Последовательно выберите пункты **Settings (Параметры) (значок шестеренки в нижней части левой боковой панели) > Preferences (Предпочтения)**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="ce1c3-174">Щелкните ссылку **Single Sign On** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="ce1c3-174">Click **Single Sign On** link.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="ce1c3-176">В раскрывающемся списке **Single Sign On** (Единый вход) выберите **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="ce1c3-178">В текстовое поле **Entry Point** (Точка входа) введите значение **URL-адрес службы единого входа** из мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="ce1c3-180">Откройте скачанный файл **сертификата в кодировке Base64** в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Signing certificate** (Сертификат для подписи).</span><span class="sxs-lookup"><span data-stu-id="ce1c3-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="ce1c3-182">В разделе **Service provider settings** (Параметры поставщика услуг) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ce1c3-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="ce1c3-184">а.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-184">a.</span></span> <span data-ttu-id="ce1c3-185">Скопируйте значение **Entity ID** (Идентификатор сущности) и вставьте его в текстовое поле **Идентификатор** в разделе **Домены и URL-адреса приложения Front** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="ce1c3-186">b.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-186">b.</span></span> <span data-ttu-id="ce1c3-187">Скопируйте значение **ACS URL** (URL-адрес ACS) и вставьте его в текстовое поле **URL-адрес входа** в разделе **Домены и URL-адреса приложения Front** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="ce1c3-188">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ce1c3-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="ce1c3-189">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ce1c3-190">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ce1c3-191">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ce1c3-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ce1c3-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce1c3-192">Create an Azure AD test user</span></span>

<span data-ttu-id="ce1c3-193">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="ce1c3-195">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ce1c3-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ce1c3-196">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ce1c3-198">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ce1c3-200">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ce1c3-202">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ce1c3-204">а.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-204">a.</span></span> <span data-ttu-id="ce1c3-205">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce1c3-206">b.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-206">b.</span></span> <span data-ttu-id="ce1c3-207">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ce1c3-208">c.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-208">c.</span></span> <span data-ttu-id="ce1c3-209">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ce1c3-210">г)</span><span class="sxs-lookup"><span data-stu-id="ce1c3-210">d.</span></span> <span data-ttu-id="ce1c3-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="ce1c3-212">Создание тестового пользователя Front</span><span class="sxs-lookup"><span data-stu-id="ce1c3-212">Create a Front test user</span></span>

<span data-ttu-id="ce1c3-213">В этом разделе описано, как создать пользователя Britta Simon в приложении Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="ce1c3-214">Обратитесь в [службу поддержки клиентов Front](mailto:support@frontapp.com), чтобы добавить пользователей на платформу Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="ce1c3-215">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ce1c3-216">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce1c3-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="ce1c3-217">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="ce1c3-219">**Чтобы назначить пользователя Britta Simon в Front, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ce1c3-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="ce1c3-220">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ce1c3-222">В списке приложений выберите **Front**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-222">In the applications list, select **Front**.</span></span>

    ![Ссылка на Front в списке "Приложения"](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="ce1c3-224">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="ce1c3-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-226">Click **Add** button.</span></span> <span data-ttu-id="ce1c3-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="ce1c3-229">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ce1c3-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce1c3-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ce1c3-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ce1c3-232">Test single sign-on</span></span>

<span data-ttu-id="ce1c3-233">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="ce1c3-234">Щелкнув элемент Front на панели доступа, вы автоматически войдете в приложение Front.</span><span class="sxs-lookup"><span data-stu-id="ce1c3-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ce1c3-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ce1c3-235">Additional resources</span></span>

* [<span data-ttu-id="ce1c3-236">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce1c3-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce1c3-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce1c3-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

