---
title: "Учебник. Интеграция Azure Active Directory с Cisco Spark | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="90280-103">Учебник. Интеграция Azure Active Directory с Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="90280-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="90280-104">В этом учебнике описано, как интегрировать Cisco Spark с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90280-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90280-105">Интеграция Azure AD с Cisco Spark обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="90280-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="90280-106">С помощью Azure AD вы можете контролировать доступ к Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="90280-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="90280-107">Вы можете включить автоматический вход пользователей в Cisco Spark (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90280-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90280-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="90280-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="90280-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90280-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90280-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90280-110">Prerequisites</span></span>

<span data-ttu-id="90280-111">Чтобы настроить интеграцию Azure AD с Cisco Spark, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="90280-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="90280-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="90280-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90280-113">подписка Cisco Spark с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="90280-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90280-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="90280-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90280-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="90280-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90280-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="90280-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90280-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90280-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90280-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="90280-118">Scenario description</span></span>
<span data-ttu-id="90280-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="90280-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90280-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="90280-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90280-121">Добавление Cisco Spark из коллекции</span><span class="sxs-lookup"><span data-stu-id="90280-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="90280-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="90280-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="90280-123">Добавление Cisco Spark из коллекции</span><span class="sxs-lookup"><span data-stu-id="90280-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="90280-124">Чтобы настроить интеграцию Cisco Spark с Azure AD, необходимо добавить Cisco Spark из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="90280-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="90280-125">**Чтобы добавить Cisco Spark из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="90280-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="90280-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="90280-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90280-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="90280-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="90280-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="90280-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="90280-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="90280-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="90280-133">В поле поиска введите **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="90280-133">In the search box, type **Cisco Spark**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="90280-135">На панели результатов выберите **Cisco Spark** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="90280-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90280-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="90280-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90280-138">В этом разделе описана настройка и проверка единого входа Azure AD в Cisco Spark с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90280-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="90280-139">Для работы единого входа Azure AD необходимо знать, какой пользователь в Cisco Spark соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90280-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="90280-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="90280-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="90280-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="90280-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="90280-142">Чтобы настроить и проверить единый вход Azure AD в Cisco Spark, потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="90280-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="90280-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="90280-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="90280-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90280-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90280-145">**[Создание тестового пользователя Cisco Spark](#creating-a-cisco-spark-test-user)** нужно для того, чтобы в Cisco Spark также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90280-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="90280-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90280-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90280-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90280-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90280-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="90280-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90280-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="90280-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="90280-150">**Чтобы настроить единый вход Azure AD в Cisco Spark, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="90280-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="90280-151">На портале Azure на странице интеграции с приложением **Cisco Spark** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="90280-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="90280-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="90280-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="90280-155">В разделе **Домены и URL-адреса приложения Cisco Spark** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="90280-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="90280-157">а.</span><span class="sxs-lookup"><span data-stu-id="90280-157">a.</span></span> <span data-ttu-id="90280-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в формате `https://web.ciscospark.com/#/signin`.</span><span class="sxs-lookup"><span data-stu-id="90280-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="90280-159">b.</span><span class="sxs-lookup"><span data-stu-id="90280-159">b.</span></span> <span data-ttu-id="90280-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="90280-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="90280-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="90280-161">This value is not real.</span></span> <span data-ttu-id="90280-162">Вместо него нужно указать фактический идентификатор.</span><span class="sxs-lookup"><span data-stu-id="90280-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="90280-163">Для получения этого значения обратитесь в [службу поддержки клиентов Cisco Spark](https://support.ciscospark.com/).</span><span class="sxs-lookup"><span data-stu-id="90280-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="90280-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="90280-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="90280-166">Приложение Cisco Spark ожидает, что утверждения SAML должны содержать определенные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="90280-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="90280-167">Настройте приведенные ниже атрибуты для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="90280-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="90280-168">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="90280-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="90280-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="90280-169">The following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="90280-171">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="90280-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="90280-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="90280-172">Attribute Name</span></span>  | <span data-ttu-id="90280-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="90280-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="90280-174">uid</span><span class="sxs-lookup"><span data-stu-id="90280-174">uid</span></span>    | <span data-ttu-id="90280-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="90280-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="90280-176">а.</span><span class="sxs-lookup"><span data-stu-id="90280-176">a.</span></span> <span data-ttu-id="90280-177">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="90280-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="90280-180">b.</span><span class="sxs-lookup"><span data-stu-id="90280-180">b.</span></span> <span data-ttu-id="90280-181">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="90280-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="90280-182">c.</span><span class="sxs-lookup"><span data-stu-id="90280-182">c.</span></span> <span data-ttu-id="90280-183">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="90280-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="90280-184">г)</span><span class="sxs-lookup"><span data-stu-id="90280-184">d.</span></span> <span data-ttu-id="90280-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="90280-185">Click **Ok**.</span></span>

