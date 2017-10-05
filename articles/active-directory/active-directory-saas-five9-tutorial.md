---
title: "Руководство по интеграции Azure Active Directory с Five9 Plus Adapter (CTI, Contact Center Agents) | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Five9 Plus Adapter (CTI, Contact Center Agents)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: d75163ea5eb3fa811e07861f06e6c4d5c758b898
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="54ac6-103">Руководство по интеграции Azure Active Directory с Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="54ac6-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="54ac6-104">В этом учебнике описано, как интегрировать Five9 Plus Adapter (CTI, Contact Center Agents) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54ac6-104">In this tutorial, you learn how to integrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54ac6-105">Интеграция Five9 Plus Adapter (CTI, Contact Center Agents) с Azure AD предоставляет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="54ac6-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54ac6-106">Вы можете управлять доступом к Five9 Plus Adapter (CTI, Contact Center Agents) в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54ac6-106">You can control in Azure AD who has access to Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="54ac6-107">Вы можете включить автоматический вход пользователей в Five9 Plus Adapter (CTI, Contact Center Agents) (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54ac6-107">You can enable your users to automatically get signed-on to Five9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54ac6-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="54ac6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="54ac6-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54ac6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54ac6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="54ac6-110">Prerequisites</span></span>

<span data-ttu-id="54ac6-111">Чтобы настроить интеграцию Azure AD с Five9 Plus Adapter (CTI, Contact Center Agents), вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="54ac6-111">To configure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need the following items:</span></span>

- <span data-ttu-id="54ac6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="54ac6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54ac6-113">подписка Five9 Plus Adapter (CTI, Contact Center Agents) с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="54ac6-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54ac6-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="54ac6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54ac6-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="54ac6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54ac6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="54ac6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54ac6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54ac6-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54ac6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="54ac6-118">Scenario description</span></span>
<span data-ttu-id="54ac6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="54ac6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54ac6-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="54ac6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54ac6-121">Добавление Five9 Plus Adapter (CTI, Contact Center Agents) из коллекции</span><span class="sxs-lookup"><span data-stu-id="54ac6-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
2. <span data-ttu-id="54ac6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="54ac6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-the-gallery"></a><span data-ttu-id="54ac6-123">Добавление Five9 Plus Adapter (CTI, Contact Center Agents) из коллекции</span><span class="sxs-lookup"><span data-stu-id="54ac6-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
<span data-ttu-id="54ac6-124">Чтобы настроить интеграцию Five9 Plus Adapter (CTI, Contact Center Agents) с Azure AD, необходимо добавить Five9 Plus Adapter (CTI, Contact Center Agents) из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="54ac6-124">To configure the integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need to add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54ac6-125">**Чтобы добавить Five9 Plus Adapter (CTI, Contact Center Agents) из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-125">**To add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="54ac6-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54ac6-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="54ac6-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="54ac6-133">В поле поиска введите **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-133">In the search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="54ac6-135">На панели результатов выберите **Five9 Plus Adapter (CTI, Contact Center Agents)** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="54ac6-135">In the results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54ac6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="54ac6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54ac6-138">В этом разделе описана настройка и проверка единого входа Azure AD в Five9 Plus Adapter (CTI, Contact Center Agents) для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54ac6-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Five9 Plus Adapter (CTI, Contact Center Agents) соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54ac6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is to a user in Azure AD.</span></span> <span data-ttu-id="54ac6-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="54ac6-140">In other words, a link relationship between an Azure AD user and the related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs to be established.</span></span>

<span data-ttu-id="54ac6-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="54ac6-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54ac6-142">Чтобы настроить и проверить единый вход Azure AD в Five9 Plus Adapter (CTI, Contact Center Agents), вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="54ac6-142">To configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54ac6-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="54ac6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54ac6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54ac6-145">**[Создание тестового пользователя Five9 Plus Adapter (CTI, Contact Center Agents)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** требуется для того, чтобы в Five9 Plus Adapter (CTI, Contact Center Agents) существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54ac6-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - to have a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54ac6-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54ac6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54ac6-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="54ac6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="54ac6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="54ac6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="54ac6-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="54ac6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="54ac6-150">**Чтобы настроить единый вход Azure AD для Five9 Plus Adapter (CTI, Contact Center Agents), выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-150">**To configure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-151">На портале Azure на странице интеграции с приложением **Five9 Plus Adapter (CTI, Contact Center Agents)** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-151">In the Azure portal, on the **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="54ac6-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="54ac6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="54ac6-155">В разделе **Домены и URL-адреса Five9 Plus Adapter (CTI, Contact Center Agents)** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="54ac6-155">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="54ac6-157">а.</span><span class="sxs-lookup"><span data-stu-id="54ac6-157">a.</span></span> <span data-ttu-id="54ac6-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="54ac6-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span>

    |    <span data-ttu-id="54ac6-159">Среда</span><span class="sxs-lookup"><span data-stu-id="54ac6-159">Environment</span></span>      |       <span data-ttu-id="54ac6-160">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="54ac6-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="54ac6-161">Для "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="54ac6-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="54ac6-162">Для "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="54ac6-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="54ac6-163">Для "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="54ac6-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="54ac6-164">b.</span><span class="sxs-lookup"><span data-stu-id="54ac6-164">b.</span></span> <span data-ttu-id="54ac6-165">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="54ac6-165">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    |      <span data-ttu-id="54ac6-166">Среда</span><span class="sxs-lookup"><span data-stu-id="54ac6-166">Environment</span></span>     |      <span data-ttu-id="54ac6-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="54ac6-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="54ac6-168">Для "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="54ac6-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="54ac6-169">Для "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="54ac6-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="54ac6-170">Для "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="54ac6-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="54ac6-171">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="54ac6-171">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="54ac6-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="54ac6-173">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="54ac6-175">В разделе **Настройка Five9 Plus Adapter (CTI, Contact Center Agents)** щелкните **Настроить Five9 Plus Adapter (CTI, Contact Center Agents)**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-175">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="54ac6-176">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="54ac6-178">Чтобы настроить единый вход на стороне **Five9 Plus Adapter (CTI, Contact Center Agents)**, нужно отправить скачанный **сертификат (Base64), URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** в [службу поддержки Five9 Plus Adapter (CTI, Contact Center Agents)](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="54ac6-178">To configure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="54ac6-179">Для дальнейшей настройки единого входа выполните следующие действия в соответствии с адаптером:</span><span class="sxs-lookup"><span data-stu-id="54ac6-179">Also additionally, for configuring SSO further please follow the below steps according to the adapter:</span></span>

    <span data-ttu-id="54ac6-180">а.</span><span class="sxs-lookup"><span data-stu-id="54ac6-180">a.</span></span> <span data-ttu-id="54ac6-181">Руководство администратора "Five9 Plus Adapter for Agent Desktop Toolkit": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="54ac6-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="54ac6-182">b.</span><span class="sxs-lookup"><span data-stu-id="54ac6-182">b.</span></span> <span data-ttu-id="54ac6-183">Руководство администратора "Five9 Plus Adapter for Microsoft Dynamics CRM": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="54ac6-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="54ac6-184">c.</span><span class="sxs-lookup"><span data-stu-id="54ac6-184">c.</span></span> <span data-ttu-id="54ac6-185">Руководство администратора "Five9 Plus Adapter for Zendesk": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="54ac6-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="54ac6-186">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="54ac6-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54ac6-187">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="54ac6-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54ac6-188">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="54ac6-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54ac6-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="54ac6-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="54ac6-190">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="54ac6-192">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-193">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="54ac6-195">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="54ac6-197">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="54ac6-199">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="54ac6-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54ac6-201">а.</span><span class="sxs-lookup"><span data-stu-id="54ac6-201">a.</span></span> <span data-ttu-id="54ac6-202">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54ac6-203">b.</span><span class="sxs-lookup"><span data-stu-id="54ac6-203">b.</span></span> <span data-ttu-id="54ac6-204">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="54ac6-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54ac6-205">c.</span><span class="sxs-lookup"><span data-stu-id="54ac6-205">c.</span></span> <span data-ttu-id="54ac6-206">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="54ac6-207">d.</span><span class="sxs-lookup"><span data-stu-id="54ac6-207">d.</span></span> <span data-ttu-id="54ac6-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="54ac6-209">Создание тестового пользователя Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="54ac6-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="54ac6-210">В этом разделе вы создадите тестового пользователя по имени Britta Simon в Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="54ac6-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="54ac6-211">Чтобы добавить пользователей в Five9 Plus Adapter (CTI, Contact Center Agents), обратитесь в [службу поддержки Five9 Plus Adapter (CTI, Contact Center Agents)](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="54ac6-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add the users in the Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="54ac6-212">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="54ac6-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="54ac6-213">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="54ac6-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="54ac6-214">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="54ac6-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Five9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="54ac6-216">**Чтобы назначить пользователя Britta Simon в Five9 Plus Adapter (CTI, Contact Center Agents), выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="54ac6-216">**To assign Britta Simon to Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="54ac6-217">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="54ac6-219">В списке приложений выберите **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-219">In the applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="54ac6-221">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="54ac6-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-223">Click **Add** button.</span></span> <span data-ttu-id="54ac6-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="54ac6-226">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54ac6-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54ac6-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="54ac6-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="54ac6-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="54ac6-229">Testing single sign-on</span></span>

<span data-ttu-id="54ac6-230">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="54ac6-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54ac6-231">Щелкнув элемент "Five9 Plus Adapter (CTI, Contact Center Agents)" на панели доступа, вы автоматически войдете в приложение Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="54ac6-231">When you click the Five9 Plus Adapter (CTI, Contact Center Agents) tile in the Access Panel, you should get automatically signed-on to your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="54ac6-232">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54ac6-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54ac6-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="54ac6-233">Additional resources</span></span>

* [<span data-ttu-id="54ac6-234">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54ac6-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54ac6-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54ac6-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

