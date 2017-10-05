---
title: "Учебник. Интеграция Azure Active Directory с Evidence.com | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="95aa4-103">Руководство. Интеграция Azure Active Directory с Evidence.com</span><span class="sxs-lookup"><span data-stu-id="95aa4-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="95aa4-104">В этом руководстве описано, как интегрировать Evidence.com с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="95aa4-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95aa4-105">Интеграция Azure AD с приложением Evidence.com обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="95aa4-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="95aa4-106">С помощью Azure AD вы можете контролировать доступ к Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="95aa4-107">Вы можете включить автоматический вход пользователей в Evidence.com (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95aa4-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="95aa4-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="95aa4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="95aa4-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95aa4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95aa4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="95aa4-110">Prerequisites</span></span>

<span data-ttu-id="95aa4-111">Чтобы настроить интеграцию Azure AD с Evidence.com, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="95aa4-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="95aa4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="95aa4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95aa4-113">Подписка Evidence.com с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="95aa4-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95aa4-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="95aa4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95aa4-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="95aa4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95aa4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="95aa4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95aa4-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95aa4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95aa4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="95aa4-118">Scenario description</span></span>
<span data-ttu-id="95aa4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="95aa4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95aa4-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="95aa4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95aa4-121">Добавление Evidence.com из коллекции.</span><span class="sxs-lookup"><span data-stu-id="95aa4-121">Adding Evidence.com from the gallery</span></span>
2. <span data-ttu-id="95aa4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="95aa4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="95aa4-123">Добавление Evidence.com из коллекции</span><span class="sxs-lookup"><span data-stu-id="95aa4-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="95aa4-124">Чтобы настроить интеграцию Evidence.com с Azure AD, необходимо добавить Evidence.com из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="95aa4-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="95aa4-125">**Чтобы добавить Evidence.com из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="95aa4-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="95aa4-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="95aa4-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="95aa4-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="95aa4-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="95aa4-133">В поле поиска введите **Evidence.com**, на панели результатов выберите **Evidence.com** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="95aa4-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![Evidence.com в списке результатов](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="95aa4-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="95aa4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="95aa4-136">В этом разделе описана настройка и проверка единого входа Azure AD в Evidence.com с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95aa4-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95aa4-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Evidence.com соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95aa4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="95aa4-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="95aa4-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="95aa4-140">Чтобы настроить и проверить единый вход Azure AD в Evidence.com, необходимо выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="95aa4-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="95aa4-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="95aa4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="95aa4-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95aa4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95aa4-143">**[Создание тестового пользователя Evidence.com](#create-a-evidencecom-test-user)** требуется для того, чтобы в Evidence.com существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95aa4-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="95aa4-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95aa4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95aa4-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="95aa4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="95aa4-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="95aa4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="95aa4-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="95aa4-148">**Чтобы настроить единый вход Azure AD в Evidence.com, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="95aa4-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="95aa4-149">На портале Azure на странице интеграции с приложением **Evidence.com** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="95aa4-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="95aa4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="95aa4-153">В разделе **Домены и URL-адреса приложения Evidence.com** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="95aa4-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="95aa4-155">а.</span><span class="sxs-lookup"><span data-stu-id="95aa4-155">a.</span></span> <span data-ttu-id="95aa4-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="95aa4-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="95aa4-157">b.</span><span class="sxs-lookup"><span data-stu-id="95aa4-157">b.</span></span> <span data-ttu-id="95aa4-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="95aa4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="95aa4-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="95aa4-159">These values are not real.</span></span> <span data-ttu-id="95aa4-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="95aa4-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="95aa4-161">Чтобы получить их, обратитесь в [службу поддержки клиентов Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE).</span><span class="sxs-lookup"><span data-stu-id="95aa4-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

4. <span data-ttu-id="95aa4-162">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="95aa4-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="95aa4-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="95aa4-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="95aa4-166">В разделе **конфигурации Evidence.com** щелкните **Настроить Evidence.com**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="95aa4-167">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="95aa4-169">В отдельном окне браузера войдите в клиент Evidence.com с правами администратора и перейдите к вкладке **Admin** (Администрирование).</span><span class="sxs-lookup"><span data-stu-id="95aa4-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

8. <span data-ttu-id="95aa4-170">Щелкните **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="95aa4-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="95aa4-171">Выберите параметр **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="95aa4-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="95aa4-172">Скопируйте **идентификатор сущности SAML**, **URL-адрес службы единого входа SAML** и **URL-адрес выхода**, отображаемые на портале Azure, и добавьте их в соответствующие поля в приложении Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="95aa4-173">Откройте скачанный файл сертификата в кодировке Base64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в поле **Security Certificate** (Сертификат безопасности).</span><span class="sxs-lookup"><span data-stu-id="95aa4-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

12. <span data-ttu-id="95aa4-174">Сохраните конфигурацию в Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="95aa4-175">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="95aa4-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="95aa4-176">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="95aa4-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="95aa4-177">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="95aa4-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="95aa4-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="95aa4-178">Create an Azure AD test user</span></span>

<span data-ttu-id="95aa4-179">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95aa4-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="95aa4-181">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="95aa4-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="95aa4-182">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="95aa4-184">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="95aa4-186">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="95aa4-188">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="95aa4-188">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="95aa4-190">а.</span><span class="sxs-lookup"><span data-stu-id="95aa4-190">a.</span></span> <span data-ttu-id="95aa4-191">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95aa4-192">b.</span><span class="sxs-lookup"><span data-stu-id="95aa4-192">b.</span></span> <span data-ttu-id="95aa4-193">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95aa4-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="95aa4-194">c.</span><span class="sxs-lookup"><span data-stu-id="95aa4-194">c.</span></span> <span data-ttu-id="95aa4-195">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="95aa4-196">г)</span><span class="sxs-lookup"><span data-stu-id="95aa4-196">d.</span></span> <span data-ttu-id="95aa4-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="95aa4-198">Создание тестового пользователя Evidence.com</span><span class="sxs-lookup"><span data-stu-id="95aa4-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="95aa4-199">Чтобы пользователи Azure AD могли выполнять вход, нужно подготовить их для доступа в приложении Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="95aa4-200">В этом разделе описано, как создавать учетные записи пользователей Azure AD в Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="95aa4-201">**Чтобы подготовить учетную запись пользователя в Evidence.com, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="95aa4-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="95aa4-202">В окне веб-браузера войдите на корпоративный веб-сайт Evidence.com в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="95aa4-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="95aa4-203">Перейдите к вкладке **Admin** (Администрирование).</span><span class="sxs-lookup"><span data-stu-id="95aa4-203">Navigate to **Admin** tab.</span></span>

