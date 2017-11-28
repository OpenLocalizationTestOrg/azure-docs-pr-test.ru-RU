---
title: "Учебник. Интеграция Azure Active Directory с IBM Kenexa Survey Enterprise | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в IBM Kenexa Survey Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c276c23288292a1c54dd9d57177d5072b90c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="0ee04-103">Руководство по интеграции Azure Active Directory с IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="0ee04-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="0ee04-104">В этом руководстве описано, как интегрировать IBM Kenexa Survey Enterprise с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ee04-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ee04-105">Интеграция IBM Kenexa Survey Enterprise с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0ee04-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0ee04-106">С помощью Azure AD можно контролировать, кто будет иметь доступ к IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0ee04-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="0ee04-107">Вы можете включить автоматический вход пользователей в IBM Kenexa Survey Enterprise (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ee04-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0ee04-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee04-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="0ee04-109">Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="0ee04-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ee04-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ee04-110">Prerequisites</span></span>

<span data-ttu-id="0ee04-111">Чтобы настроить интеграцию Azure AD с IBM Kenexa Survey Enterprise, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="0ee04-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="0ee04-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0ee04-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ee04-113">подписка на IBM Kenexa Survey Enterprise с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0ee04-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ee04-114">Мы не рекомендуем использовать рабочую среду для тестирования действий, выполняемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="0ee04-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="0ee04-115">При проверке действий в этом руководстве соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="0ee04-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="0ee04-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0ee04-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ee04-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ee04-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ee04-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0ee04-118">Scenario description</span></span>
<span data-ttu-id="0ee04-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0ee04-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="0ee04-120">Сценарий, описанный в этом руководстве, состоит из двух основных стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="0ee04-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="0ee04-121">Добавление IBM Kenexa Survey Enterprise из коллекции.</span><span class="sxs-lookup"><span data-stu-id="0ee04-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="0ee04-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ee04-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="0ee04-123">Добавление IBM Kenexa Survey Enterprise из коллекции</span><span class="sxs-lookup"><span data-stu-id="0ee04-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="0ee04-124">Чтобы настроить интеграцию IBM Kenexa Survey Enterprise в Azure AD, следует добавить IBM Kenexa Survey Enterprise из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0ee04-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0ee04-125">Чтобы добавить IBM Kenexa Survey Enterprise из коллекции, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0ee04-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="0ee04-126">На [портале Azure](https://portal.azure.com) в левой области нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="0ee04-128">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="0ee04-130">Чтобы добавить приложение, нажмите кнопку **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-130">To add an application, click the **New application** button.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="0ee04-132">В поле поиска введите **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="0ee04-134">Из списка результатов выберите **IBM Kenexa Survey Enterprise**, а затем нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="0ee04-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![IBM Kenexa Survey Enterprise в списке результатов](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0ee04-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ee04-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0ee04-137">В этом разделе описана настройка и проверка единого входа Azure AD в IBM Kenexa Survey Enterprise с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ee04-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0ee04-138">Чтобы единый вход работал, в Azure AD необходимо указать, какой пользователь в IBM Kenexa Survey Enterprise соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ee04-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="0ee04-139">Иными словами, в Azure AD необходимо установить связь между пользователем Azure AD и соответствующим пользователем в IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0ee04-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="0ee04-140">Чтобы установить эту связь, назначьте **имя пользователя** в IBM Kenexa Survey Enterprise в качестве значения **имени пользователя** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ee04-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="0ee04-141">Чтобы настроить и проверить единый вход Azure AD в IBM Kenexa Survey Enterprise, выполните действия в следующих двух стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="0ee04-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="0ee04-142">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ee04-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="0ee04-143">В этом разделе вы включите единый вход Azure AD на портале Azure и настроите единый вход в приложении IBM Kenexa Survey Enterprise. Для этого выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="0ee04-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="0ee04-144">На портале Azure на странице интеграции с приложением **IBM Kenexa Survey Enterprise** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка для настройки единого входа для IBM Kenexa Survey Enterprise][4]

2. <span data-ttu-id="0ee04-146">В диалоговом окне **Единый вход** из списка **Режим** выберите значение **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="0ee04-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="0ee04-148">В разделе **Домены и URL-адреса приложения IBM Kenexa Survey Enterprise** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0ee04-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="0ee04-150">а.</span><span class="sxs-lookup"><span data-stu-id="0ee04-150">a.</span></span> <span data-ttu-id="0ee04-151">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://surveys.kenexa.com/<companycode>`.</span><span class="sxs-lookup"><span data-stu-id="0ee04-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="0ee04-152">b.</span><span class="sxs-lookup"><span data-stu-id="0ee04-152">b.</span></span> <span data-ttu-id="0ee04-153">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`.</span><span class="sxs-lookup"><span data-stu-id="0ee04-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ee04-154">Приведенные выше значения используются только для примера.</span><span class="sxs-lookup"><span data-stu-id="0ee04-154">The preceding values are not real.</span></span> <span data-ttu-id="0ee04-155">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="0ee04-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="0ee04-156">Чтобы получить фактические значения, обратитесь к [группе поддержки IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="0ee04-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="0ee04-157">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)** и сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0ee04-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![Ссылки для скачивания сертификата в кодировке Base64](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="0ee04-159">Приложение IBM Kenexa Survey Enterprise ожидает утверждения SAML (язык разметки заявлений системы безопасности) в определенном формате, поэтому необходимо добавить настраиваемые сопоставления атрибутов в конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="0ee04-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="0ee04-160">Полученное в ответ значение утверждения идентификатора пользователя должно совпадать с идентификатором единого входа, настроенным в системе Kenexa.</span><span class="sxs-lookup"><span data-stu-id="0ee04-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="0ee04-161">Чтобы сопоставить соответствующий идентификатор пользователя в организации для применения единого входа на основе протокола IDP, обратитесь к [группе поддержки IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="0ee04-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="0ee04-162">По умолчанию Azure AD в качестве идентификатора пользователя задает значение имени участника-пользователя (UPN).</span><span class="sxs-lookup"><span data-stu-id="0ee04-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="0ee04-163">Это значение можно изменить на вкладке **Атрибут**, как показано на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="0ee04-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="0ee04-164">Интеграция заработает только после правильной настройки сопоставления.</span><span class="sxs-lookup"><span data-stu-id="0ee04-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![Диалоговое окно "Атрибуты пользователя"](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png)   

5. <span data-ttu-id="0ee04-166">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-166">Click **Save**.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ee04-168">Чтобы открыть окно **Настройка единого входа**, в разделе **Конфигурация IBM Kenexa Survey Enterprise** щелкните **Настроить IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![Ссылка "Настройка IBM Kenexa Survey Enterprise"](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="0ee04-170">Скопируйте значения **URL-адрес выхода**, **SAML Entity ID** (Идентификатор сущности SAML) и **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML) из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

8. <span data-ttu-id="0ee04-171">В окне **Настройка единого входа** из раздела **Краткий справочник** скопируйте значения **URL-адрес выхода**, **SAML Entity ID** (Идентификатор сущности SAML) и **SAML single sign-on Service URL** (URL-адрес службы единого входа SAML).</span><span class="sxs-lookup"><span data-stu-id="0ee04-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="0ee04-172">Чтобы настроить единый вход на стороне **IBM Kenexa Survey Enterprise**, отправьте скачанный **сертификат в кодировке Base64**, **URL-адрес выхода**, **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** [группе поддержки IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="0ee04-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="0ee04-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="0ee04-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="0ee04-174">После добавления приложения из раздела **Active Directory** > **Корпоративные приложения** просто выберите вкладку **Единый вход** и ознакомьтесь со встроенной документацией, воспользовавшись разделом **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0ee04-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="0ee04-175">Чтобы узнать больше, ознакомьтесь со [встроенной документацией Azure AD](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0ee04-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0ee04-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ee04-176">Create an Azure AD test user</span></span>
<span data-ttu-id="0ee04-177">В этом разделе вы создадите на портале Azure тестового пользователя Britta Simon, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0ee04-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Создание тестового пользователя Azure AD][100]

1. <span data-ttu-id="0ee04-179">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ee04-181">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ee04-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ee04-185">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="0ee04-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ee04-187">а.</span><span class="sxs-lookup"><span data-stu-id="0ee04-187">a.</span></span> <span data-ttu-id="0ee04-188">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ee04-189">b.</span><span class="sxs-lookup"><span data-stu-id="0ee04-189">b.</span></span> <span data-ttu-id="0ee04-190">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ee04-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0ee04-191">c.</span><span class="sxs-lookup"><span data-stu-id="0ee04-191">c.</span></span> <span data-ttu-id="0ee04-192">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0ee04-193">г)</span><span class="sxs-lookup"><span data-stu-id="0ee04-193">d.</span></span> <span data-ttu-id="0ee04-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="0ee04-195">Создание тестового пользователя IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="0ee04-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="0ee04-196">В этом разделе описано, как создать пользователя Britta Simon в приложении IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0ee04-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="0ee04-197">Чтобы создать пользователей в системе IBM Kenexa Survey Enterprise и сопоставить с ними идентификатор единого входа, вы можете обратиться к [группе поддержки IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="0ee04-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="0ee04-198">Это значение идентификатора единого входа необходимо также сопоставить со значением идентификатора пользователя из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ee04-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="0ee04-199">Эти заданные по умолчанию параметры можно изменить на вкладке **Атрибут**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0ee04-200">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ee04-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="0ee04-201">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0ee04-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="0ee04-203">Чтобы назначить пользователя Britta Simon в IBM Kenexa Survey Enterprise, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0ee04-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="0ee04-204">На портале Azure откройте представление **Приложения**, перейдите к представлению **Каталог**, выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Ссылки "Корпоративные приложения" и "Все приложения"][201] 

2. <span data-ttu-id="0ee04-206">Из списка **Приложения** выберите **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![Ссылка на IBM Kenexa Survey Enterprise в списке "Приложения"](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="0ee04-208">В области слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-208">In the left pane, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="0ee04-210">Нажмите кнопку **Добавить**, затем в области **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="0ee04-212">В диалоговом окне **Пользователи и группы** в списке **Пользователи** выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="0ee04-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="0ee04-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0ee04-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0ee04-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0ee04-215">Test single sign-on</span></span>

<span data-ttu-id="0ee04-216">В этом разделе вы с помощью панели доступа выполните проверку конфигурации единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ee04-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="0ee04-217">Щелкнув элемент **IBM Kenexa Survey Enterprise** на панели доступа, вы автоматически войдете в приложение IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0ee04-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ee04-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0ee04-218">Additional resources</span></span>

* [<span data-ttu-id="0ee04-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ee04-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ee04-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ee04-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
