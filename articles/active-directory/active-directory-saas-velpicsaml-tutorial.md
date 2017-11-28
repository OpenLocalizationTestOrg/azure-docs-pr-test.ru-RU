---
title: "Руководство по интеграции Azure Active Directory с Velpic SAML | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="7a6ad-103">Руководство. Интеграция Azure Active Directory с Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="7a6ad-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="7a6ad-104">В этом руководстве описано, как интегрировать Velpic SAML с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a6ad-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a6ad-105">Интеграция Azure AD с приложением Velpic SAML обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7a6ad-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7a6ad-106">С помощью Azure AD вы можете контролировать доступ к Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="7a6ad-107">Вы можете включить автоматический вход пользователей в Velpic SAML (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a6ad-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="7a6ad-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a6ad-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a6ad-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a6ad-110">Prerequisites</span></span>

<span data-ttu-id="7a6ad-111">Чтобы настроить интеграцию Azure AD с Velpic SAML, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="7a6ad-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="7a6ad-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7a6ad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a6ad-113">подписка на приложение Velpic SAML с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a6ad-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a6ad-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7a6ad-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a6ad-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7a6ad-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a6ad-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a6ad-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7a6ad-118">Scenario description</span></span>
<span data-ttu-id="7a6ad-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a6ad-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="7a6ad-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a6ad-121">Добавление Velpic SAML из коллекции</span><span class="sxs-lookup"><span data-stu-id="7a6ad-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="7a6ad-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6ad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="7a6ad-123">Добавление Velpic SAML из коллекции</span><span class="sxs-lookup"><span data-stu-id="7a6ad-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="7a6ad-124">Чтобы настроить интеграцию Velpic SAML с Azure AD, необходимо добавить Velpic SAML из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7a6ad-125">**Чтобы добавить Velpic SAML из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7a6ad-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7a6ad-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7a6ad-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7a6ad-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7a6ad-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7a6ad-133">В поле поиска введите **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-133">In the search box, type **Velpic SAML**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="7a6ad-135">На панели результатов выберите **Velpic SAML** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a6ad-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6ad-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a6ad-138">В этом разделе описана настройка и проверка единого входа Azure AD в Velpic SAML с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a6ad-139">Для работы единого входа Azure AD необходимо знать, какой пользователь в Velpic SAML соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="7a6ad-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="7a6ad-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="7a6ad-142">Чтобы настроить и проверить единый вход Azure AD в Velpic SAML, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7a6ad-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7a6ad-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a6ad-145">**[Создание тестового пользователя Velpic SAML](#creating-a-velpic-saml-test-user)** требуется для создания в Velpic SAML пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7a6ad-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a6ad-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a6ad-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6ad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a6ad-149">В этом разделе описано, как включить единый вход в Azure AD на портале управления Azure и настроить его в приложении Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="7a6ad-150">**Чтобы настроить единый вход Azure AD в Velpic SAML, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7a6ad-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="7a6ad-151">На портале управления Azure на странице интеграции с приложением **Velpic SAML** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7a6ad-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="7a6ad-155">Введите сведения в разделе **Домены и URL-адреса приложения Velpic SAML**</span><span class="sxs-lookup"><span data-stu-id="7a6ad-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="7a6ad-157">а.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-157">a.</span></span> <span data-ttu-id="7a6ad-158">В текстовом поле **URL-адрес для входа** введите значение `https://<sub-domain>.velpicsaml.net`.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="7a6ad-159">b.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-159">b.</span></span> <span data-ttu-id="7a6ad-160">В текстовом поле **Идентификатор** вставьте значение параметра **URL-адрес единого входа**.`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="7a6ad-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7a6ad-161">Обратите внимание, что URL-адрес входа предоставляется командой поддержки Velpic SAML, а значение идентификатора станет доступно только после настройки подключаемого модуля единого входа на стороне Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="7a6ad-162">Скопируйте это значение на странице приложения Velpic SAML и вставьте в это поле.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="7a6ad-163">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="7a6ad-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7a6ad-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7a6ad-167">В разделе "Настройка Velpic SAML" щелкните "Настроить Velpic SAML", чтобы открыть окно "Настройка единого входа".</span><span class="sxs-lookup"><span data-stu-id="7a6ad-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="7a6ad-168">Скопируйте идентификатор сущности SAML из раздела "Краткий справочник".</span><span class="sxs-lookup"><span data-stu-id="7a6ad-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="7a6ad-169">В другом окне веб-браузера войдите на корпоративный сайт Velpic SAML с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="7a6ad-170">Щелкните вкладку **Manage** (Управление), перейдите к разделу **Integration** (Интеграция) и нажмите там кнопку **Plugins** (Подключаемые модули), чтобы создать новый подключаемый модуль для входа.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="7a6ad-172">Нажмите кнопку **Add plugin** (Добавить подключаемый модуль).</span><span class="sxs-lookup"><span data-stu-id="7a6ad-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="7a6ad-174">Щелкните плитку **SAML** на странице добавления подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="7a6ad-176">Введите имя нового подключаемого модуля SAML и нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="7a6ad-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="7a6ad-178">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="7a6ad-178">Enter the details as follows:</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="7a6ad-180">а.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-180">a.</span></span> <span data-ttu-id="7a6ad-181">В текстовом поле **Name** (Имя) введите имя подключаемого модуля SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="7a6ad-182">b.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-182">b.</span></span> <span data-ttu-id="7a6ad-183">В текстовом поле **Issuer URL** (URL-адрес издателя), вставьте **идентификатор сущности SAML**, который вы скопировали в окне **Настройка входа** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="7a6ad-184">c.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-184">c.</span></span> <span data-ttu-id="7a6ad-185">В поле **Provider Metadata Config** (Конфигурация поставщика метаданных) загрузите XML-файл метаданных, который вы скачали с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="7a6ad-186">d.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-186">d.</span></span> <span data-ttu-id="7a6ad-187">Также вы можете установить флажок **Auto create new users** (Автоматическое создание новых пользователей), чтобы включить JIT-подготовку SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="7a6ad-188">Если этот флаг не установлен, то при попытке входа в Velpic несуществующего пользователя из Azure произойдет ошибка входа.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="7a6ad-189">Если флаг установлен, новые пользователи будут автоматически создаваться для Velpic при первом входе.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="7a6ad-190">д.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-190">e.</span></span> <span data-ttu-id="7a6ad-191">Скопируйте значение из текстового поля **Single sign on URL** (URL-адрес единого входа) и вставьте его на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="7a6ad-192">f.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-192">f.</span></span> <span data-ttu-id="7a6ad-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a6ad-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6ad-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a6ad-195">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7a6ad-197">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7a6ad-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7a6ad-198">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a6ad-200">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a6ad-202">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a6ad-204">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a6ad-206">а.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-206">a.</span></span> <span data-ttu-id="7a6ad-207">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a6ad-208">b.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-208">b.</span></span> <span data-ttu-id="7a6ad-209">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a6ad-210">c.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-210">c.</span></span> <span data-ttu-id="7a6ad-211">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7a6ad-212">d.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-212">d.</span></span> <span data-ttu-id="7a6ad-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="7a6ad-214">Создание тестового пользователя Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="7a6ad-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="7a6ad-215">Этот шаг обычно не является обязательным, так как приложение поддерживает JIT-подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="7a6ad-216">Но если вы решите отключить автоматическую подготовку пользователей, то пользователя можно создать вручную, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="7a6ad-217">Войдите на корпоративный сайт Velpic SAML с правами администратора и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="7a6ad-218">Щелкните вкладку "Manage" (Управление) и перейдите в раздел "Users" (Пользователи), а затем нажмите кнопку "New" (Добавить), чтобы добавить пользователей.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![добавить пользователя](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="7a6ad-220">На странице **Create New User** (Создание пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="7a6ad-222">а.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-222">a.</span></span> <span data-ttu-id="7a6ad-223">В текстовое поле **First Name** (Имя) введите имя пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="7a6ad-224">b.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-224">b.</span></span> <span data-ttu-id="7a6ad-225">В текстовое поле **Last Name** (Фамилия) введите фамилию пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="7a6ad-226">c.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-226">c.</span></span> <span data-ttu-id="7a6ad-227">В текстовое поле **User Name** (Имя пользователя) введите имя пользователя для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="7a6ad-228">d.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-228">d.</span></span> <span data-ttu-id="7a6ad-229">В текстовом поле **Электронная почта** введите адрес электронной почты учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="7a6ad-230">д.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-230">e.</span></span> <span data-ttu-id="7a6ad-231">Все остальные данные являются необязательными, но вы можете внести их, если сочтете нужным.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="7a6ad-232">f.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-232">f.</span></span> <span data-ttu-id="7a6ad-233">Щелкните **СОХРАНИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7a6ad-234">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6ad-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7a6ad-235">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7a6ad-237">**Чтобы назначить пользователя Britta Simon в Velpic SAML, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="7a6ad-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="7a6ad-238">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7a6ad-240">Из списка приложений выберите **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="7a6ad-242">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7a6ad-244">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-244">Click **Add** button.</span></span> <span data-ttu-id="7a6ad-245">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7a6ad-247">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7a6ad-248">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a6ad-249">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a6ad-250">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7a6ad-250">Testing single sign-on</span></span>

<span data-ttu-id="7a6ad-251">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="7a6ad-252">Когда вы нажмете плитку Velpic SAML на панели доступа, должна появиться страница входа в приложение Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="7a6ad-253">На этой странице входа вы увидите кнопку **Log In With Azure AD** (Войти с помощью Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a6ad-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="7a6ad-255">Щелкните кнопку **Log In With Azure AD** (Войти с помощью Azure AD), чтобы войти в Velpic с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6ad-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7a6ad-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7a6ad-256">Additional resources</span></span>

* [<span data-ttu-id="7a6ad-257">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a6ad-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a6ad-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a6ad-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

