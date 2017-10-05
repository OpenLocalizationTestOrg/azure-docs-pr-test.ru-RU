---
title: "Руководство по интеграции Azure Active Directory с BenSelect | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="bf1bc-103">Руководство. Интеграция Azure Active Directory с BenSelect</span><span class="sxs-lookup"><span data-stu-id="bf1bc-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="bf1bc-104">В этом руководстве описано, как интегрировать BenSelect с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf1bc-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf1bc-105">Интеграция Azure AD с приложением BenSelect дает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bf1bc-106">С помощью Azure AD вы можете контролировать доступ к BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="bf1bc-107">Вы можете включить автоматический вход пользователей в BenSelect (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf1bc-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bf1bc-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf1bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf1bc-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bf1bc-110">Prerequisites</span></span>

<span data-ttu-id="bf1bc-111">Чтобы настроить интеграцию Azure AD с BenSelect, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="bf1bc-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="bf1bc-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bf1bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf1bc-113">подписка BenSelect с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf1bc-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf1bc-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="bf1bc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf1bc-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf1bc-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf1bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf1bc-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bf1bc-118">Scenario description</span></span>
<span data-ttu-id="bf1bc-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf1bc-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="bf1bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf1bc-121">Добавление BenSelect из коллекции.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="bf1bc-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf1bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="bf1bc-123">Добавление BenSelect из коллекции.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="bf1bc-124">Чтобы настроить интеграцию BenSelect с Azure AD, необходимо добавить BenSelect из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bf1bc-125">**Чтобы добавить BenSelect из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="bf1bc-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bf1bc-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bf1bc-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bf1bc-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bf1bc-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bf1bc-133">В поле поиска введите **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-133">In the search box, type **BenSelect**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="bf1bc-135">На панели результатов выберите **BenSelect** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf1bc-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf1bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf1bc-138">В этом разделе описана настройка и проверка единого входа Azure AD в BenSelect с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf1bc-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в BenSelect соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="bf1bc-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="bf1bc-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bf1bc-142">Чтобы настроить и проверить единый вход Azure AD в BenSelect, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bf1bc-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bf1bc-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf1bc-145">**[Создание тестового пользователя BenSelect](#creating-a-benselect-test-user)** нужно для того, чтобы в BenSelect также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf1bc-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf1bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf1bc-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf1bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf1bc-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="bf1bc-150">**Чтобы настроить единый вход Azure AD в BenSelect, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="bf1bc-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="bf1bc-151">На портале Azure на странице интеграции с приложением **BenSelect** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bf1bc-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="bf1bc-155">В разделе **Домены и URL-адреса приложения BenSelect** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="bf1bc-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bf1bc-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-158">This value is not real.</span></span> <span data-ttu-id="bf1bc-159">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="bf1bc-160">Чтобы получить это значение, обратитесь к [группе поддержки BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="bf1bc-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="bf1bc-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (необработанный)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="bf1bc-163">Приложение BenSelect ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="bf1bc-164">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-164">Configure the following claims for this application.</span></span> <span data-ttu-id="bf1bc-165">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="bf1bc-166">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-166">The following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="bf1bc-168">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="bf1bc-169">а.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-169">a.</span></span> <span data-ttu-id="bf1bc-170">Из раскрывающегося списка **Идентификатор пользователя** выберите **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="bf1bc-171">b.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-171">b.</span></span> <span data-ttu-id="bf1bc-172">Из раскрывающегося списка **Электронная почта** выберите **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="bf1bc-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bf1bc-173">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bf1bc-175">В разделе **Конфигурация BenSelect** щелкните **Настроить BenSelect**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bf1bc-176">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="bf1bc-178">Чтобы настроить единый вход на стороне **BenSelect**, нужно отправить скачанный **сертификат (необработанный)**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="bf1bc-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="bf1bc-179">Необходимо отметить, что для этой интеграции требуется алгоритм SHA256 (SHA1 не поддерживается), чтобы настроить единый вход на соответствующем сервере, например app2101 и т. п.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="bf1bc-180">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bf1bc-181">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bf1bc-182">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="bf1bc-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf1bc-183">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf1bc-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf1bc-184">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bf1bc-186">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bf1bc-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bf1bc-187">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf1bc-189">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf1bc-191">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf1bc-193">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf1bc-195">а.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-195">a.</span></span> <span data-ttu-id="bf1bc-196">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf1bc-197">b.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-197">b.</span></span> <span data-ttu-id="bf1bc-198">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf1bc-199">c.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-199">c.</span></span> <span data-ttu-id="bf1bc-200">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bf1bc-201">d.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-201">d.</span></span> <span data-ttu-id="bf1bc-202">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="bf1bc-203">Создание тестового пользователя BenSelect</span><span class="sxs-lookup"><span data-stu-id="bf1bc-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="bf1bc-204">Цель этого раздела — создать пользователя с именем Britta Simon в BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="bf1bc-205">Обратитесь к [группе поддержки BenSelect](mailto:support@selerix.com), чтобы добавить пользователей в учетную запись BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bf1bc-206">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf1bc-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bf1bc-207">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bf1bc-209">**Чтобы назначить пользователя Britta Simon в BenSelect, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="bf1bc-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="bf1bc-210">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bf1bc-212">В списке приложений выберите **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-212">In the applications list, select **BenSelect**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="bf1bc-214">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bf1bc-216">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-216">Click **Add** button.</span></span> <span data-ttu-id="bf1bc-217">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bf1bc-219">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bf1bc-220">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf1bc-221">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf1bc-222">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bf1bc-222">Testing single sign-on</span></span>

<span data-ttu-id="bf1bc-223">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="bf1bc-224">Щелкнув элемент BenSelect на панели доступа, вы автоматически войдете в приложение BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf1bc-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf1bc-225">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bf1bc-225">Additional resources</span></span>

* [<span data-ttu-id="bf1bc-226">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf1bc-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf1bc-227">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf1bc-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

