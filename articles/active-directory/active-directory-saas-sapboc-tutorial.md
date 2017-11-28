---
title: "Руководство по интеграции Azure Active Directory с SAP Business Object Cloud | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в SAP Business Object Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: 6d517c5e302ac36e5bba2053998c75f8f4d42683
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="a853b-103">Руководство по интеграции Azure Active Directory с SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="a853b-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="a853b-104">В этом руководстве описано, как интегрировать SAP Business Object Cloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a853b-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a853b-105">Интеграция SAP Business Object Cloud с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a853b-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="a853b-106">С помощью Microsoft Azure AD вы можете контролировать доступ к приложению SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a853b-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span></span>
- <span data-ttu-id="a853b-107">Вы можете включить автоматический вход пользователей в SAP Business Object Cloud с использованием функции единого входа и учетной записи пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a853b-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="a853b-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a853b-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="a853b-109">Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a853b-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a853b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a853b-110">Prerequisites</span></span>

<span data-ttu-id="a853b-111">Чтобы настроить интеграцию Azure AD с SAP Business Object Cloud, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a853b-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span></span>

- <span data-ttu-id="a853b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a853b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a853b-113">подписка SAP Business Object Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a853b-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="a853b-114">Мы не рекомендуем использовать рабочую среду для проверки действий, выполняемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="a853b-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="a853b-115">Для проверки действий в этом руководстве соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a853b-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="a853b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a853b-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="a853b-117">Если у вас нет пробной среды Azure AD, вы можете [получить бесплатную пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a853b-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a853b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a853b-118">Scenario description</span></span>
<span data-ttu-id="a853b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a853b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="a853b-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a853b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a853b-121">Добавление SAP Business Object Cloud из коллекции.</span><span class="sxs-lookup"><span data-stu-id="a853b-121">Add SAP Business Object Cloud from the gallery.</span></span>
2. <span data-ttu-id="a853b-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a853b-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-the-gallery"></a><span data-ttu-id="a853b-123">Добавление SAP Business Object Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="a853b-123">Add SAP Business Object Cloud from the gallery</span></span>
<span data-ttu-id="a853b-124">Чтобы настроить интеграцию SAP Business Object Cloud с Azure AD, в коллекции необходимо добавить SAP Business Object Cloud в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a853b-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a853b-125">Чтобы добавить SAP Business Object Cloud из коллекции, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a853b-125">To add SAP Business Object Cloud from the gallery:</span></span>

1. <span data-ttu-id="a853b-126">На [портале Azure](https://portal.azure.com) в меню слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a853b-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="a853b-128">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a853b-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Страница "Корпоративные приложения"][2]
    
3. <span data-ttu-id="a853b-130">Чтобы добавить новое приложение, выберите **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="a853b-130">To add a new application, select **New application**.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="a853b-132">В поле поиска введите **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a853b-132">In the search box, enter **SAP Business Object Cloud**.</span></span>

    ![Поле поиска](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="a853b-134">В области результатов выберите **SAP Business Object Cloud** и **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a853b-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business Object Cloud в списке результатов](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a853b-136">Настройка и проверка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="a853b-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="a853b-137">В этом разделе описана настройка и проверка единого входа Azure AD в SAP Business Object Cloud с использованием тестового пользователя *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="a853b-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="a853b-138">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Microsoft Azure AD соответствует пользователю в SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a853b-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="a853b-139">Необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a853b-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="a853b-140">Для этого назначьте **имя пользователя** в Microsoft Azure AD в качестве значения **имени пользователя** в SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a853b-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="a853b-141">Чтобы настроить и проверить единый вход Azure AD в SAP Business Object Cloud, выполните следующие задания:</span><span class="sxs-lookup"><span data-stu-id="a853b-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span></span>

1. <span data-ttu-id="a853b-142">[Настройка единого входа Azure AD](#set-up-azure-ad-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="a853b-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="a853b-143">необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a853b-143">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="a853b-144">[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)</span><span class="sxs-lookup"><span data-stu-id="a853b-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="a853b-145">требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a853b-145">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="a853b-146">[Создание тестового пользователя SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user)</span><span class="sxs-lookup"><span data-stu-id="a853b-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="a853b-147">требуется для создания пользователя Britta Simon в SAP Business Object Cloud, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a853b-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="a853b-148">[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)</span><span class="sxs-lookup"><span data-stu-id="a853b-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="a853b-149">позволяет пользователю Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a853b-149">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a853b-150">[Проверка единого входа](#test-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="a853b-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="a853b-151">необходима, чтобы убедиться, что конфигурация работает правильно.</span><span class="sxs-lookup"><span data-stu-id="a853b-151">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="a853b-152">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="a853b-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="a853b-153">В этом разделе описано, как включить единый вход Azure AD на портале Azure</span><span class="sxs-lookup"><span data-stu-id="a853b-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="a853b-154">и настроить его в приложении SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a853b-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="a853b-155">Чтобы настроить единый вход Azure AD в SAP Business Object Cloud, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a853b-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="a853b-156">На портале Azure на странице интеграции с приложением **SAP Business Object Cloud** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a853b-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Выбор параметра "Единый вход"][4]

2. <span data-ttu-id="a853b-158">На странице **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**.</span><span class="sxs-lookup"><span data-stu-id="a853b-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Выбор параметра "Вход на основе SAML"](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="a853b-160">В разделе **Домены и URL-адреса приложения SAP Business Object Cloud** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a853b-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span></span>

    1. <span data-ttu-id="a853b-161">В поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="a853b-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="a853b-162">В поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="a853b-162">In the **Identifier** box, enter a URL that has the following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![Домены и URL-адреса приложения SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="a853b-164">Значения этих URL-адресов приведены только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a853b-164">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="a853b-165">Замените эти значения фактическим URL-адресом для входа и URL-адресом идентификатора.</span><span class="sxs-lookup"><span data-stu-id="a853b-165">Update the values with the actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="a853b-166">Чтобы получить URL-адрес для входа, обратитесь в [службу поддержки клиентов SAP Business Object Cloud](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="a853b-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="a853b-167">Вы можете получить URL-адрес идентификатора при загрузке метаданных SAP Business Object Cloud из консоли администрирования.</span><span class="sxs-lookup"><span data-stu-id="a853b-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span></span> <span data-ttu-id="a853b-168">Это объясняется далее в руководстве.</span><span class="sxs-lookup"><span data-stu-id="a853b-168">This is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="a853b-169">В разделе **Сертификат подписи SAML** выберите **XML метаданных**.</span><span class="sxs-lookup"><span data-stu-id="a853b-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="a853b-170">Затем сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a853b-170">Then, save the metadata file on your computer.</span></span>

    ![Выбор XML метаданных](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="a853b-172">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a853b-172">Select **Save**.</span></span>

    ![Нажатие кнопки "Сохранить"](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a853b-174">В другом окне браузера войдите на сайт SAP Business Object Cloud своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="a853b-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="a853b-175">Выберите **Меню** > **Система** > **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="a853b-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Выбор параметров "Меню", "Система" и "Администрирование"](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="a853b-177">На вкладке **Безопасность** щелкните значок пера **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="a853b-177">On the **Security** tab, select the **Edit** (pen) icon.</span></span>
    
    ![Выбор значка пера "Изменить" на вкладке "Безопасность"](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="a853b-179">В качестве **метода проверки подлинности** выберите **SAML Single Sign-On (SSO)** (Единый вход SAML (SSO)).</span><span class="sxs-lookup"><span data-stu-id="a853b-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Выбор параметра SAML Single Sign-On (SSO) (Единый вход SAML (SSO)) в качестве метода проверки подлинности](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="a853b-181">Нажмите кнопку **Загрузить** для загрузки метаданных поставщика услуг (шаг 1).</span><span class="sxs-lookup"><span data-stu-id="a853b-181">To download the service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="a853b-182">В файле метаданных найдите и скопируйте значение **EntityID**</span><span class="sxs-lookup"><span data-stu-id="a853b-182">In the metadata file, find and copy the **entityID** value.</span></span> <span data-ttu-id="a853b-183">и вставьте его в поле **Идентификатор** на портале Azure в разделе **Домены и URL-адреса приложения SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a853b-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span></span>

    ![Копирование и вставка значения EntityID](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="a853b-185">Чтобы отправить метаданные поставщика услуг (шаг 2) в файл, загруженный с портала Azure, в разделе **Upload Identity Provider metadata** (Отправить метаданные поставщика удостоверений) нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="a853b-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Нажатие кнопки "Отправить" в разделе Upload Identity Provider metadata (Отправить метаданные поставщика удостоверений)](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="a853b-187">В списке **Атрибут пользователя** выберите атрибут пользователя (шаг 3), который хотите использовать в своей реализации.</span><span class="sxs-lookup"><span data-stu-id="a853b-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span></span> <span data-ttu-id="a853b-188">Этот атрибут пользователя сопоставляется с поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="a853b-188">This user attribute maps to the identity provider.</span></span> <span data-ttu-id="a853b-189">Чтобы ввести пользовательский атрибут на странице пользователя, используйте параметр **Custom SAML Mapping** (Пользовательское сопоставление SAML).</span><span class="sxs-lookup"><span data-stu-id="a853b-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span></span> <span data-ttu-id="a853b-190">Или выберите **Email** или **USER ID** в качестве пользовательского атрибута.</span><span class="sxs-lookup"><span data-stu-id="a853b-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span></span> <span data-ttu-id="a853b-191">В нашем примере выбран **Email**, так как мы сопоставили утверждение идентификатора пользователя с атрибутом **userprincipalname** в разделе **Атрибуты пользователя** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a853b-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span></span> <span data-ttu-id="a853b-192">Так вы получаете уникальный адрес электронной почты пользователя, который отправляется в приложение SAP Business Object Cloud в каждом успешном ответе SAML.</span><span class="sxs-lookup"><span data-stu-id="a853b-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Выбор атрибута пользователя](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="a853b-194">Чтобы проверить учетную запись с помощью поставщика удостоверений (шаг 4), в поле **Login Credential (Email)** (Учетные данные входа (электронная почта)) введите адрес электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="a853b-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span></span> <span data-ttu-id="a853b-195">Выберите **Проверить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="a853b-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="a853b-196">Система добавит учетные данные входа в учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="a853b-196">The system adds sign-in credentials to the user account.</span></span>

    ![Ввод электронного адреса и нажатие кнопки "Проверить учетную запись"](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="a853b-198">Щелкните значок **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a853b-198">Select the **Save** icon.</span></span>

    ![Значок "Сохранить"](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="a853b-200">Краткую версию этих инструкций можно также прочесть на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a853b-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="a853b-201">После добавления этого приложения из раздела **Active Directory** > **Корпоративные приложения** выберите вкладку **Единый вход**. Откройте встроенную документацию в разделе **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a853b-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="a853b-202">Чтобы узнать больше, ознакомьтесь со [встроенной документацией по Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a853b-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a853b-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a853b-203">Create an Azure AD test user</span></span>
<span data-ttu-id="a853b-204">В этом разделе описано, как создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a853b-204">In this section, you create a test user named Britta Simon in the Azure portal.</span></span>

<span data-ttu-id="a853b-205">Чтобы создать тестового пользователя в Azure AD, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a853b-205">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="a853b-206">На портале Azure в меню слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a853b-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a853b-208">Чтобы открыть список пользователей, выберите **Пользователи и группы**, а затем — **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a853b-208">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a853b-210">Щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="a853b-210">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a853b-212">В диалоговом окне **Пользователь** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a853b-212">In the **User** dialog box, complete the following steps:</span></span>
 
    1. <span data-ttu-id="a853b-213">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a853b-213">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="a853b-214">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a853b-214">In the **User name** box, enter the email address of the user Britta Simon.</span></span>

    3. <span data-ttu-id="a853b-215">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a853b-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="a853b-216">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a853b-216">Select **Create**.</span></span>

        ![Диалоговое окно "Пользователь"](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Создание пользователя Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="a853b-219">Создание тестового пользователя SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="a853b-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="a853b-220">Пользователей Azure AD нужно подготовить в SAP Business Object Cloud, прежде чем они смогут входить в SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a853b-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span></span> <span data-ttu-id="a853b-221">В SAP Business Object Cloud подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="a853b-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="a853b-222">Чтобы подготовить учетную запись пользователя, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a853b-222">To provision a user account:</span></span>

1. <span data-ttu-id="a853b-223">Выполните вход на корпоративный сайт SAP Business Object Cloud с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a853b-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="a853b-224">Выберите **Меню** > **Безопасность** > **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a853b-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="a853b-226">На странице **Пользователи** щелкните **+**, чтобы добавить сведения о новом пользователе.</span><span class="sxs-lookup"><span data-stu-id="a853b-226">On the **Users** page, to add new user details, select **+**.</span></span> 

    ![Страница добавления пользователей](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="a853b-228">Затем сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a853b-228">Then, complete the following steps:</span></span>

    1. <span data-ttu-id="a853b-229">В поле **ИД пользователя** введите идентификатор пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a853b-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span></span>

    2. <span data-ttu-id="a853b-230">В текстовом поле **Имя** введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a853b-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span></span>

    3. <span data-ttu-id="a853b-231">В текстовом поле **Фамилия** введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a853b-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span></span>

    4. <span data-ttu-id="a853b-232">В текстовом поле **Отображаемое имя** введите полное имя пользователя, например **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a853b-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="a853b-233">В текстовом поле **Электронная почта** введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a853b-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="a853b-234">На странице **выбора ролей** выберите соответствующую роль для пользователя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a853b-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span></span>

      ![Выбрать роль](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="a853b-236">Щелкните значок **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a853b-236">Select the **Save** icon.</span></span>    


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a853b-237">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a853b-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="a853b-238">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure AD, предоставив доступ учетных записей пользователей к SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a853b-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span></span>

<span data-ttu-id="a853b-239">Чтобы назначить пользователя Britta Simon приложению SAP Business Object Cloud, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a853b-239">To assign Britta Simon to SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="a853b-240">На портале Azure откройте представление приложений и перейдите к представлению каталога.</span><span class="sxs-lookup"><span data-stu-id="a853b-240">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="a853b-241">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a853b-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a853b-243">В списке приложений выберите **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a853b-243">In the applications list, select **SAP Business Object Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="a853b-245">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a853b-245">In the left menu, select **Users and groups**.</span></span>

    ![Выбор параметра "Пользователи и группы"][202] 

4. <span data-ttu-id="a853b-247">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a853b-247">Select **Add**.</span></span> <span data-ttu-id="a853b-248">Затем на странице **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a853b-248">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Страница "Добавление назначения"][203]

5. <span data-ttu-id="a853b-250">На странице **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a853b-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="a853b-251">На странице **Пользователи и группы** щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a853b-251">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="a853b-252">На странице **Добавление назначения** выберите **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a853b-252">On the **Add Assignment** page, select **Assign**.</span></span>

![Назначение роли пользователя][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a853b-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a853b-254">Test single sign-on</span></span>

<span data-ttu-id="a853b-255">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a853b-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="a853b-256">Щелкнув плитку SAP Business Object Cloud на панели доступа, вы автоматически войдете в приложение SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a853b-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="a853b-257">Дополнительные сведения о панели доступа см. в статье [Что такое панель доступа?](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a853b-257">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a853b-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a853b-258">Additional resources</span></span>

* [<span data-ttu-id="a853b-259">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a853b-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a853b-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a853b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