3. <span data-ttu-id="95aa4-204">Щелкните **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="95aa4-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="95aa4-205">Нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="95aa4-205">Click the **Add** button.</span></span>

5. <span data-ttu-id="95aa4-206">Параметр **Email Address** (Адрес электронной почты) для нового пользователя должен совпадать с именем пользователя в Azure AD, которому вы хотите предоставить доступ.</span><span class="sxs-lookup"><span data-stu-id="95aa4-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="95aa4-207">Возможно, в вашей организации в качестве имени пользователя не используется адрес электронной почты. Тогда зайдите на портале Azure в раздел **Evidence.com > Атрибуты > Единый вход** и измените параметр nameidentifier (идентификатор имени, отправляемый приложению Evidence.com) так, чтобы передавался именно адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="95aa4-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="95aa4-208">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="95aa4-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="95aa4-209">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="95aa4-211">**Чтобы назначить пользователя Britta Simon приложению Evidence.com, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="95aa4-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="95aa4-212">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="95aa4-214">В списке приложений выберите **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-214">In the applications list, select **Evidence.com**.</span></span>

    ![Ссылка Evidence.com в списке приложений](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="95aa4-216">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="95aa4-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-218">Click **Add** button.</span></span> <span data-ttu-id="95aa4-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="95aa4-221">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="95aa4-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95aa4-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="95aa4-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="95aa4-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="95aa4-224">Test single sign-on</span></span>

<span data-ttu-id="95aa4-225">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="95aa4-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="95aa4-226">Щелкнув элемент Evidence.com на панели доступа, вы автоматически войдете в приложение Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="95aa4-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="95aa4-227">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="95aa4-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="95aa4-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="95aa4-228">Additional resources</span></span>

* [<span data-ttu-id="95aa4-229">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95aa4-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95aa4-230">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95aa4-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

