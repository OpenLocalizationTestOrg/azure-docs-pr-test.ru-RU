---
title: "Руководство. Интеграция Azure Active Directory с eKincare | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="701b7-103">Руководство. Интеграция Azure Active Directory с eKincare</span><span class="sxs-lookup"><span data-stu-id="701b7-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="701b7-104">В этом руководстве описано, как интегрировать eKincare с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="701b7-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="701b7-105">Интеграция приложения eKincare с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="701b7-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="701b7-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению eKincare.</span><span class="sxs-lookup"><span data-stu-id="701b7-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="701b7-107">Вы можете включить автоматический вход пользователей в eKincare (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="701b7-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="701b7-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="701b7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="701b7-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="701b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="701b7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="701b7-110">Prerequisites</span></span>

<span data-ttu-id="701b7-111">Чтобы настроить интеграцию Azure AD с eKincare, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="701b7-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="701b7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="701b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="701b7-113">подписка eKincare с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="701b7-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="701b7-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="701b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="701b7-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="701b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="701b7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="701b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="701b7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="701b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="701b7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="701b7-118">Scenario description</span></span>
<span data-ttu-id="701b7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="701b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="701b7-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="701b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="701b7-121">Добавление eKincare из коллекции</span><span class="sxs-lookup"><span data-stu-id="701b7-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="701b7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="701b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="701b7-123">Добавление eKincare из коллекции</span><span class="sxs-lookup"><span data-stu-id="701b7-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="701b7-124">Чтобы настроить интеграцию приложения eKincare с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="701b7-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="701b7-125">**Добавление приложения eKincare из коллекции**</span><span class="sxs-lookup"><span data-stu-id="701b7-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="701b7-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="701b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="701b7-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="701b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="701b7-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="701b7-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="701b7-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="701b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="701b7-133">В поле поиска введите **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="701b7-133">In the search box, type **eKincare**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="701b7-135">На панели результатов выберите **eKincare** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="701b7-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="701b7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="701b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="701b7-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение eKincare с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="701b7-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="701b7-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в eKincare соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="701b7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="701b7-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в eKincare.</span><span class="sxs-lookup"><span data-stu-id="701b7-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="701b7-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в eKincare.</span><span class="sxs-lookup"><span data-stu-id="701b7-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="701b7-142">Чтобы настроить и проверить единый вход Azure AD в eKincare, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="701b7-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="701b7-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="701b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="701b7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="701b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="701b7-145">**[Создание тестового пользователя eKincare](#creating-a-ekincare-test-user)** требуется для создания в eKincare пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="701b7-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="701b7-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="701b7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="701b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="701b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="701b7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="701b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="701b7-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении eKincare.</span><span class="sxs-lookup"><span data-stu-id="701b7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="701b7-150">**Настройка единого входа Azure AD в eKincare**</span><span class="sxs-lookup"><span data-stu-id="701b7-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="701b7-151">На портале Azure на странице интеграции с приложением **eKincare** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="701b7-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="701b7-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="701b7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="701b7-155">В разделе **Домены и URL-адреса приложения eKincare** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="701b7-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="701b7-157">а.</span><span class="sxs-lookup"><span data-stu-id="701b7-157">a.</span></span> <span data-ttu-id="701b7-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="701b7-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="701b7-159">b.</span><span class="sxs-lookup"><span data-stu-id="701b7-159">b.</span></span> <span data-ttu-id="701b7-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<instancename>.ekincare.com/hul/saml`.</span><span class="sxs-lookup"><span data-stu-id="701b7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="701b7-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="701b7-161">These values are not real.</span></span> <span data-ttu-id="701b7-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="701b7-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="701b7-163">Чтобы получить эти значения, обратитесь в [службу поддержки eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="701b7-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="701b7-164">Приложение eKincare ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="701b7-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="701b7-165">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="701b7-165">Configure the following claims for this application.</span></span> <span data-ttu-id="701b7-166">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="701b7-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="701b7-167">На следующем снимке экрана приведен пример конфигурации.</span><span class="sxs-lookup"><span data-stu-id="701b7-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="701b7-168">Утверждение всегда будет носить имя **employeeid** и иметь значение, сопоставленное с параметром user.extensionattribute1, который содержит идентификатор сотрудника (employeeid) для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="701b7-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="701b7-169">Имена двух других утверждений, а именно</span><span class="sxs-lookup"><span data-stu-id="701b7-169">The other two claims' name i.e</span></span> <span data-ttu-id="701b7-170">**organizationid** и **organizationname** всегда неизменны, а их значения содержат сведения об организации, к которой относится пользователь.</span><span class="sxs-lookup"><span data-stu-id="701b7-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="701b7-172">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="701b7-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="701b7-173">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="701b7-173">Attribute Name</span></span> | <span data-ttu-id="701b7-174">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="701b7-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="701b7-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="701b7-175">employeeid</span></span> | <span data-ttu-id="701b7-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="701b7-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="701b7-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="701b7-177">organizationid</span></span> | <span data-ttu-id="701b7-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="701b7-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="701b7-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="701b7-179">organizationname</span></span> | <span data-ttu-id="701b7-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="701b7-180">*user.companyname*</span></span> |

    <span data-ttu-id="701b7-181">а.</span><span class="sxs-lookup"><span data-stu-id="701b7-181">a.</span></span> <span data-ttu-id="701b7-182">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="701b7-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="701b7-185">b.</span><span class="sxs-lookup"><span data-stu-id="701b7-185">b.</span></span> <span data-ttu-id="701b7-186">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="701b7-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="701b7-187">c.</span><span class="sxs-lookup"><span data-stu-id="701b7-187">c.</span></span> <span data-ttu-id="701b7-188">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="701b7-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="701b7-189">d.</span><span class="sxs-lookup"><span data-stu-id="701b7-189">d.</span></span> <span data-ttu-id="701b7-190">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="701b7-190">Click **Ok**</span></span>

6. <span data-ttu-id="701b7-191">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="701b7-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="701b7-193">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="701b7-193">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="701b7-195">Чтобы настроить единый вход на стороне **eKincare**, отправьте в [службу поддержки eKincare](mailto:tech@ekincare.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="701b7-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="701b7-196">Специалисты службы поддержки правильно настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="701b7-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="701b7-197">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="701b7-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="701b7-198">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="701b7-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="701b7-199">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="701b7-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="701b7-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="701b7-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="701b7-201">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="701b7-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="701b7-203">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="701b7-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="701b7-204">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="701b7-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="701b7-206">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="701b7-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="701b7-208">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="701b7-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="701b7-210">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="701b7-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="701b7-212">а.</span><span class="sxs-lookup"><span data-stu-id="701b7-212">a.</span></span> <span data-ttu-id="701b7-213">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="701b7-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="701b7-214">b.</span><span class="sxs-lookup"><span data-stu-id="701b7-214">b.</span></span> <span data-ttu-id="701b7-215">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="701b7-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="701b7-216">c.</span><span class="sxs-lookup"><span data-stu-id="701b7-216">c.</span></span> <span data-ttu-id="701b7-217">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="701b7-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="701b7-218">d.</span><span class="sxs-lookup"><span data-stu-id="701b7-218">d.</span></span> <span data-ttu-id="701b7-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="701b7-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="701b7-220">Создание тестового пользователя eKincare</span><span class="sxs-lookup"><span data-stu-id="701b7-220">Creating a eKincare test user</span></span>

<span data-ttu-id="701b7-221">Приложение поддерживает JIT-подготовку пользователей, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="701b7-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="701b7-222">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="701b7-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="701b7-223">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к eKincare.</span><span class="sxs-lookup"><span data-stu-id="701b7-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="701b7-225">**Назначение пользователя Britta Simon приложению eKincare**</span><span class="sxs-lookup"><span data-stu-id="701b7-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="701b7-226">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="701b7-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="701b7-228">В списке приложений выберите **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="701b7-228">In the applications list, select **eKincare**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="701b7-230">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="701b7-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="701b7-232">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="701b7-232">Click **Add** button.</span></span> <span data-ttu-id="701b7-233">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="701b7-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="701b7-235">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="701b7-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="701b7-236">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="701b7-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="701b7-237">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="701b7-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="701b7-238">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="701b7-238">Testing single sign-on</span></span>

<span data-ttu-id="701b7-239">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="701b7-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="701b7-240">Щелкнув плитку eKincare на панели доступа, вы автоматически войдете в приложение eKincare.</span><span class="sxs-lookup"><span data-stu-id="701b7-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="701b7-241">Дополнительные сведения о панели доступа см. в статье [Что такое панель доступа?](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="701b7-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="701b7-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="701b7-242">Additional resources</span></span>

* [<span data-ttu-id="701b7-243">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="701b7-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="701b7-244">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="701b7-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

