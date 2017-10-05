---
title: "Руководство. Интеграция Azure Active Directory с AirWatch | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1996ec97e7c0d94c5606ca43bb5956548f1f3712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="dab07-103">Руководство. Интеграция Azure Active Directory с AirWatch</span><span class="sxs-lookup"><span data-stu-id="dab07-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="dab07-104">В этом руководстве описано, как интегрировать AirWatch с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dab07-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dab07-105">Интеграция приложения AirWatch c Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="dab07-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dab07-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению AirWatch.</span><span class="sxs-lookup"><span data-stu-id="dab07-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="dab07-107">Вы можете включить автоматический вход пользователей в AirWatch (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dab07-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dab07-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dab07-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dab07-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dab07-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dab07-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dab07-110">Prerequisites</span></span>

<span data-ttu-id="dab07-111">Чтобы настроить интеграцию Azure AD с AirWatch, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="dab07-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="dab07-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dab07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dab07-113">подписка AirWatch с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dab07-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dab07-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="dab07-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dab07-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="dab07-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dab07-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dab07-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dab07-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dab07-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dab07-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dab07-118">Scenario description</span></span>
<span data-ttu-id="dab07-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dab07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dab07-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="dab07-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dab07-121">Добавление AirWatch из коллекции.</span><span class="sxs-lookup"><span data-stu-id="dab07-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="dab07-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dab07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="dab07-123">Добавление AirWatch из коллекции</span><span class="sxs-lookup"><span data-stu-id="dab07-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="dab07-124">Чтобы настроить интеграцию приложения AirWatch с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dab07-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dab07-125">**Добавление приложения AirWatch из коллекции**</span><span class="sxs-lookup"><span data-stu-id="dab07-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dab07-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dab07-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dab07-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="dab07-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dab07-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dab07-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dab07-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="dab07-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dab07-133">В поле поиска введите **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="dab07-133">In the search box, type **AirWatch**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="dab07-135">На панели результатов выберите **AirWatch** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="dab07-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dab07-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dab07-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dab07-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение AirWatch с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab07-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dab07-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в AirWatch соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dab07-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="dab07-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в AirWatch.</span><span class="sxs-lookup"><span data-stu-id="dab07-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="dab07-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в AirWatch.</span><span class="sxs-lookup"><span data-stu-id="dab07-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="dab07-142">Чтобы настроить и проверить единый вход Azure AD в AirWatch, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dab07-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dab07-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="dab07-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dab07-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab07-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dab07-145">**[Создание тестового пользователя AirWatch](#creating-a-airwatch-test-user)** требуется для создания в AirWatch пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dab07-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dab07-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dab07-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dab07-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dab07-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dab07-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dab07-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dab07-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении AirWatch.</span><span class="sxs-lookup"><span data-stu-id="dab07-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="dab07-150">**Настройка единого входа Azure AD в AirWatch**</span><span class="sxs-lookup"><span data-stu-id="dab07-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="dab07-151">На портале Azure на странице интеграции с приложением **AirWatch** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="dab07-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dab07-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="dab07-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="dab07-155">В разделе **Домены и URL-адреса приложения AirWatch** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dab07-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="dab07-157">а.</span><span class="sxs-lookup"><span data-stu-id="dab07-157">a.</span></span> <span data-ttu-id="dab07-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="dab07-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="dab07-159">b.</span><span class="sxs-lookup"><span data-stu-id="dab07-159">b.</span></span> <span data-ttu-id="dab07-160">В текстовом поле **Идентификатор** введите значение `AirWatch`.</span><span class="sxs-lookup"><span data-stu-id="dab07-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dab07-161">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="dab07-161">This value is not the real.</span></span> <span data-ttu-id="dab07-162">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="dab07-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="dab07-163">Для получения этого значения обратитесь в [службу поддержки клиентов AirWatch](http://www.air-watch.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="dab07-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="dab07-164">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dab07-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="dab07-166">В разделе **Конфигурация AirWatch** щелкните **Настроить AirWatch**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dab07-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dab07-167">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="dab07-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="dab07-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dab07-169">Click **Save** button.</span></span>

    <span data-ttu-id="dab07-170">![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="dab07-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="dab07-171">В другом окне веб-браузера войдите на корпоративный веб-сайт AirWatch с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="dab07-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="dab07-172">На панели навигации слева щелкните **Accounts** (Учетные записи), а затем — **Administrators** (Администраторы).</span><span class="sxs-lookup"><span data-stu-id="dab07-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="dab07-173">![Администраторы](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Администраторы")</span><span class="sxs-lookup"><span data-stu-id="dab07-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="dab07-174">Разверните меню **Settings** (Параметры) и выберите пункт **Directory Services** (Службы каталогов).</span><span class="sxs-lookup"><span data-stu-id="dab07-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="dab07-175">![Параметры](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="dab07-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="dab07-176">Откройте вкладку **User** (Пользователь), введите в текстовое поле **Base DN** (Базовое доменное имя) используемое доменное имя и щелкните **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="dab07-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="dab07-177">![Пользователь](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="dab07-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="dab07-178">Откройте вкладку **Server** (Сервер).</span><span class="sxs-lookup"><span data-stu-id="dab07-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="dab07-179">![Сервер](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Сервер")</span><span class="sxs-lookup"><span data-stu-id="dab07-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="dab07-180">Выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dab07-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="dab07-181">![Передача](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Передача")</span><span class="sxs-lookup"><span data-stu-id="dab07-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="dab07-182">а.</span><span class="sxs-lookup"><span data-stu-id="dab07-182">a.</span></span> <span data-ttu-id="dab07-183">Для параметра **Directory Type** (Тип каталога) выберите значение **None** (Нет).</span><span class="sxs-lookup"><span data-stu-id="dab07-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="dab07-184">b.</span><span class="sxs-lookup"><span data-stu-id="dab07-184">b.</span></span> <span data-ttu-id="dab07-185">Установите флажок **Use SAML For Authentication**(Использовать SAML для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="dab07-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="dab07-186">c.</span><span class="sxs-lookup"><span data-stu-id="dab07-186">c.</span></span> <span data-ttu-id="dab07-187">Чтобы отправить скачанный сертификат, нажмите кнопку **Upload**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="dab07-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="dab07-188">В разделе **Request** (Запрос) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dab07-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="dab07-189">![Запрос](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Запрос")</span><span class="sxs-lookup"><span data-stu-id="dab07-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="dab07-190">а.</span><span class="sxs-lookup"><span data-stu-id="dab07-190">a.</span></span> <span data-ttu-id="dab07-191">Для параметра **Request Binding Type** (Тип привязки запроса) выберите значение **POST**.</span><span class="sxs-lookup"><span data-stu-id="dab07-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="dab07-192">b.</span><span class="sxs-lookup"><span data-stu-id="dab07-192">b.</span></span> <span data-ttu-id="dab07-193">На портале Azure на диалоговой странице **Настройка единого входа в AirWatch** скопируйте значение в поле **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML) и вставьте его в текстовое поле **Identity Provider Single Sign On URL** (URL-адрес единого входа для поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="dab07-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="dab07-194">c.</span><span class="sxs-lookup"><span data-stu-id="dab07-194">c.</span></span> <span data-ttu-id="dab07-195">Для параметра **NameID Format** (Формат идентификатора имени) выберите значение **Email Address** (Адрес электронной почты).</span><span class="sxs-lookup"><span data-stu-id="dab07-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="dab07-196">г)</span><span class="sxs-lookup"><span data-stu-id="dab07-196">d.</span></span> <span data-ttu-id="dab07-197">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dab07-197">Click **Save**.</span></span>

14. <span data-ttu-id="dab07-198">Снова откройте вкладку **Пользователь** .</span><span class="sxs-lookup"><span data-stu-id="dab07-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="dab07-199">![Пользователь](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="dab07-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="dab07-200">В разделе **Атрибут** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dab07-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="dab07-201">![Атрибут](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Атрибут")</span><span class="sxs-lookup"><span data-stu-id="dab07-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="dab07-202">а.</span><span class="sxs-lookup"><span data-stu-id="dab07-202">a.</span></span> <span data-ttu-id="dab07-203">В текстовом поле **Object Identifier** (Идентификатор объекта) введите **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="dab07-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="dab07-204">b.</span><span class="sxs-lookup"><span data-stu-id="dab07-204">b.</span></span> <span data-ttu-id="dab07-205">В текстовом поле **Username** (Имя пользователя) введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="dab07-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="dab07-206">c.</span><span class="sxs-lookup"><span data-stu-id="dab07-206">c.</span></span> <span data-ttu-id="dab07-207">В текстовом поле **Display Name** (Отображаемое имя) введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="dab07-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="dab07-208">г)</span><span class="sxs-lookup"><span data-stu-id="dab07-208">d.</span></span> <span data-ttu-id="dab07-209">В текстовом поле **First Name** (Имя) введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="dab07-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="dab07-210">д.</span><span class="sxs-lookup"><span data-stu-id="dab07-210">e.</span></span> <span data-ttu-id="dab07-211">В текстовом поле **Last Name** (Фамилия) введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="dab07-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="dab07-212">f.</span><span class="sxs-lookup"><span data-stu-id="dab07-212">f.</span></span> <span data-ttu-id="dab07-213">В текстовом поле **Email** (Электронная почта) введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="dab07-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="dab07-214">g.</span><span class="sxs-lookup"><span data-stu-id="dab07-214">g.</span></span> <span data-ttu-id="dab07-215">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dab07-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dab07-216">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dab07-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="dab07-217">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab07-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dab07-219">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dab07-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dab07-220">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dab07-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dab07-222">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="dab07-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dab07-224">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dab07-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dab07-226">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dab07-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dab07-228">а.</span><span class="sxs-lookup"><span data-stu-id="dab07-228">a.</span></span> <span data-ttu-id="dab07-229">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dab07-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dab07-230">b.</span><span class="sxs-lookup"><span data-stu-id="dab07-230">b.</span></span> <span data-ttu-id="dab07-231">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab07-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="dab07-232">c.</span><span class="sxs-lookup"><span data-stu-id="dab07-232">c.</span></span> <span data-ttu-id="dab07-233">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="dab07-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dab07-234">d.</span><span class="sxs-lookup"><span data-stu-id="dab07-234">d.</span></span> <span data-ttu-id="dab07-235">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dab07-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="dab07-236">Создание тестового пользователя AirWatch</span><span class="sxs-lookup"><span data-stu-id="dab07-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="dab07-237">Чтобы пользователи Azure AD могли выполнять вход в AirWatch, они должны быть подготовлены в AirWatch.</span><span class="sxs-lookup"><span data-stu-id="dab07-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="dab07-238">Подготовка в AirWatch выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="dab07-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="dab07-239">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="dab07-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="dab07-240">Выполните вход на корпоративном веб-сайте **AirWatch** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="dab07-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="dab07-241">На панели навигации слева щелкните **Accounts** (Учетные записи), а затем —**Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="dab07-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="dab07-242">![Пользователи](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="dab07-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="dab07-243">В меню **Users** (Пользователи) выберите пункт **List View** (Представление списка), а затем щелкните **Add \> Add User** (Добавить > Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="dab07-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="dab07-244">![Добавление пользователя](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="dab07-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="dab07-245">В диалоговом окне **Add / Edit User** (Добавление или изменение пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dab07-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="dab07-246">![Добавление пользователя](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="dab07-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="dab07-247">В текстовых полях **Username** (Имя пользователя), **Password** (Пароль), **Confirm Password** (Подтверждение пароля), **First Name** (Имя), **Last Name** (Фамилия) и **Email Address** (Адрес электронной почты) введите соответствующие данные действующей учетной записи Azure Active Directory, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="dab07-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="dab07-248">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dab07-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="dab07-249">Вы можете использовать любые другие средства создания учетной записи пользователя AirWatch или API, предоставляемые AirWatch для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="dab07-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dab07-250">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dab07-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dab07-251">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к AirWatch.</span><span class="sxs-lookup"><span data-stu-id="dab07-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dab07-253">**Назначение пользователя Britta Simon приложению AirWatch**</span><span class="sxs-lookup"><span data-stu-id="dab07-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="dab07-254">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dab07-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dab07-256">В списке приложений выберите **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="dab07-256">In the applications list, select **AirWatch**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="dab07-258">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dab07-258">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dab07-260">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dab07-260">Click **Add** button.</span></span> <span data-ttu-id="dab07-261">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dab07-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dab07-263">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dab07-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dab07-264">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dab07-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dab07-265">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dab07-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dab07-266">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dab07-266">Testing single sign-on</span></span>

<span data-ttu-id="dab07-267">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="dab07-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dab07-268">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="dab07-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="dab07-269">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dab07-269">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dab07-270">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dab07-270">Additional resources</span></span>

* [<span data-ttu-id="dab07-271">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dab07-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dab07-272">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dab07-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

