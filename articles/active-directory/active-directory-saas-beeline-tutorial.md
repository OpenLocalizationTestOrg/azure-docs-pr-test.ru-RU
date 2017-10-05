---
title: "Руководство по интеграции Azure Active Directory с BeeLine | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 93acbd90bbe5f0a40bf3f56edb766a0fdd30f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="163f9-103">Руководство по интеграции Azure Active Directory с Beeline</span><span class="sxs-lookup"><span data-stu-id="163f9-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="163f9-104">В этом руководстве описано, как интегрировать BeeLine с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="163f9-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="163f9-105">Интеграция BeeLine с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="163f9-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="163f9-106">С помощью Azure AD вы можете контролировать доступ к BeeLine.</span><span class="sxs-lookup"><span data-stu-id="163f9-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="163f9-107">Вы можете включить автоматический вход пользователей в BeeLine (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="163f9-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="163f9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="163f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="163f9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="163f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="163f9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="163f9-110">Prerequisites</span></span>

<span data-ttu-id="163f9-111">Чтобы настроить интеграцию Azure AD с BeeLine, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="163f9-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="163f9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="163f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="163f9-113">подписка BeeLine с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="163f9-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="163f9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="163f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="163f9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="163f9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="163f9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="163f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="163f9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="163f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="163f9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="163f9-118">Scenario description</span></span>
<span data-ttu-id="163f9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="163f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="163f9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="163f9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="163f9-121">Добавление BeeLine из коллекции.</span><span class="sxs-lookup"><span data-stu-id="163f9-121">Adding BeeLine from the gallery</span></span>
2. <span data-ttu-id="163f9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="163f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="163f9-123">Добавление BeeLine из коллекции</span><span class="sxs-lookup"><span data-stu-id="163f9-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="163f9-124">Чтобы настроить интеграцию приложения BeeLine с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="163f9-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="163f9-125">**Чтобы добавить BeeLine из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="163f9-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="163f9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="163f9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="163f9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="163f9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="163f9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="163f9-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="163f9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="163f9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="163f9-133">В поле поиска введите **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="163f9-133">In the search box, type **BeeLine**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="163f9-135">На панели результатов выберите **BeeLine** и щелкните **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="163f9-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="163f9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="163f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="163f9-138">В этом разделе описана настройка и проверка единого входа Azure AD в BeeLine с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="163f9-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="163f9-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в BeeLine соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="163f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="163f9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в BeeLine.</span><span class="sxs-lookup"><span data-stu-id="163f9-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="163f9-141">Чтобы установить эту связь, присвойте **имя пользователя** в Azure AD в качестве значения **Имя пользователя** в BeeLine.</span><span class="sxs-lookup"><span data-stu-id="163f9-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="163f9-142">Чтобы настроить и проверить единый вход Azure AD в BeeLine, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="163f9-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="163f9-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="163f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="163f9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="163f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="163f9-145">**[Создание тестового пользователя BeeLine](#creating-a-beeline-test-user)** требуется для создания пользователя Britta Simon в BeeLine, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="163f9-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="163f9-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="163f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="163f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="163f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="163f9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="163f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="163f9-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении BeeLine.</span><span class="sxs-lookup"><span data-stu-id="163f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="163f9-150">**Чтобы настроить единый вход Azure AD в BeeLine, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="163f9-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="163f9-151">На портале Azure на странице интеграции с приложением **BeeLine** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="163f9-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="163f9-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="163f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="163f9-155">В разделе **Домены и URL-адреса приложения BeeLine** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="163f9-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="163f9-157">а.</span><span class="sxs-lookup"><span data-stu-id="163f9-157">a.</span></span> <span data-ttu-id="163f9-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="163f9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="163f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="163f9-159">b.</span></span> <span data-ttu-id="163f9-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="163f9-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="163f9-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="163f9-161">These values are not real.</span></span> <span data-ttu-id="163f9-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="163f9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="163f9-163">Чтобы получить эти значения, обратитесь в [службу поддержки BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="163f9-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
4. <span data-ttu-id="163f9-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="163f9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="163f9-166">Приложение Beeline ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="163f9-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="163f9-167">Обратитесь в [службу поддержки BeeLine](https://www.beeline.com/contact-us/), чтобы определить правильный идентификатор пользователя, который будет сопоставляться в приложении.</span><span class="sxs-lookup"><span data-stu-id="163f9-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="163f9-168">Необходимо выполнить рекомендации от [службы поддержки BeeLine](https://www.beeline.com/contact-us/), касающиеся атрибута, который она хочет использовать для данного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="163f9-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="163f9-169">Управлять значением этого атрибута можно на вкладке **Атрибуты пользователя** приложения.</span><span class="sxs-lookup"><span data-stu-id="163f9-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="163f9-170">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="163f9-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="163f9-171">Утверждение **Идентификатор пользователя** было сопоставлено с атрибутом **userprincipalname**. Таким образом был получен уникальный идентификатор пользователя, который будет отправляться в приложение Beeline в каждом успешном ответе SAML.</span><span class="sxs-lookup"><span data-stu-id="163f9-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="163f9-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="163f9-173">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="163f9-175">В разделе **Настройка BeeLine** щелкните **Настроить BeeLine**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="163f9-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="163f9-176">Скопируйте **URL-адрес выхода** и **идентификатор сущности SAM** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="163f9-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="163f9-178">Для настройки единого входа на стороне **BeeLine** необходимо отправить скачанный **XML-файл метаданных** и **идентификатор сущности SAML**, **URL-адрес выхода** в [службу поддержки BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="163f9-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="163f9-179">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="163f9-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="163f9-180">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="163f9-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="163f9-181">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="163f9-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="163f9-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="163f9-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="163f9-183">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="163f9-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="163f9-185">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="163f9-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="163f9-186">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="163f9-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="163f9-188">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="163f9-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="163f9-190">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="163f9-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="163f9-192">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="163f9-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="163f9-194">а.</span><span class="sxs-lookup"><span data-stu-id="163f9-194">a.</span></span> <span data-ttu-id="163f9-195">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="163f9-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="163f9-196">b.</span><span class="sxs-lookup"><span data-stu-id="163f9-196">b.</span></span> <span data-ttu-id="163f9-197">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="163f9-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="163f9-198">c.</span><span class="sxs-lookup"><span data-stu-id="163f9-198">c.</span></span> <span data-ttu-id="163f9-199">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="163f9-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="163f9-200">d.</span><span class="sxs-lookup"><span data-stu-id="163f9-200">d.</span></span> <span data-ttu-id="163f9-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="163f9-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="163f9-202">Создание тестового пользователя BeeLine</span><span class="sxs-lookup"><span data-stu-id="163f9-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="163f9-203">В этом разделе описано, как создать пользователя Britta Simon в приложении Beeline.</span><span class="sxs-lookup"><span data-stu-id="163f9-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="163f9-204">Перед выполнением единого входа все пользователи должны быть подготовлены в приложении BeeLine.</span><span class="sxs-lookup"><span data-stu-id="163f9-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="163f9-205">Для этого обратитесь в [службу поддержки BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="163f9-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="163f9-206">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="163f9-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="163f9-207">В этом разделе описано, как предоставить пользователю Britta Simon доступ к BeeLine, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="163f9-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="163f9-209">**Чтобы назначить пользователя Britta Simon в BeeLine, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="163f9-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="163f9-210">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="163f9-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="163f9-212">В списке приложений выберите **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="163f9-212">In the applications list, select **BeeLine**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="163f9-214">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="163f9-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="163f9-216">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="163f9-216">Click **Add** button.</span></span> <span data-ttu-id="163f9-217">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="163f9-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="163f9-219">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="163f9-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="163f9-220">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="163f9-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="163f9-221">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="163f9-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="163f9-222">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="163f9-222">Testing single sign-on</span></span>

<span data-ttu-id="163f9-223">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="163f9-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="163f9-224">Щелкнув элемент Beeline на панели доступа, вы автоматически войдете в приложение Beeline.</span><span class="sxs-lookup"><span data-stu-id="163f9-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="163f9-225">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="163f9-225">Additional resources</span></span>

* [<span data-ttu-id="163f9-226">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="163f9-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="163f9-227">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="163f9-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

