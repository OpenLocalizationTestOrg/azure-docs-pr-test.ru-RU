---
title: "Руководство по интеграции Azure Active Directory с FreshDesk | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f4b47e345a40b64f69ad8a4618564662b4a6c879
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="11147-103">Руководство по интеграции Azure Active Directory с FreshDesk</span><span class="sxs-lookup"><span data-stu-id="11147-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="11147-104">В этом руководстве описано, как интегрировать приложение FreshDesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11147-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11147-105">Интеграция Azure AD с FreshDesk обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="11147-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11147-106">С помощью Azure AD вы можете контролировать доступ к FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="11147-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="11147-107">Вы можете включить автоматический вход пользователей в FreshDesk (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11147-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11147-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="11147-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="11147-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11147-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11147-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="11147-110">Prerequisites</span></span>

<span data-ttu-id="11147-111">Чтобы настроить интеграцию Azure AD с FreshDesk, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="11147-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="11147-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="11147-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11147-113">подписка FreshDesk с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="11147-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11147-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="11147-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11147-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="11147-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11147-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="11147-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="11147-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11147-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11147-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="11147-118">Scenario description</span></span>
<span data-ttu-id="11147-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="11147-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11147-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="11147-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11147-121">Добавление FreshDesk из коллекции</span><span class="sxs-lookup"><span data-stu-id="11147-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="11147-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="11147-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="11147-123">Добавление FreshDesk из коллекции</span><span class="sxs-lookup"><span data-stu-id="11147-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="11147-124">Чтобы настроить интеграцию FreshDesk с Azure AD, необходимо добавить FreshDesk из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="11147-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11147-125">**Чтобы добавить FreshDesk из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="11147-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11147-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11147-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11147-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="11147-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11147-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="11147-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="11147-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="11147-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="11147-133">В поле поиска введите **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="11147-133">In the search box, type **FreshDesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="11147-135">На панели результатов выберите **FreshDesk** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="11147-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11147-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="11147-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11147-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение FreshDesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11147-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11147-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь во FreshDesk соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11147-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="11147-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="11147-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="11147-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** во FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="11147-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="11147-142">Чтобы настроить и проверить единый вход Azure AD в FreshDesk, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="11147-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11147-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="11147-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="11147-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11147-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11147-145">**[Создание тестового пользователя FreshDesk](#creating-a-freshdesk-test-user)** требуется для создания во FreshDesk пользователя Britta Simon, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11147-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="11147-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11147-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11147-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="11147-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11147-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="11147-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11147-149">В этом разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="11147-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="11147-150">**Чтобы настроить единый вход Azure AD во FreshDesk, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="11147-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="11147-151">На портале управления Azure на странице интеграции с приложением **FreshDesk** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="11147-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="11147-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="11147-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="11147-155">В разделе **Домены и URL-адреса приложения FreshDesk** введите в поле **URL-адрес для входа** значение `https://<tenant-name>.freshdesk.com` или любое другое значение, предлагаемое Freshdesk.</span><span class="sxs-lookup"><span data-stu-id="11147-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="11147-157">Обратите внимание, что это значение используется только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="11147-157">Please note that this is not the real value.</span></span> <span data-ttu-id="11147-158">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="11147-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="11147-159">Для получения этого значения обратитесь в [службу поддержки клиентов FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).</span><span class="sxs-lookup"><span data-stu-id="11147-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="11147-160">В разделе **Сертификат подписи SAML** щелкните **Сертификат**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="11147-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="11147-162">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="11147-162">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="11147-164">В разделе **Конфигурация FreshDesk** щелкните **Настроить FreshDesk**, чтобы открыть окно настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="11147-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="11147-165">Скопируйте URL-адрес службы единого входа SAML и URL-адрес выхода из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="11147-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="11147-167">В другом окне браузера войдите на свой корпоративный веб-сайт Freshdesk в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="11147-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="11147-168">В верхнем меню щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="11147-168">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="11147-169">![Администратор](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="11147-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="11147-170">На вкладке **General Settings** (Общие параметры) щелкните **Security** (Безопасность).</span><span class="sxs-lookup"><span data-stu-id="11147-170">In the **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="11147-171">![Безопасность](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="11147-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="11147-172">В разделе **Security** (Безопасность) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="11147-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="11147-173">![Единый вход](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="11147-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="11147-174">а.</span><span class="sxs-lookup"><span data-stu-id="11147-174">a.</span></span> <span data-ttu-id="11147-175">Выберите для параметра **Single Sign On (SSO)** (Единый вход) значение **On** (Включено).</span><span class="sxs-lookup"><span data-stu-id="11147-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="11147-176">b.</span><span class="sxs-lookup"><span data-stu-id="11147-176">b.</span></span> <span data-ttu-id="11147-177">Выберите **Единый вход SAML**.</span><span class="sxs-lookup"><span data-stu-id="11147-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="11147-178">c.</span><span class="sxs-lookup"><span data-stu-id="11147-178">c.</span></span> <span data-ttu-id="11147-179">Введите **URL-адрес службы единого входа SAML**, скопированный на портале Azure, в текстовое поле **SAML Login URL** (URL-адрес входа SAML).</span><span class="sxs-lookup"><span data-stu-id="11147-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="11147-180">d.</span><span class="sxs-lookup"><span data-stu-id="11147-180">d.</span></span> <span data-ttu-id="11147-181">Введите **URL-адрес выхода**, скопированный на портале Azure, в текстовое поле **Logout URL** (URL-адрес выхода).</span><span class="sxs-lookup"><span data-stu-id="11147-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="11147-182">д.</span><span class="sxs-lookup"><span data-stu-id="11147-182">e.</span></span> <span data-ttu-id="11147-183">Скопируйте значение поля **Thumbprint** (Отпечаток) из скачанного с портала Azure сертификата и вставьте его в текстовое поле **Security Certificate Fingerprint** (Отпечаток сертификата безопасности).</span><span class="sxs-lookup"><span data-stu-id="11147-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="11147-184">Дополнительные сведения см. в статье [Практическое руководство. Извлечение отпечатка сертификата](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="11147-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="11147-185">f.</span><span class="sxs-lookup"><span data-stu-id="11147-185">f.</span></span> <span data-ttu-id="11147-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="11147-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11147-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="11147-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="11147-188">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11147-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="11147-190">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="11147-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11147-191">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11147-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11147-193">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="11147-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11147-195">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="11147-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11147-197">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="11147-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11147-199">а.</span><span class="sxs-lookup"><span data-stu-id="11147-199">a.</span></span> <span data-ttu-id="11147-200">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11147-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11147-201">b.</span><span class="sxs-lookup"><span data-stu-id="11147-201">b.</span></span> <span data-ttu-id="11147-202">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11147-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11147-203">c.</span><span class="sxs-lookup"><span data-stu-id="11147-203">c.</span></span> <span data-ttu-id="11147-204">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="11147-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="11147-205">d.</span><span class="sxs-lookup"><span data-stu-id="11147-205">d.</span></span> <span data-ttu-id="11147-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="11147-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="11147-207">Создание тестового пользователя FreshDesk</span><span class="sxs-lookup"><span data-stu-id="11147-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="11147-208">Чтобы пользователи Azure AD могли входить во FreshDesk, их необходимо подготовить во FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="11147-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="11147-209">В случае с FreshDesk подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="11147-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="11147-210">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="11147-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="11147-211">Выполните вход в клиент **Freshdesk** .</span><span class="sxs-lookup"><span data-stu-id="11147-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="11147-212">В верхнем меню щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="11147-212">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="11147-213">![Администратор](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="11147-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="11147-214">На вкладке **General Settings** (Общие параметры) выберите **Agents** (Агенты).</span><span class="sxs-lookup"><span data-stu-id="11147-214">In the **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="11147-215">![Агенты](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Агенты")</span><span class="sxs-lookup"><span data-stu-id="11147-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="11147-216">Нажмите **Создать агента**.</span><span class="sxs-lookup"><span data-stu-id="11147-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="11147-217">![Создание агента](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Создание агента")</span><span class="sxs-lookup"><span data-stu-id="11147-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="11147-218">В диалоговом окне "Сведения об агенте " выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="11147-218">On the Agent Information dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="11147-219">![Сведения об агенте](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Сведения об агенте")</span><span class="sxs-lookup"><span data-stu-id="11147-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="11147-220">а.</span><span class="sxs-lookup"><span data-stu-id="11147-220">a.</span></span> <span data-ttu-id="11147-221">В текстовое поле **Полное имя** введите имя учетной записи Azure AD, которую желаете подготовить.</span><span class="sxs-lookup"><span data-stu-id="11147-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="11147-222">b.</span><span class="sxs-lookup"><span data-stu-id="11147-222">b.</span></span> <span data-ttu-id="11147-223">В текстовое поле **Электронная почта** введите адрес электронной почты той учетной записи Azure AD, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="11147-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="11147-224">c.</span><span class="sxs-lookup"><span data-stu-id="11147-224">c.</span></span> <span data-ttu-id="11147-225">В текстовое поле **Название** введите название учетной записи Azure AD, которую желаете подготовить.</span><span class="sxs-lookup"><span data-stu-id="11147-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="11147-226">г)</span><span class="sxs-lookup"><span data-stu-id="11147-226">d.</span></span> <span data-ttu-id="11147-227">Выберите **Agents role** (Роль агента) и нажмите кнопку **Assign** (Назначить).</span><span class="sxs-lookup"><span data-stu-id="11147-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="11147-228">д.</span><span class="sxs-lookup"><span data-stu-id="11147-228">e.</span></span> <span data-ttu-id="11147-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="11147-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="11147-230">Владелец учетной записи Azure AD получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="11147-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="11147-231">Вы можете использовать любые другие средства создания учетной записи пользователя Freshdesk или API, предоставляемые Freshdesk, для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="11147-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="11147-232">во FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="11147-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="11147-233">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="11147-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="11147-234">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Box.</span><span class="sxs-lookup"><span data-stu-id="11147-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="11147-236">**Чтобы назначить пользователя Britta Simon во FreshDesk, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="11147-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="11147-237">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="11147-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="11147-239">В списке приложений выберите **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="11147-239">In the applications list, select **FreshDesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="11147-241">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="11147-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="11147-243">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="11147-243">Click **Add** button.</span></span> <span data-ttu-id="11147-244">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="11147-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="11147-246">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="11147-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="11147-247">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="11147-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11147-248">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="11147-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11147-249">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="11147-249">Testing single sign-on</span></span>

<span data-ttu-id="11147-250">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="11147-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="11147-251">Щелкнув элемент FreshDesk на панели доступа, вы автоматически войдете в приложение FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="11147-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11147-252">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="11147-252">Additional resources</span></span>

* [<span data-ttu-id="11147-253">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11147-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11147-254">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11147-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

