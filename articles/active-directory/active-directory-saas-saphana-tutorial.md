---
title: "Руководство по интеграции Azure Active Directory с SAP HANA | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: a7e73f6ee763d1005ad85935cf2d8f6b24ecf116
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="1b309-103">Руководство по интеграции Azure Active Directory с SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1b309-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="1b309-104">В этом руководстве описано, как интегрировать SAP HANA с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b309-104">In this tutorial, you learn how to integrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b309-105">Интеграция SAP HANA с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1b309-105">Integrating SAP HANA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1b309-106">С помощью Azure AD вы можете контролировать доступ к SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1b309-106">You can control in Azure AD who has access to SAP HANA</span></span>
- <span data-ttu-id="1b309-107">Вы можете включить автоматический вход пользователей в SAP HANA (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b309-107">You can enable your users to automatically get signed-on to SAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b309-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1b309-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1b309-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b309-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b309-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1b309-110">Prerequisites</span></span>

<span data-ttu-id="1b309-111">Чтобы настроить интеграцию Azure AD с SAP HANA, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="1b309-111">To configure Azure AD integration with SAP HANA, you need the following items:</span></span>

- <span data-ttu-id="1b309-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1b309-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b309-113">подписка SAP HANA с поддержкой единого входа;</span><span class="sxs-lookup"><span data-stu-id="1b309-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="1b309-114">экземпляр HANA, выполняемый на любой общедоступной IaaS, локально, на виртуальной машине Azure или в решении "Крупные экземпляры SAP в Azure";</span><span class="sxs-lookup"><span data-stu-id="1b309-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="1b309-115">веб-интерфейс администрирования XSA, а также среда HANA Studio, установленная на экземпляре HANA.</span><span class="sxs-lookup"><span data-stu-id="1b309-115">The XSA Administration Web Interface as well as HANA Studio installed on the HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="1b309-116">Мы не рекомендуем использовать рабочую среду SAP HANA для проверки действий в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="1b309-116">To test the steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="1b309-117">Сначала протестируйте интеграцию в среде разработки или промежуточной среде приложения, а затем используйте ее в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1b309-117">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="1b309-118">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="1b309-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b309-119">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1b309-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b309-120">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b309-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b309-121">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1b309-121">Scenario description</span></span>
<span data-ttu-id="1b309-122">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1b309-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b309-123">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="1b309-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b309-124">Добавление SAP HANA из коллекции.</span><span class="sxs-lookup"><span data-stu-id="1b309-124">Adding SAP HANA from the gallery</span></span>
2. <span data-ttu-id="1b309-125">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b309-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-the-gallery"></a><span data-ttu-id="1b309-126">Добавление SAP HANA из коллекции</span><span class="sxs-lookup"><span data-stu-id="1b309-126">Adding SAP HANA from the gallery</span></span>
<span data-ttu-id="1b309-127">Чтобы настроить интеграцию SAP HANA с Azure AD, необходимо добавить SAP HANA из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1b309-127">To configure the integration of SAP HANA into Azure AD, you need to add SAP HANA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b309-128">**Чтобы добавить SAP HANA из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="1b309-128">**To add SAP HANA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b309-129">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b309-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="1b309-131">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="1b309-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1b309-132">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1b309-132">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="1b309-134">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="1b309-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="1b309-136">В поле поиска введите **SAP HANA**, выберите **SAP HANA** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="1b309-136">In the search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button to add the application.</span></span> 

    ![Новое приложение](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b309-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b309-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b309-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение SAP HANA с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b309-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1b309-140">Для работы единого входа в Azure AD необходимо знать, какой пользователь в SAP HANA соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b309-140">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP HANA is to a user in Azure AD.</span></span> <span data-ttu-id="1b309-141">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1b309-141">In other words, a link relationship between an Azure AD user and the related user in SAP HANA needs to be established.</span></span>

<span data-ttu-id="1b309-142">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1b309-142">In SAP HANA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1b309-143">Чтобы настроить и проверить единый вход Azure AD в SAP HANA, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="1b309-143">To configure and test Azure AD single sign-on with SAP HANA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b309-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="1b309-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1b309-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b309-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b309-146">**[Создание тестового пользователя SAP HANA](#creating-a-sap-hana-test-user)** требуется для создания в SAP HANA пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b309-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - to have a counterpart of Britta Simon in SAP HANA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b309-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b309-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b309-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1b309-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b309-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b309-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b309-150">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1b309-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="1b309-151">**Чтобы настроить единый вход Azure AD в SAP HANA, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="1b309-151">**To configure Azure AD single sign-on with SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="1b309-152">На портале Azure на странице интеграции с приложением **SAP NetWeaver** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="1b309-152">In the Azure portal, on the **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1b309-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="1b309-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="1b309-156">В разделе **Домены и URL-адреса приложения SAP HANA** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1b309-156">On the **SAP HANA Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="1b309-158">а.</span><span class="sxs-lookup"><span data-stu-id="1b309-158">a.</span></span> <span data-ttu-id="1b309-159">В текстовом поле **Идентификатор** введите `HA100`.</span><span class="sxs-lookup"><span data-stu-id="1b309-159">In the **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="1b309-160">b.</span><span class="sxs-lookup"><span data-stu-id="1b309-160">b.</span></span> <span data-ttu-id="1b309-161">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`.</span><span class="sxs-lookup"><span data-stu-id="1b309-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1b309-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1b309-162">These values are not real.</span></span> <span data-ttu-id="1b309-163">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="1b309-163">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1b309-164">Чтобы получить их, обратитесь в [службу поддержки клиентов SAP HANA](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="1b309-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="1b309-165">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1b309-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="1b309-167">Если сертификат не активен, активируйте его, установив флажок "Сделать сертификат активным" в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b309-167">If certificate is not active then make it active by clicking the “Make new certificate active” checkbox in the Azure AD.</span></span> 

5. <span data-ttu-id="1b309-168">Приложение SAP HANA ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="1b309-168">SAP HANA application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1b309-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="1b309-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="1b309-170">Здесь сопоставлен **идентификатор пользователя** с функцией **ExtractMailPrefix()** **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="1b309-170">Here we have mapped the **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="1b309-171">Таким образом получено значение префикса адреса электронной почты пользователя, которое представляет собой уникальный идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b309-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="1b309-172">Он будет отправляться в приложение SAP HANA в каждом успешном ответе.</span><span class="sxs-lookup"><span data-stu-id="1b309-172">This is sent to the SAP HANA application in every successful response.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="1b309-174">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1b309-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="1b309-175">а.</span><span class="sxs-lookup"><span data-stu-id="1b309-175">a.</span></span> <span data-ttu-id="1b309-176">Из раскрывающегося списка **Идентификатор пользователя** выберите **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="1b309-176">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="1b309-177">b.</span><span class="sxs-lookup"><span data-stu-id="1b309-177">b.</span></span> <span data-ttu-id="1b309-178">В раскрывающемся списке **Почта** выберите **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="1b309-178">In the **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="1b309-179">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1b309-179">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="1b309-181">Для настройки единого входа на стороне **SAP HANA** войдите в **веб-консоль XSA HANA**, перейдя к соответствующей конечной точке HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1b309-181">To configure single sign-on on **SAP HANA** side, login to your **HANA XSA Web Console**  by browsing to the respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="1b309-182">В конфигурации по умолчанию URL-адрес перенаправляет запрос на экран входа в систему, который требует учетные данные прошедшего проверку подлинности пользователя базы данных SAP HANA, чтобы завершить процесс входа в систему.</span><span class="sxs-lookup"><span data-stu-id="1b309-182">In the default configuration, the URL redirects the request to a logon screen, which requires the credentials of an authenticated SAP HANA database user to complete the logon process.</span></span> <span data-ttu-id="1b309-183">Пользователь, который входит в систему, должен иметь разрешения, необходимые для выполнения задач администрирования SAML.</span><span class="sxs-lookup"><span data-stu-id="1b309-183">The user who logs on must have the privileges required to perform SAML administration tasks.</span></span>

9. <span data-ttu-id="1b309-184">В веб-интерфейсе XSA перейдите к **поставщику удостоверений SAML** и в нем щелкните **"+"** в нижней части экрана, чтобы отобразить область Add Identity Provider Info (Добавление сведений о поставщике удостоверений) и выполните такие действия:</span><span class="sxs-lookup"><span data-stu-id="1b309-184">In the XSA Web Interface, navigate to **SAML Identity Provider** and from there, click the **“+”** -button on the bottom of the screen to display the Add Identity Provider Info pane and perform the following steps:</span></span>

    ![Добавление поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="1b309-186">а.</span><span class="sxs-lookup"><span data-stu-id="1b309-186">a.</span></span> <span data-ttu-id="1b309-187">В области **Add Identity Provider Info** (Добавление сведений о поставщике удостоверений) в текстовое поле **Metadata** (Метаданные) добавьте содержимое XML-файла метаданных, скачанного с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1b309-187">In the **Add Identity Provider Info** pane, paste the contents of the Metadata XML, which you have downloaded from Azure portal into the **Metadata** textbox.</span></span>

    ![Добавление параметров поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="1b309-189">b.</span><span class="sxs-lookup"><span data-stu-id="1b309-189">b.</span></span> <span data-ttu-id="1b309-190">Если содержимое XML-документа является допустимым, процесс синтаксического анализа извлечет сведения, необходимые для вставки в поля **темы, идентификатора сущности и издателя** в области экрана General Data (Общие данные) и поля URL-адресов в области экрана Destination (Место назначения), например, **базовый URL-адрес и URL-адрес единого входа (*)**.</span><span class="sxs-lookup"><span data-stu-id="1b309-190">If the contents of the XML document are valid, the parsing process extracts the information required to insert into the **Subject, Entity ID, and Issuer** fields in the General Data screen area, and the URL fields in the Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Добавление параметров поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="1b309-192">c.</span><span class="sxs-lookup"><span data-stu-id="1b309-192">c.</span></span> <span data-ttu-id="1b309-193">В поле Name (Имя) области экрана General Data (Общие данные) введите имя нового поставщика удостоверений единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="1b309-193">In the Name box of the General Data screen area, enter a name for the new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="1b309-194">Имя поставщика удостоверений SAML является обязательным и должно быть уникальным. Оно появится в списке доступных поставщиков удостоверений SAML, который отображается при выборе SAML в качестве метода проверки подлинности для приложений XS SAP HANA, например, в области экрана Authentication (Проверка подлинности) средства управления артефактом XS.</span><span class="sxs-lookup"><span data-stu-id="1b309-194">The name of the SAML IDP is mandatory and must be unique; it appears in the list of available SAML IDPs that is displayed, if you select SAML as the authentication method for SAP HANA XS applications to use, for example, in the Authentication screen area of the XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="1b309-195">Сохраните сведения о новом поставщике удостоверений SAML.</span><span class="sxs-lookup"><span data-stu-id="1b309-195">Save the details of the new SAML identity provider.</span></span> <span data-ttu-id="1b309-196">Нажмите кнопку **Save** (Сохранить), чтобы сохранить сведения о поставщике удостоверений SAML и добавить нового поставщика удостоверений SAML в список известных поставщиков удостоверений SAML.</span><span class="sxs-lookup"><span data-stu-id="1b309-196">Choose **Save** to save the details of the SAML identity provider and add the new SAML IDP to the list of known SAML IDPs.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="1b309-198">В HANA Studio в свойствах системы на вкладке **Configuration** (Конфигурация) отфильтруйте параметры по **SAML** и измените значение параметра **assertion_timeout** с **10 секунд** на **120 секунд**.</span><span class="sxs-lookup"><span data-stu-id="1b309-198">In HANA Studio within the system properties of the **Configuration** tab, just filter settings by **saml** and adjust the **assertion_timeout** from **10 sec** to **120 sec**.</span></span>

    ![Параметр assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="1b309-200">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="1b309-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1b309-201">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="1b309-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1b309-202">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="1b309-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b309-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b309-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b309-204">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b309-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1b309-206">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="1b309-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b309-207">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b309-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b309-209">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="1b309-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b309-211">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1b309-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b309-213">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1b309-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b309-215">а.</span><span class="sxs-lookup"><span data-stu-id="1b309-215">a.</span></span> <span data-ttu-id="1b309-216">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b309-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b309-217">b.</span><span class="sxs-lookup"><span data-stu-id="1b309-217">b.</span></span> <span data-ttu-id="1b309-218">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1b309-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b309-219">c.</span><span class="sxs-lookup"><span data-stu-id="1b309-219">c.</span></span> <span data-ttu-id="1b309-220">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="1b309-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1b309-221">d.</span><span class="sxs-lookup"><span data-stu-id="1b309-221">d.</span></span> <span data-ttu-id="1b309-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1b309-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="1b309-223">Создание тестового пользователя SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1b309-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="1b309-224">Чтобы пользователи Azure AD могли выполнять вход в SAP HANA, они должны быть подготовлены в SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1b309-224">To enable Azure AD users to log in to SAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="1b309-225">SAP HANA поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1b309-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1b309-226">Если необходимо создать пользователя вручную, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1b309-226">If you need to create a user manually, perform the following steps:</span></span>

>[!Note]
><span data-ttu-id="1b309-227">Можно изменить метод внешней проверки, используемый пользователем.</span><span class="sxs-lookup"><span data-stu-id="1b309-227">You can change the external authentication used by the user.</span></span>
<span data-ttu-id="1b309-228">Внешние пользователи проходят проверку подлинности с помощью внешней системы, например системы Kerberos.</span><span class="sxs-lookup"><span data-stu-id="1b309-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="1b309-229">Чтобы получить дополнительные сведения о внешних удостоверениях, свяжитесь со своим [администратором домена](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="1b309-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="1b309-230">Откройте [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) от имени администратора и включите пользователя базы данных для единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="1b309-230">Open the [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable the DB-User for SAML SSO.</span></span>

    ![создать пользователя](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="1b309-232">Установите невидимый флажок слева от **SAML** и перейдите по ссылке для настройки.</span><span class="sxs-lookup"><span data-stu-id="1b309-232">Tick the invisible checkbox to the left of **SAML** and follow the Configure link.</span></span>

3. <span data-ttu-id="1b309-233">Нажмите кнопку **Add** (Добавить), чтобы добавить поставщика удостоверений SAML, а затем нажмите кнопку **ОК**, выбрав соответствующего поставщика удостоверений SAML.</span><span class="sxs-lookup"><span data-stu-id="1b309-233">Click **Add** to add the SAML IDP and click **OK** selecting the appropriate SAML IDP.</span></span>

4. <span data-ttu-id="1b309-234">Добавьте **внешнее удостоверение** (например,</span><span class="sxs-lookup"><span data-stu-id="1b309-234">Add the **External Identity** (ex.</span></span> <span data-ttu-id="1b309-235">Britta Simon) или выберите **Any** (Любой) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1b309-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="1b309-236">Если флажок Any (Любой) не установлен, имя пользователя в HANA должно точно совпадать с именем пользователя в имени участника-пользователя перед суффиксом домена (например, BrittaSimon@contoso.com станет BrittaSimon в HANA).</span><span class="sxs-lookup"><span data-stu-id="1b309-236">If "ANY" check-box is not checked, then the user name in HANA needs to exactly match the name of the user in the UPN before the domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="1b309-237">Для тестирования назначьте все роли **XS** пользователю.</span><span class="sxs-lookup"><span data-stu-id="1b309-237">For testing purposes, assign all **"XS"** roles to the user.</span></span>

    ![Назначение ролей](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="1b309-239">Следует предоставить разрешения, которые подходят только для вашего варианта использования.</span><span class="sxs-lookup"><span data-stu-id="1b309-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="1b309-240">Сохраните пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b309-240">Save the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1b309-241">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b309-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1b309-242">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1b309-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP HANA.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="1b309-244">**Чтобы назначить пользователя Britta Simon в SAP HANA, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="1b309-244">**To assign Britta Simon to SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="1b309-245">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1b309-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1b309-247">В списке приложений выберите **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="1b309-247">In the applications list, select **SAP HANA**.</span></span>

    ![Назначение пользователя](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="1b309-249">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1b309-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="1b309-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1b309-251">Click **Add** button.</span></span> <span data-ttu-id="1b309-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1b309-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="1b309-254">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b309-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1b309-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1b309-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b309-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1b309-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1b309-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1b309-257">Testing single sign-on</span></span>

<span data-ttu-id="1b309-258">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="1b309-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1b309-259">Щелкнув плитку SAP HANA на панели доступа, вы автоматически войдете в приложение SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1b309-259">When you click the SAP HANA tile in the Access Panel, you should get automatically signed-on to your SAP HANA application.</span></span>
<span data-ttu-id="1b309-260">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b309-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b309-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1b309-261">Additional resources</span></span>

* [<span data-ttu-id="1b309-262">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b309-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b309-263">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b309-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

