---
title: "Руководство по интеграции Azure Active Directory с Qlik Sense Enterprise | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Qlik Sense Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4964634cd5aaf0dbb98c766f5e12700c4d118750
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="5b840-103">Руководство. Интеграция Azure Active Directory с Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="5b840-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="5b840-104">В этом руководстве описано, как интегрировать Qlik Sense Enterprise с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b840-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b840-105">Интеграция Qlik Sense Enterprise с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5b840-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b840-106">С помощью Azure AD можно контролировать, кто будет иметь доступ к Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5b840-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="5b840-107">Вы можете включить автоматический вход пользователей в Qlik Sense Enterprise (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b840-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5b840-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5b840-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5b840-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b840-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b840-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5b840-110">Prerequisites</span></span>

<span data-ttu-id="5b840-111">Чтобы настроить интеграцию Azure AD с Qlik Sense Enterprise, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5b840-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="5b840-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5b840-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b840-113">подписка Qlik Sense Enterprise с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5b840-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b840-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5b840-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b840-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5b840-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b840-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5b840-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b840-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b840-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b840-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5b840-118">Scenario description</span></span>
<span data-ttu-id="5b840-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5b840-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b840-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5b840-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b840-121">Добавление Qlik Sense Enterprise из коллекции</span><span class="sxs-lookup"><span data-stu-id="5b840-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="5b840-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b840-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="5b840-123">Добавление Qlik Sense Enterprise из коллекции</span><span class="sxs-lookup"><span data-stu-id="5b840-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="5b840-124">Чтобы настроить интеграцию Qlik Sense Enterprise в Azure AD, необходимо добавить Qlik Sense Enterprise из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5b840-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b840-125">**Чтобы добавить Qlik Sense Enterprise из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5b840-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b840-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b840-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="5b840-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5b840-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b840-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5b840-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="5b840-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5b840-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="5b840-133">В поле поиска введите **Qlik Sense Enterprise**, выберите **Qlik Sense Enterprise** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="5b840-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![Qlik Sense Enterprise в списке результатов](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5b840-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b840-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5b840-136">В этом разделе описана настройка и проверка единого входа Azure AD в Qlik Sense Enterprise с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b840-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b840-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Qlik Sense Enterprise соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b840-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="5b840-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5b840-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="5b840-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5b840-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5b840-140">Чтобы настроить и проверить единый вход Azure AD в Qlik Sense Enterprise, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="5b840-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b840-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5b840-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5b840-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b840-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b840-143">**[Создание тестового пользователя Qlik Sense Enterprise](#create-a-qlik-sense-enterprise-test-user)** требуется для того, чтобы в Qlik Sense Enterprise существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b840-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b840-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b840-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b840-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5b840-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5b840-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b840-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5b840-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5b840-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="5b840-148">**Чтобы настроить единый вход Azure AD в Qlik Sense Enterprise, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5b840-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="5b840-149">На портале Azure на странице интеграции с приложением **Qlik Sense Enterprise** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5b840-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="5b840-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5b840-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="5b840-153">В разделе **Домены и URL-адреса приложения Qlik Sense Enterprise** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5b840-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах в приложении Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="5b840-155">а.</span><span class="sxs-lookup"><span data-stu-id="5b840-155">a.</span></span> <span data-ttu-id="5b840-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="5b840-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5b840-157">Обратите внимание на косую черту в конце этого URI.</span><span class="sxs-lookup"><span data-stu-id="5b840-157">Note the trailing slash at the end of this URI.</span></span> <span data-ttu-id="5b840-158">Она обязательная.</span><span class="sxs-lookup"><span data-stu-id="5b840-158">It is required.</span></span>
    
    <span data-ttu-id="5b840-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b840-159">b.</span></span> <span data-ttu-id="5b840-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="5b840-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="5b840-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5b840-161">These values are not real.</span></span> <span data-ttu-id="5b840-162">Вместо этих значений укажите фактические идентификатор и URL-адрес ответа, к которым мы вернемся позже в этом руководстве, или обратитесь к [группе поддержки Qlik Sense Enterprise](https://www.qlik.com/us/services/support), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="5b840-162">Update these values with the actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span> 

4. <span data-ttu-id="5b840-163">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5b840-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="5b840-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5b840-165">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b840-167">Подготовьте XML-файл метаданных федерации для отправки на сервер Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5b840-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5b840-168">Перед отправкой метаданных IdP на сервер Qlik Sense файл необходимо изменить. В нем нужно удалить определенные сведения, чтобы обеспечить корректное взаимодействие Azure AD и сервера Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5b840-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="5b840-170">а.</span><span class="sxs-lookup"><span data-stu-id="5b840-170">a.</span></span> <span data-ttu-id="5b840-171">Откройте в текстовом редакторе файл FederationMetaData.xml, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5b840-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="5b840-172">b.</span><span class="sxs-lookup"><span data-stu-id="5b840-172">b.</span></span> <span data-ttu-id="5b840-173">Найдите значение **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="5b840-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="5b840-174">Вы найдете четыре записи (две пары открывающих и закрывающих тегов для элементов).</span><span class="sxs-lookup"><span data-stu-id="5b840-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="5b840-175">c.</span><span class="sxs-lookup"><span data-stu-id="5b840-175">c.</span></span> <span data-ttu-id="5b840-176">Удалите теги RoleDescriptor и все данные между ними из файла.</span><span class="sxs-lookup"><span data-stu-id="5b840-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="5b840-177">г)</span><span class="sxs-lookup"><span data-stu-id="5b840-177">d.</span></span> <span data-ttu-id="5b840-178">Сохраните файл и держите его под рукой для дальнейшего использования в этом документе.</span><span class="sxs-lookup"><span data-stu-id="5b840-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="5b840-179">Перейдите к консоли управления Qlik Management Console (QMC) Qlik Sense как пользователь с возможностью создания конфигураций виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="5b840-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="5b840-180">В QMC щелкните пункт меню **Virtual Proxies** (Виртуальные прокси-серверы).</span><span class="sxs-lookup"><span data-stu-id="5b840-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="5b840-182">В нижней части страницы нажмите кнопку **Create new** (Создать).</span><span class="sxs-lookup"><span data-stu-id="5b840-182">At the bottom of the screen, click the **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="5b840-184">Появится экран Virtual proxy edit (Редактирование виртуального прокси-сервера).</span><span class="sxs-lookup"><span data-stu-id="5b840-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="5b840-185">В правой части экрана расположено меню для отображения параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5b840-185">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="5b840-187">Установите галочку возле пункта меню Identification (Идентификация) и введите идентифицирующие сведения для конфигурации виртуального прокси-сервера Azure.</span><span class="sxs-lookup"><span data-stu-id="5b840-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="5b840-189">а.</span><span class="sxs-lookup"><span data-stu-id="5b840-189">a.</span></span> <span data-ttu-id="5b840-190">В поле **Description** (Описание) укажите понятное имя для конфигурации виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="5b840-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="5b840-191">Введите значение в поле Description (Описание).</span><span class="sxs-lookup"><span data-stu-id="5b840-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="5b840-192">b.</span><span class="sxs-lookup"><span data-stu-id="5b840-192">b.</span></span> <span data-ttu-id="5b840-193">Значение в поле **Prefix** (Префикс) определяет конечную точку виртуального прокси-сервера для подключения к Qlik Sense с использованием единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b840-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="5b840-194">Введите уникальное имя префикса для этого виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="5b840-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="5b840-195">c.</span><span class="sxs-lookup"><span data-stu-id="5b840-195">c.</span></span> <span data-ttu-id="5b840-196">**Session inactivity timeout (minutes)** (Время ожидания при бездействии сеанса (в минутах)) — это время для ожидания подключений через этот виртуальный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="5b840-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="5b840-197">d.</span><span class="sxs-lookup"><span data-stu-id="5b840-197">d.</span></span> <span data-ttu-id="5b840-198">**Session cookie header name** (Имя заголовка сеанса в файле cookie) — имя cookie, которое содержит идентификатор для сеанса Qlik Sense, полученный пользователем после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5b840-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="5b840-199">Это имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="5b840-199">This name must be unique.</span></span>

12. <span data-ttu-id="5b840-200">Щелкните пункт меню Authentication (Проверка подлинности), чтобы сделать его видимым.</span><span class="sxs-lookup"><span data-stu-id="5b840-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="5b840-201">Появится экран Authentication (Проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="5b840-201">The Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="5b840-203">а.</span><span class="sxs-lookup"><span data-stu-id="5b840-203">a.</span></span> <span data-ttu-id="5b840-204">Значение в раскрывающемся списке **Anonymous access mode** (Режим анонимного доступа) определяет, могут ли анонимные пользователи получить доступ к Qlik Sense через виртуальный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="5b840-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="5b840-205">Параметр по умолчанию — No anonymous user (Без анонимных пользователей).</span><span class="sxs-lookup"><span data-stu-id="5b840-205">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="5b840-206">b.</span><span class="sxs-lookup"><span data-stu-id="5b840-206">b.</span></span> <span data-ttu-id="5b840-207">В раскрывающемся меню **Authentication method** (Метод аутентификации) следует выбрать схему аутентификации, которую будет использовать виртуальный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="5b840-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="5b840-208">Выберите в этом списке элемент SAML.</span><span class="sxs-lookup"><span data-stu-id="5b840-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="5b840-209">После этого появятся дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="5b840-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="5b840-210">c.</span><span class="sxs-lookup"><span data-stu-id="5b840-210">c.</span></span> <span data-ttu-id="5b840-211">В поле **SAML host URI** (URI узла SAML) введите имя узла, которое пользователи будут вводить для доступа к Qlik Sense через этот виртуальный прокси-сервер SAML.</span><span class="sxs-lookup"><span data-stu-id="5b840-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="5b840-212">Имя узла представляет собой URI сервера Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5b840-212">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="5b840-213">d.</span><span class="sxs-lookup"><span data-stu-id="5b840-213">d.</span></span> <span data-ttu-id="5b840-214">В поле **SAML entity ID** (Идентификатор сущности SAML) введите то же значение, что и в поле SAML host URI (URI узла SAML).</span><span class="sxs-lookup"><span data-stu-id="5b840-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="5b840-215">д.</span><span class="sxs-lookup"><span data-stu-id="5b840-215">e.</span></span> <span data-ttu-id="5b840-216">**SAML IdP metadata** (Метаданные IdP SAML) — это файл, измененный ранее в разделе **Изменение метаданных федерации из конфигурации Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="5b840-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="5b840-217">**Перед отправкой метаданных IdP файл необходимо изменить.** В нем нужно удалить определенные сведения, чтобы обеспечить корректное взаимодействие между Azure AD и сервером Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5b840-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="5b840-218">**Если файл нужно изменить, см. инструкции выше.**</span><span class="sxs-lookup"><span data-stu-id="5b840-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="5b840-219">Если файл изменен, щелкните кнопку Browse (Обзор) и выберите измененный файл метаданных для передачи в конфигурацию виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="5b840-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="5b840-220">f.</span><span class="sxs-lookup"><span data-stu-id="5b840-220">f.</span></span> <span data-ttu-id="5b840-221">Введите имя атрибута или ссылку на схему для атрибута SAML, представляющего **идентификатор пользователя**, который Azure AD отправит на сервер Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5b840-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="5b840-222">Сведения о ссылке на схему доступны в постконфигурации экранов приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="5b840-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="5b840-223">Чтобы использовать атрибут имени, введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="5b840-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="5b840-224">ж.</span><span class="sxs-lookup"><span data-stu-id="5b840-224">g.</span></span> <span data-ttu-id="5b840-225">Введите значение для **каталога пользователя** , который будет присоединен к пользователям при проверке подлинности на сервере Qlik Sense с использованием Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b840-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="5b840-226">Жестко заданные значения нужно заключить в **квадратные скобки []**.</span><span class="sxs-lookup"><span data-stu-id="5b840-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="5b840-227">Чтобы использовать атрибут, отправленный в утверждении SAML Azure AD, введите имя атрибута в этом текстовом поле **без** квадратных скобок.</span><span class="sxs-lookup"><span data-stu-id="5b840-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="5b840-228">h.</span><span class="sxs-lookup"><span data-stu-id="5b840-228">h.</span></span> <span data-ttu-id="5b840-229">В раскрывающемся списке **SAML signing algorithm** (Алгоритм подписывания SAML) можно задать подписывание сертификата поставщика услуг (в этом случае сервер Qlik Sense) для конфигурации виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="5b840-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="5b840-230">Если сервер Qlik Sense использует доверенный сертификат, созданный с помощью Microsoft Enhanced RSA и AES Cryptographic Provider, измените алгоритм подписывания SAML на **SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="5b840-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="5b840-231">i.</span><span class="sxs-lookup"><span data-stu-id="5b840-231">i.</span></span> <span data-ttu-id="5b840-232">В разделе SAML attribute mapping (Сопоставление атрибутов SAML) можно отправлять дополнительные атрибуты, например группы, в Qlik Sense для использования в правилах безопасности.</span><span class="sxs-lookup"><span data-stu-id="5b840-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="5b840-233">Щелкните пункт меню **Load balancing** (Балансировка нагрузки), чтобы сделать его видимым.</span><span class="sxs-lookup"><span data-stu-id="5b840-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="5b840-234">Появится экран Load balancing (Балансировка нагрузки).</span><span class="sxs-lookup"><span data-stu-id="5b840-234">The Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="5b840-236">Нажмите кнопку **Add new server node** (Добавить новый узел сервера), выберите узел или узлы обработчика, на которые Qlik Sense будет отправлять сеансы для балансировки нагрузки, а затем нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="5b840-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="5b840-238">Щелкните пункт меню Advanced (Дополнительно), чтобы сделать его видимым.</span><span class="sxs-lookup"><span data-stu-id="5b840-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="5b840-239">Откроется экран Advanced (Дополнительно).</span><span class="sxs-lookup"><span data-stu-id="5b840-239">The Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="5b840-241">В разделе Host white list (Список разрешенных узлов) определяются имена принимаемых узлов при подключении к серверу Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5b840-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="5b840-242">**Введите имя узла, которое пользователи будут указывать при подключении к серверу Qlik Sense.**</span><span class="sxs-lookup"><span data-stu-id="5b840-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="5b840-243">Для имени узла указывается то же значение, что и для URI узла SAML, только без https://.</span><span class="sxs-lookup"><span data-stu-id="5b840-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="5b840-244">Щелкните кнопку **Apply** (Применить).</span><span class="sxs-lookup"><span data-stu-id="5b840-244">Click the **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="5b840-246">Нажмите кнопку OK (ОК), чтобы принять предупреждение о перезапуске прокси-серверов, связанных с виртуальным прокси-сервером.</span><span class="sxs-lookup"><span data-stu-id="5b840-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="5b840-248">В правой части экрана отображается меню Associated items (Связанные элементы).</span><span class="sxs-lookup"><span data-stu-id="5b840-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="5b840-249">Щелкните пункт меню **Proxies** (Прокси-серверы).</span><span class="sxs-lookup"><span data-stu-id="5b840-249">Click on the **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="5b840-251">Появится экран прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="5b840-251">The proxy screen appears.</span></span>  <span data-ttu-id="5b840-252">Щелкните кнопку **Link** (Связать) внизу, чтобы связать прокси-сервер с виртуальным прокси-сервером.</span><span class="sxs-lookup"><span data-stu-id="5b840-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="5b840-254">Выберите узел прокси-сервера, который будет поддерживать подключение к этому виртуальному прокси-серверу, и щелкните кнопку **Link** (Связать).</span><span class="sxs-lookup"><span data-stu-id="5b840-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="5b840-255">После установки связи прокси-сервер отобразится в списке связанных прокси-серверов.</span><span class="sxs-lookup"><span data-stu-id="5b840-255">After linking, the proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="5b840-258">Через 5–10 секунд появится сообщение об обновлении QMC.</span><span class="sxs-lookup"><span data-stu-id="5b840-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="5b840-259">Нажмите кнопку **Refresh QMC** (Обновить QMC).</span><span class="sxs-lookup"><span data-stu-id="5b840-259">Click the **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="5b840-261">После обновления QMC щелкните пункт меню **Virtual proxies** (Виртуальные прокси-серверы).</span><span class="sxs-lookup"><span data-stu-id="5b840-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="5b840-262">Новая запись виртуального прокси-сервера SAML указана в таблице на экране.</span><span class="sxs-lookup"><span data-stu-id="5b840-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="5b840-263">Выделите запись виртуального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="5b840-263">Single click on the virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="5b840-265">В нижней части экрана станет активной кнопка Download SP metadata (Скачать метаданные SP).</span><span class="sxs-lookup"><span data-stu-id="5b840-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="5b840-266">Щелкните **Download SP metadata** (Скачать метаданные SP), чтобы сохранить метаданные в файл.</span><span class="sxs-lookup"><span data-stu-id="5b840-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="5b840-268">Откройте файл метаданных SP.</span><span class="sxs-lookup"><span data-stu-id="5b840-268">Open the sp metadata file.</span></span>  <span data-ttu-id="5b840-269">Обратите внимание на записи **entityID** и **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="5b840-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="5b840-270">Значения этих записей должны быть эквивалентны **идентификатору** и **URL-адресу для входа** в конфигурации приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b840-270">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="5b840-271">Вставьте эти значения в разделе **Домены и URL-адреса приложения Qlik Sense Enterprise** в параметрах конфигурации приложения в Azure AD. Если они не совпадают, измените их через мастер настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b840-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="5b840-273">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5b840-273">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5b840-274">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5b840-274">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5b840-275">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5b840-275">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5b840-276">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b840-276">Create an Azure AD test user</span></span>
<span data-ttu-id="5b840-277">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b840-277">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="5b840-279">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5b840-279">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b840-280">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b840-280">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![Кнопка "Azure Active Directory"](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5b840-282">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5b840-282">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5b840-284">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5b840-284">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![Кнопка "Добавить"](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5b840-286">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="5b840-286">In the **User** dialog box, perform the following steps:</span></span>

   ![Диалоговое окно "Пользователь"](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="5b840-288">а.</span><span class="sxs-lookup"><span data-stu-id="5b840-288">a.</span></span> <span data-ttu-id="5b840-289">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b840-289">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="5b840-290">b.</span><span class="sxs-lookup"><span data-stu-id="5b840-290">b.</span></span> <span data-ttu-id="5b840-291">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b840-291">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="5b840-292">c.</span><span class="sxs-lookup"><span data-stu-id="5b840-292">c.</span></span> <span data-ttu-id="5b840-293">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5b840-293">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="5b840-294">г)</span><span class="sxs-lookup"><span data-stu-id="5b840-294">d.</span></span> <span data-ttu-id="5b840-295">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5b840-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="5b840-296">Создание тестового пользователя Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="5b840-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="5b840-297">В этом разделе описано, как создать пользователя Britta Simon в приложении Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5b840-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="5b840-298">Обратитесь в [службу поддержки Qlik Sense Enterprise](https://www.qlik.com/us/services/support), чтобы добавить пользователей для платформы Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5b840-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="5b840-299">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="5b840-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5b840-300">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b840-300">Assign the Azure AD test user</span></span>

<span data-ttu-id="5b840-301">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5b840-301">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="5b840-303">**Чтобы назначить Britta Simon в Qlik Sense Enterprise, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5b840-303">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="5b840-304">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5b840-304">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5b840-306">В списке приложений выберите **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="5b840-306">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![Ссылка на Qlik Sense Enterprise в списке приложений](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="5b840-308">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5b840-308">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="5b840-310">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5b840-310">Click **Add** button.</span></span> <span data-ttu-id="5b840-311">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5b840-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="5b840-313">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5b840-313">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b840-314">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5b840-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b840-315">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5b840-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5b840-316">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5b840-316">Test single sign-on</span></span>

<span data-ttu-id="5b840-317">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5b840-317">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5b840-318">Щелкнув плитку Qlik Sense Enterprise на панели доступа, вы автоматически войдете в приложение Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5b840-318">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5b840-319">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5b840-319">Additional resources</span></span>

* [<span data-ttu-id="5b840-320">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b840-320">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b840-321">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b840-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

