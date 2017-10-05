---
title: "Руководство по интеграции Azure Active Directory с BetterWorks | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и BetterWorks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="0172d-103">Учебник. Интеграция Azure Active Directory с BetterWorks</span><span class="sxs-lookup"><span data-stu-id="0172d-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="0172d-104">В этом руководстве описано, как интегрировать BetterWorks с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0172d-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0172d-105">Интеграция Azure AD с BetterWorks обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="0172d-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0172d-106">С помощью Azure AD вы можете контролировать доступ к BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="0172d-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="0172d-107">Вы можете включить автоматический вход пользователей в BetterWorks (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0172d-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0172d-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0172d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0172d-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0172d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0172d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0172d-110">Prerequisites</span></span>

<span data-ttu-id="0172d-111">Чтобы настроить интеграцию Azure AD с BetterWorks, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="0172d-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="0172d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0172d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0172d-113">подписка BetterWorks с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0172d-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0172d-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0172d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0172d-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="0172d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0172d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0172d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0172d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0172d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0172d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0172d-118">Scenario description</span></span>
<span data-ttu-id="0172d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0172d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0172d-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="0172d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0172d-121">Добавление BetterWorks из коллекции</span><span class="sxs-lookup"><span data-stu-id="0172d-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="0172d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0172d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="0172d-123">Добавление BetterWorks из коллекции</span><span class="sxs-lookup"><span data-stu-id="0172d-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="0172d-124">Чтобы настроить интеграцию BetterWorks с Azure AD, необходимо добавить BetterWorks из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0172d-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0172d-125">**Чтобы добавить BetterWorks из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0172d-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0172d-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0172d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0172d-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="0172d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0172d-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0172d-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0172d-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="0172d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0172d-133">В поле поиска введите **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="0172d-133">In the search box, type **BetterWorks**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="0172d-135">На панели результатов выберите **BetterWorks** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="0172d-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0172d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0172d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0172d-138">В этом разделе описана настройка и проверка единого входа Azure AD в BetterWorks с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0172d-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0172d-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в BetterWorks соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0172d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="0172d-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="0172d-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="0172d-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="0172d-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0172d-142">Чтобы настроить и проверить единый вход Azure AD в BetterWorks, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="0172d-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0172d-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="0172d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0172d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0172d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0172d-145">**[Создание тестового пользователя BetterWorks](#creating-a-betterworks-test-user)** нужно для того, чтобы в BetterWorks также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0172d-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0172d-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0172d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0172d-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0172d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0172d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0172d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0172d-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="0172d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="0172d-150">**Чтобы настроить единый вход Azure AD в BetterWorks, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0172d-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="0172d-151">На портале Azure на странице интеграции с приложением **BetterWorks** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0172d-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0172d-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="0172d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="0172d-155">Если вы хотите настроить приложение в **режиме, инициируемом IdP**, то в разделе **Домены и URL-адреса приложения BetterWorks** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0172d-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="0172d-157">а.</span><span class="sxs-lookup"><span data-stu-id="0172d-157">a.</span></span> <span data-ttu-id="0172d-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="0172d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="0172d-159">b.</span><span class="sxs-lookup"><span data-stu-id="0172d-159">b.</span></span> <span data-ttu-id="0172d-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://app.betterworks.com/saml2/acs/`.</span><span class="sxs-lookup"><span data-stu-id="0172d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="0172d-161">Если вы хотите настроить приложение в **режиме, инициируемом поставщиком услуг**, то в разделе **Домены и URL-адреса приложения BetterWorks** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0172d-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="0172d-163">а.</span><span class="sxs-lookup"><span data-stu-id="0172d-163">a.</span></span> <span data-ttu-id="0172d-164">Установите флажок **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="0172d-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="0172d-165">b.</span><span class="sxs-lookup"><span data-stu-id="0172d-165">b.</span></span> <span data-ttu-id="0172d-166">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://app.betterworks.com`.</span><span class="sxs-lookup"><span data-stu-id="0172d-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0172d-167">Значения, указанные выше, приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0172d-167">These are not real values.</span></span> <span data-ttu-id="0172d-168">Вместо них необходимо указать фактические значения URL-адреса ответа, идентификатора и URL-адреса для входа.</span><span class="sxs-lookup"><span data-stu-id="0172d-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="0172d-169">Чтобы получить эти значения, обратитесь к [группе поддержки BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="0172d-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="0172d-170">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0172d-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="0172d-172">Приложение BetterWorks ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="0172d-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0172d-173">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="0172d-173">Configure the following claims for this application.</span></span> <span data-ttu-id="0172d-174">Управлять значениями этих атрибутов можно на вкладке **Attribute** (Атрибут) приложения.</span><span class="sxs-lookup"><span data-stu-id="0172d-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="0172d-175">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="0172d-175">The following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="0172d-177">В диалоговом окне **Атрибуты токена SAML** для каждой строки в таблице ниже выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0172d-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="0172d-178">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="0172d-178">Attribute Name</span></span> | <span data-ttu-id="0172d-179">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="0172d-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="0172d-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="0172d-180">saml_token</span></span>     | <span data-ttu-id="0172d-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="0172d-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="0172d-182">а.</span><span class="sxs-lookup"><span data-stu-id="0172d-182">a.</span></span> <span data-ttu-id="0172d-183">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="0172d-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="0172d-186">b.</span><span class="sxs-lookup"><span data-stu-id="0172d-186">b.</span></span> <span data-ttu-id="0172d-187">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="0172d-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="0172d-188">c.</span><span class="sxs-lookup"><span data-stu-id="0172d-188">c.</span></span> <span data-ttu-id="0172d-189">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="0172d-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="0172d-190">г)</span><span class="sxs-lookup"><span data-stu-id="0172d-190">d.</span></span> <span data-ttu-id="0172d-191">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0172d-191">Click **Ok**.</span></span>

7. <span data-ttu-id="0172d-192">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0172d-192">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0172d-194">Чтобы настроить единый вход на стороне **BetterWorks**, отправьте скачанный **XML-файл метаданных** [группе поддержки BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="0172d-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="0172d-195">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="0172d-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0172d-196">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0172d-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0172d-197">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0172d-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0172d-198">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0172d-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="0172d-199">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0172d-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0172d-201">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0172d-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0172d-202">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0172d-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0172d-204">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0172d-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0172d-206">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0172d-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0172d-208">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0172d-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0172d-210">а.</span><span class="sxs-lookup"><span data-stu-id="0172d-210">a.</span></span> <span data-ttu-id="0172d-211">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0172d-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0172d-212">b.</span><span class="sxs-lookup"><span data-stu-id="0172d-212">b.</span></span> <span data-ttu-id="0172d-213">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0172d-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0172d-214">c.</span><span class="sxs-lookup"><span data-stu-id="0172d-214">c.</span></span> <span data-ttu-id="0172d-215">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="0172d-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0172d-216">d.</span><span class="sxs-lookup"><span data-stu-id="0172d-216">d.</span></span> <span data-ttu-id="0172d-217">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0172d-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="0172d-218">Создание тестового пользователя BetterWorks</span><span class="sxs-lookup"><span data-stu-id="0172d-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="0172d-219">В этом разделе описано, как создать пользователя Britta Simon в приложении BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="0172d-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="0172d-220">Обратитесь к [группе поддержки BetterWorks](mailto:support@betterworks.com), чтобы добавить пользователей на платформу BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="0172d-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0172d-221">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0172d-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0172d-222">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="0172d-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0172d-224">**Чтобы назначить пользователя Britta Simon в BetterWorks, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0172d-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="0172d-225">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0172d-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0172d-227">В списке приложений выберите **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="0172d-227">In the applications list, select **BetterWorks**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="0172d-229">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0172d-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0172d-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0172d-231">Click **Add** button.</span></span> <span data-ttu-id="0172d-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0172d-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0172d-234">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0172d-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0172d-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0172d-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0172d-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0172d-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0172d-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0172d-237">Testing single sign-on</span></span>

<span data-ttu-id="0172d-238">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="0172d-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0172d-239">Щелкнув элемент BetterWorks на панели доступа, вы автоматически войдете в приложение BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="0172d-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0172d-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0172d-240">Additional resources</span></span>

* [<span data-ttu-id="0172d-241">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0172d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0172d-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0172d-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