7. <span data-ttu-id="90280-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="90280-186">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="90280-188">Войдите в [службу Cisco для управления совместной работой в облаке](https://admin.ciscospark.com/), указав учетные данные администратора с полными правами.</span><span class="sxs-lookup"><span data-stu-id="90280-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="90280-189">Выберите **Settings** (Параметры) и в разделе **Authentication** (Аутентификация) щелкните **Modify** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="90280-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="90280-191">Выберите **Integrate a 3rd-party identity provider. (Advanced)** (Интеграция стороннего поставщика удостоверений. (Дополнительно)) и перейдите к следующему экрану.</span><span class="sxs-lookup"><span data-stu-id="90280-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="90280-192">На странице **Import Idp Metadata** (Импорт метаданных IdP) либо перетащите файл метаданных Azure AD на страницу, либо воспользуйтесь обозревателем файлов, чтобы найти и передать файл метаданных Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90280-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="90280-193">Затем выберите **Require certificate signed by a certificate authority in Metadata (more secure)** (Требовать наличия в метаданных сертификата, подписанного центром сертификации) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="90280-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="90280-195">Выберите **Test SSO Connection** (Проверить подключение для единого входа) и, когда откроется новая вкладка браузера, пройдите аутентификацию Azure AD, выполнив вход.</span><span class="sxs-lookup"><span data-stu-id="90280-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="90280-196">Вернитесь к на вкладку браузера **Служба Cisco для управления совместной работой в облаке**.</span><span class="sxs-lookup"><span data-stu-id="90280-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="90280-197">Если проверка прошла успешно, выберите **This test was successful. Enable Single Sign-On option** (Этот тест прошел успешно. Включить единый вход) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="90280-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="90280-198">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="90280-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="90280-199">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="90280-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="90280-200">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="90280-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90280-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="90280-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="90280-202">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90280-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="90280-204">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="90280-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="90280-205">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="90280-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90280-207">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="90280-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90280-209">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="90280-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90280-211">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="90280-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90280-213">а.</span><span class="sxs-lookup"><span data-stu-id="90280-213">a.</span></span> <span data-ttu-id="90280-214">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90280-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90280-215">b.</span><span class="sxs-lookup"><span data-stu-id="90280-215">b.</span></span> <span data-ttu-id="90280-216">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90280-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90280-217">c.</span><span class="sxs-lookup"><span data-stu-id="90280-217">c.</span></span> <span data-ttu-id="90280-218">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="90280-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="90280-219">d.</span><span class="sxs-lookup"><span data-stu-id="90280-219">d.</span></span> <span data-ttu-id="90280-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="90280-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="90280-221">Создание тестового пользователя Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="90280-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="90280-222">В этом разделе описано, как создать пользователя Britta Simon в Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="90280-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="90280-223">В этом разделе описано, как создать пользователя Britta Simon в Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="90280-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="90280-224">Войдите в [службу Cisco для управления совместной работой в облаке](https://admin.ciscospark.com/), указав учетные данные администратора с полными правами.</span><span class="sxs-lookup"><span data-stu-id="90280-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="90280-225">Щелкните **Пользователи** и **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="90280-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="90280-227">В окне **Manage User** (Управление пользователем) выберите **Manually add or modify users** (Добавить или изменить пользователей вручную) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="90280-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="90280-228">Выберите **Names and Email address** (Имя, фамилия и электронный адрес).</span><span class="sxs-lookup"><span data-stu-id="90280-228">Select **Names and Email address**.</span></span> <span data-ttu-id="90280-229">Затем заполните текстовые поля следующим образом.</span><span class="sxs-lookup"><span data-stu-id="90280-229">Then, fill out the textbox as follows:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="90280-231">а.</span><span class="sxs-lookup"><span data-stu-id="90280-231">a.</span></span> <span data-ttu-id="90280-232">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="90280-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="90280-233">b.</span><span class="sxs-lookup"><span data-stu-id="90280-233">b.</span></span> <span data-ttu-id="90280-234">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="90280-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="90280-235">c.</span><span class="sxs-lookup"><span data-stu-id="90280-235">c.</span></span> <span data-ttu-id="90280-236">В текстовом поле **Email address** (Электронный адрес) введите **britta.simon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="90280-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="90280-237">Щелкните знак "плюс", чтобы добавить пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90280-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="90280-238">Затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="90280-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="90280-239">В окне **Add Services for Users** (Добавление служб для пользователей) нажмите кнопку **Save** (Сохранить), затем — кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="90280-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="90280-240">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="90280-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="90280-241">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="90280-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="90280-243">**Чтобы назначить пользователя Britta Simon в Cisco Spark, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="90280-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="90280-244">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="90280-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="90280-246">Из списка приложений выберите **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="90280-246">In the applications list, select **Cisco Spark**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="90280-248">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="90280-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="90280-250">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="90280-250">Click **Add** button.</span></span> <span data-ttu-id="90280-251">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="90280-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="90280-253">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="90280-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="90280-254">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="90280-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90280-255">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="90280-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90280-256">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="90280-256">Testing single sign-on</span></span>

<span data-ttu-id="90280-257">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="90280-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="90280-258">Щелкнув элемент "Cisco Spark" на панели доступа, вы автоматически войдете в приложение Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="90280-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90280-259">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="90280-259">Additional resources</span></span>

* [<span data-ttu-id="90280-260">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90280-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90280-261">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="90280-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

