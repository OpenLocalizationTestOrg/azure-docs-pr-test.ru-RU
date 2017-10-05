---
title: "Руководство по интеграции Azure Active Directory с LinkedIn Elevate | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и LinkedIn Elevate."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 5336543e06d60be555722a615568b12048c2aa2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="875d8-103">Руководство по интеграции Azure Active Directory с LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="875d8-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="875d8-104">В этом руководстве описано, как интегрировать приложение LinkedIn Elevate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="875d8-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="875d8-105">Интеграция Azure AD с LinkedIn Elevate обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="875d8-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="875d8-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="875d8-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="875d8-107">Вы можете включить автоматический вход пользователей в LinkedIn Elevate (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="875d8-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="875d8-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="875d8-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="875d8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="875d8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="875d8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="875d8-110">Prerequisites</span></span>

<span data-ttu-id="875d8-111">Чтобы настроить интеграцию Azure AD с LinkedIn Elevate, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="875d8-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="875d8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="875d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="875d8-113">подписка LinkedIn Elevate с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="875d8-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="875d8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="875d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="875d8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="875d8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="875d8-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="875d8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="875d8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="875d8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="875d8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="875d8-118">Scenario description</span></span>
<span data-ttu-id="875d8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="875d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="875d8-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="875d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="875d8-121">Добавление LinkedIn Elevate из коллекции</span><span class="sxs-lookup"><span data-stu-id="875d8-121">Adding LinkedIn Elevate from the gallery</span></span>
2. <span data-ttu-id="875d8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="875d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="875d8-123">Добавление LinkedIn Elevate из коллекции</span><span class="sxs-lookup"><span data-stu-id="875d8-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="875d8-124">Чтобы настроить интеграцию приложения LinkedIn Elevate с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="875d8-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="875d8-125">**Добавление приложения LinkedIn Elevate из коллекции**</span><span class="sxs-lookup"><span data-stu-id="875d8-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="875d8-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="875d8-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="875d8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="875d8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="875d8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="875d8-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="875d8-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="875d8-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="875d8-133">В поле поиска введите **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="875d8-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="875d8-134">На панели результатов щелкните **LinkedIn Elevate**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="875d8-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="875d8-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="875d8-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="875d8-137">В этом разделе описана настройка и проверка единого входа Azure AD в приложение LinkedIn Elevate с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="875d8-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="875d8-138">Для работы единого входа службе Azure AD нужно знать, какой пользователь в LinkedIn Elevate соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="875d8-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="875d8-139">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="875d8-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="875d8-140">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="875d8-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="875d8-141">Чтобы настроить и проверить единый вход Azure AD в LinkedIn Elevate, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="875d8-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="875d8-142">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="875d8-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="875d8-143">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="875d8-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="875d8-144">**[Создание тестового пользователя LinkedIn Elevate](#creating-a-linkedin-elevate-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="875d8-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="875d8-145">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="875d8-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="875d8-146">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="875d8-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="875d8-147">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="875d8-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="875d8-148">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="875d8-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="875d8-149">**Настройка единого входа Azure AD в LinkedIn Elevate**</span><span class="sxs-lookup"><span data-stu-id="875d8-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="875d8-150">На портале управления Azure на странице интеграции с приложением **LinkedIn Elevate** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="875d8-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="875d8-152">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="875d8-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="875d8-154">В другом окне веб-браузера войдите в свой клиент LinkedIn Elevate с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="875d8-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="875d8-155">В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры).</span><span class="sxs-lookup"><span data-stu-id="875d8-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="875d8-156">Кроме того, выберите **Elevate — Elevate AAD Test** (Проверка Azure AD для Elevate) из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="875d8-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="875d8-158">Щелкните **OR Click Here to load and copy individual fields from the form** (Или щелкните здесь, чтобы загрузить и скопировать отдельные поля из формы) и скопируйте значения **Entity Id** (Идентификатор сущности) и **Assertion Consumer Service (ACS) Url** (URL-адрес службы обработчика утверждений (ACS)).</span><span class="sxs-lookup"><span data-stu-id="875d8-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="875d8-160">Если вы хотите настроить единый вход в режиме, **инициированном поставщиком удостоверений**, то на портале Azure в разделе **Домены и URL-адреса приложения LinkedIn Elevate** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="875d8-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="875d8-162">а.</span><span class="sxs-lookup"><span data-stu-id="875d8-162">a.</span></span> <span data-ttu-id="875d8-163">В текстовом поле **Идентификатор** введите **идентификатор сущности**, скопированный с портала LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="875d8-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="875d8-164">b.</span><span class="sxs-lookup"><span data-stu-id="875d8-164">b.</span></span> <span data-ttu-id="875d8-165">В текстовом поле **URL-адрес ответа** введите **URL-адрес службы обработчика утверждений (ACS)**, скопированный с портала LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="875d8-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="875d8-166">Если вы хотите настроить единый вход в режиме, **инициированном поставщиком услуг**, то установите флажок "Показать дополнительные параметры URL-адресов" в разделе настроек и настройте URL-адрес входа в таком формате:</span><span class="sxs-lookup"><span data-stu-id="875d8-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="875d8-168">Приложение LinkedIn Elevate ожидает утверждения SAML в определенном формате, а для этого вам нужно добавить настраиваемые сопоставления атрибутов в конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="875d8-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="875d8-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="875d8-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="875d8-170">По умолчанию **идентификатор пользователя** имеет значение **user.userprincipalname**, но для LinkedIn Elevate требуется сопоставить это значение с адресом электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="875d8-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="875d8-171">Для этого можно использовать атрибут **user.mail** из списка или соответствующее значение атрибута, основанное на конфигурации организации.</span><span class="sxs-lookup"><span data-stu-id="875d8-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="875d8-173">В разделе **Атрибуты пользователя** установите флажок **Просмотреть и изменить все другие атрибуты пользователей** и задайте эти атрибуты.</span><span class="sxs-lookup"><span data-stu-id="875d8-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="875d8-174">Необходимо также добавить утверждение с именем **department**, значение которого должно быть сопоставлено с **user.department**.</span><span class="sxs-lookup"><span data-stu-id="875d8-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="875d8-175">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="875d8-175">Attribute Name</span></span> | <span data-ttu-id="875d8-176">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="875d8-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="875d8-177">department</span><span class="sxs-lookup"><span data-stu-id="875d8-177">department</span></span>| <span data-ttu-id="875d8-178">user.department</span><span class="sxs-lookup"><span data-stu-id="875d8-178">user.department</span></span> |

      ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="875d8-180">а.</span><span class="sxs-lookup"><span data-stu-id="875d8-180">a.</span></span> <span data-ttu-id="875d8-181">Щелкните "Добавить атрибут", чтобы открыть страницу сведений об атрибутах. Добавьте атрибут department, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="875d8-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="875d8-183">b.</span><span class="sxs-lookup"><span data-stu-id="875d8-183">b.</span></span> <span data-ttu-id="875d8-184">Нажмите кнопку **ОК**, чтобы сохранить атрибут.</span><span class="sxs-lookup"><span data-stu-id="875d8-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="875d8-185">c.</span><span class="sxs-lookup"><span data-stu-id="875d8-185">c.</span></span> <span data-ttu-id="875d8-186">Измените имя атрибута **emailaddress** на **email**.</span><span class="sxs-lookup"><span data-stu-id="875d8-186">Change the name of the attribute **emailaddress** to **email**.</span></span>


10. <span data-ttu-id="875d8-187">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="875d8-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="875d8-189">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="875d8-189">Click **Save**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="875d8-191">Перейдите в раздел **LinkedIn Admin Settings** (Параметры администратора LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="875d8-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="875d8-192">Передайте XML-файл, скачанный с портала Azure. Для этого нажмите кнопку "Upload XML file" (Передать XML-файл).</span><span class="sxs-lookup"><span data-stu-id="875d8-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="875d8-194">Нажмите кнопку **On** (Включить), чтобы включить единый вход.</span><span class="sxs-lookup"><span data-stu-id="875d8-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="875d8-195">Состояние единого входа изменится с **Not Connected** (Не подключено) на **Connected** (Подключено.)</span><span class="sxs-lookup"><span data-stu-id="875d8-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="875d8-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="875d8-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="875d8-198">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="875d8-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="875d8-200">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="875d8-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="875d8-201">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="875d8-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="875d8-203">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="875d8-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="875d8-205">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="875d8-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="875d8-207">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="875d8-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="875d8-209">а.</span><span class="sxs-lookup"><span data-stu-id="875d8-209">a.</span></span> <span data-ttu-id="875d8-210">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="875d8-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="875d8-211">b.</span><span class="sxs-lookup"><span data-stu-id="875d8-211">b.</span></span> <span data-ttu-id="875d8-212">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="875d8-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="875d8-213">c.</span><span class="sxs-lookup"><span data-stu-id="875d8-213">c.</span></span> <span data-ttu-id="875d8-214">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="875d8-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="875d8-215">d.</span><span class="sxs-lookup"><span data-stu-id="875d8-215">d.</span></span> <span data-ttu-id="875d8-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="875d8-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="875d8-217">Создание тестового пользователя LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="875d8-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="875d8-218">Приложение Linked Elevate поддерживает JIT-подготовку пользователей, поэтому после аутентификации пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="875d8-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="875d8-219">На странице параметров администратора на портале LinkedIn Elevate включите параметр **Automatically assign licenses** (Автоматически назначать лицензии), чтобы активировать JIT-подготовку, одновременно с которой пользователю будет сразу назначена лицензия.</span><span class="sxs-lookup"><span data-stu-id="875d8-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>

   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="875d8-221">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="875d8-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="875d8-222">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="875d8-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="875d8-224">**Назначение пользователя Britta Simon приложению LinkedIn Elevate**</span><span class="sxs-lookup"><span data-stu-id="875d8-224">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="875d8-225">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="875d8-225">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="875d8-227">В списке приложений выберите **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="875d8-227">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="875d8-229">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="875d8-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="875d8-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="875d8-231">Click **Add** button.</span></span> <span data-ttu-id="875d8-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="875d8-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="875d8-234">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="875d8-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="875d8-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="875d8-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="875d8-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="875d8-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="875d8-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="875d8-237">Testing single sign-on</span></span>

<span data-ttu-id="875d8-238">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="875d8-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="875d8-239">Щелкнув элемент LinkedIn Elevate на панели доступа, вы перейдете на страницу входа Azure. Успешно выполнив вход, вы должны попасть в приложение LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="875d8-239">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="875d8-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="875d8-240">Additional resources</span></span>

* [<span data-ttu-id="875d8-241">Руководство по настройке LinkedIn Elevate для автоматической подготовки пользователей с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="875d8-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="875d8-242">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="875d8-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="875d8-243">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="875d8-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
