---
title: "Руководство по интеграции Azure Active Directory с ScaleX Enterprise | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="c2523-103">Руководство по интеграции Azure Active Directory с ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="c2523-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="c2523-104">В этом руководстве описано, как интегрировать ScaleX Enterprise с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c2523-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c2523-105">Интеграция ScaleX Enterprise с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c2523-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c2523-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c2523-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="c2523-107">Вы можете включить автоматический вход пользователей в ScaleX Enterprise (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2523-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c2523-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c2523-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c2523-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье</span><span class="sxs-lookup"><span data-stu-id="c2523-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="c2523-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c2523-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2523-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2523-111">Prerequisites</span></span>

<span data-ttu-id="c2523-112">Чтобы настроить интеграцию Azure AD с ScaleX Enterprise, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c2523-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="c2523-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c2523-113">An Azure AD subscription</span></span>
- <span data-ttu-id="c2523-114">подписка ScaleX Enterprise с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c2523-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2523-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c2523-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c2523-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c2523-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c2523-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c2523-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c2523-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2523-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c2523-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c2523-119">Scenario description</span></span>
<span data-ttu-id="c2523-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c2523-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c2523-121">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c2523-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c2523-122">Добавление ScaleX Enterprise из коллекции</span><span class="sxs-lookup"><span data-stu-id="c2523-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="c2523-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2523-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="c2523-124">Добавление ScaleX Enterprise из коллекции</span><span class="sxs-lookup"><span data-stu-id="c2523-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="c2523-125">Чтобы настроить интеграцию приложения ScaleX Enterprise с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c2523-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c2523-126">**Добавление приложения ScaleX Enterprise из коллекции**</span><span class="sxs-lookup"><span data-stu-id="c2523-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c2523-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2523-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c2523-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c2523-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c2523-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c2523-130">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c2523-132">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c2523-132">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c2523-134">В поле поиска введите **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="c2523-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="c2523-136">На панели результатов выберите **ScaleX Enterprise** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="c2523-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c2523-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2523-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c2523-139">В этом разделе описана настройка и проверка единого входа Azure AD в ScaleX Enterprise с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2523-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c2523-140">Для работы единого входа службе Azure AD нужно знать, какой пользователь в ScaleX Enterprise соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2523-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="c2523-141">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c2523-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="c2523-142">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c2523-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="c2523-143">Чтобы настроить и проверить единый вход Azure AD в ScaleX Enterprise, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c2523-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c2523-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c2523-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c2523-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2523-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c2523-146">**[Создание тестового пользователя ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)** требуется для создания пользователя Britta Simon в ScaleX Enterprise, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2523-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c2523-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2523-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c2523-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c2523-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c2523-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2523-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c2523-150">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c2523-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="c2523-151">**Настройка единого входа Azure AD в ScaleX Enterprise**</span><span class="sxs-lookup"><span data-stu-id="c2523-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="c2523-152">На портале Azure на странице интеграции с приложением **ScaleX Enterprise** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c2523-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c2523-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c2523-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="c2523-156">Если вы хотите настроить приложение в режиме, инициированном **поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения ScaleX Enterprise** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c2523-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="c2523-158">а.</span><span class="sxs-lookup"><span data-stu-id="c2523-158">a.</span></span> <span data-ttu-id="c2523-159">В текстовом поле **Идентификатор** введите значение в следующем формате: `https://platform.rescale.com/saml2/<company id>/`.</span><span class="sxs-lookup"><span data-stu-id="c2523-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="c2523-160">b.</span><span class="sxs-lookup"><span data-stu-id="c2523-160">b.</span></span> <span data-ttu-id="c2523-161">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://platform.rescale.com/saml2/<company id>/acs/`.</span><span class="sxs-lookup"><span data-stu-id="c2523-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="c2523-162">Установите флажок **Показать дополнительные параметры URL-адресов**, если вы хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="c2523-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="c2523-164">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://platform.rescale.com/saml2/<company id>/sso/`.</span><span class="sxs-lookup"><span data-stu-id="c2523-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c2523-165">Значения, указанные выше, приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c2523-165">These are not the real values.</span></span> <span data-ttu-id="c2523-166">Измените их на фактические значения идентификатора, URL-адреса ответа или URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="c2523-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="c2523-167">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов ScaleX Enterprise](http://info.rescale.com/contact_sales).</span><span class="sxs-lookup"><span data-stu-id="c2523-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="c2523-168">Приложение ScaleX ожидает проверочные утверждения SAML в определенном формате, который требует изменить настраиваемые сопоставления атрибутов для конфигурации атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="c2523-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="c2523-169">Установите флажок **Просмотреть и изменить все другие атрибуты пользователей**, чтобы открыть пользовательские параметры атрибутов.</span><span class="sxs-lookup"><span data-stu-id="c2523-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="c2523-171">а.</span><span class="sxs-lookup"><span data-stu-id="c2523-171">a.</span></span> <span data-ttu-id="c2523-172">Щелкните правой кнопкой мыши атрибут **name** и щелкните "Удалить".</span><span class="sxs-lookup"><span data-stu-id="c2523-172">Right click the attribute **name** and click delete.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="c2523-174">b.</span><span class="sxs-lookup"><span data-stu-id="c2523-174">b.</span></span> <span data-ttu-id="c2523-175">Щелкните атрибут **emailaddress**, чтобы открыть окно "Изменить атрибут".</span><span class="sxs-lookup"><span data-stu-id="c2523-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="c2523-176">Измените его значение с **user.mail** на **user.userprincipalname** и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="c2523-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="c2523-178">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c2523-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="c2523-180">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c2523-180">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c2523-182">В разделе **Настройка ScaleX Enterprise** щелкните **Настроить ScaleX Enterprise**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c2523-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c2523-183">Скопируйте **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="c2523-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="c2523-185">Чтобы настроить единый вход на стороне **ScaleX Enterprise**, войдите на веб-сайт компании ScaleX Enterprise в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c2523-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="c2523-186">В правом верхнем углу щелкните меню и выберите **Contoso Administration** (Администрирование Contoso).</span><span class="sxs-lookup"><span data-stu-id="c2523-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c2523-187">Contoso является лишь примером.</span><span class="sxs-lookup"><span data-stu-id="c2523-187">Contoso is just an example.</span></span> <span data-ttu-id="c2523-188">Используйте фактическое название компании.</span><span class="sxs-lookup"><span data-stu-id="c2523-188">This should be your actual Company Name.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="c2523-190">В верхнем меню выберите **Integrations** (Интеграции) и щелкните **Single Sign-On** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="c2523-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="c2523-192">Заполните форму следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c2523-192">Complete the form as follows:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="c2523-194">а.</span><span class="sxs-lookup"><span data-stu-id="c2523-194">a.</span></span> <span data-ttu-id="c2523-195">Выберите **Create any user who can authenticate with SSO** (Создание любого пользователя, который может выполнить проверку подлинности с помощью единого входа).</span><span class="sxs-lookup"><span data-stu-id="c2523-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="c2523-196">b.</span><span class="sxs-lookup"><span data-stu-id="c2523-196">b.</span></span> <span data-ttu-id="c2523-197">**Service Provider SAML** (Поставщик услуг SAML). Вставьте значение ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***.</span><span class="sxs-lookup"><span data-stu-id="c2523-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="c2523-198">c.</span><span class="sxs-lookup"><span data-stu-id="c2523-198">c.</span></span> <span data-ttu-id="c2523-199">**Name of Identity Provider email field in ACS response** (Имя поля электронного адреса поставщика удостоверений в ответе ACS). Вставьте значение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="c2523-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="c2523-200">d.</span><span class="sxs-lookup"><span data-stu-id="c2523-200">d.</span></span> <span data-ttu-id="c2523-201">**Identity Provider EntityDescriptor Entity ID** (Идентификатор сущности EntityDescriptor поставщика удостоверений). Вставьте значение **идентификатора сущности SAML**, скопированное с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c2523-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="c2523-202">д.</span><span class="sxs-lookup"><span data-stu-id="c2523-202">e.</span></span> <span data-ttu-id="c2523-203">**Identity Provider SingleSignOnService URL** (URL-адрес SingleSignOnService поставщика удостоверений). Вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c2523-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="c2523-204">f.</span><span class="sxs-lookup"><span data-stu-id="c2523-204">f.</span></span> <span data-ttu-id="c2523-205">**Identity Provider public X509 certificate** (Общий сертификат X509 поставщика удостоверений). Откройте сертификат X509, скачанный на портале Azure, в Блокноте и вставьте содержимое в это поле.</span><span class="sxs-lookup"><span data-stu-id="c2523-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="c2523-206">Убедитесь в отсутствии разрыва строк в середине содержимого сертификата.</span><span class="sxs-lookup"><span data-stu-id="c2523-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="c2523-207">g.</span><span class="sxs-lookup"><span data-stu-id="c2523-207">g.</span></span> <span data-ttu-id="c2523-208">Установите следующие флажки: **Enabled, Encrypt NameID and Sign AuthnRequests** (Включено, Шифрование идентификатора имени, Подпись AuthnRequests).</span><span class="sxs-lookup"><span data-stu-id="c2523-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="c2523-209">h.</span><span class="sxs-lookup"><span data-stu-id="c2523-209">h.</span></span> <span data-ttu-id="c2523-210">Нажмите кнопку **Update SSO Settings** (Обновить параметры единого входа), чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="c2523-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="c2523-211">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c2523-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c2523-212">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c2523-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c2523-213">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c2523-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c2523-214">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2523-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="c2523-215">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2523-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c2523-217">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c2523-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c2523-218">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2523-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c2523-220">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="c2523-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c2523-222">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="c2523-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c2523-224">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c2523-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c2523-226">а.</span><span class="sxs-lookup"><span data-stu-id="c2523-226">a.</span></span> <span data-ttu-id="c2523-227">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c2523-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c2523-228">b.</span><span class="sxs-lookup"><span data-stu-id="c2523-228">b.</span></span> <span data-ttu-id="c2523-229">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c2523-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c2523-230">c.</span><span class="sxs-lookup"><span data-stu-id="c2523-230">c.</span></span> <span data-ttu-id="c2523-231">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c2523-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c2523-232">d.</span><span class="sxs-lookup"><span data-stu-id="c2523-232">d.</span></span> <span data-ttu-id="c2523-233">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c2523-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="c2523-234">Создание тестового пользователя ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="c2523-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="c2523-235">Чтобы пользователи Azure AD могли входить в ScaleX Enterprise, их нужно подготовить для ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c2523-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="c2523-236">В случае с ScaleX Enterprise подготовка пользователей осуществляется автоматически, при этом никакие ручные действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="c2523-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="c2523-237">Для всех пользователей, которые успешно выполнят проверку подлинности с помощью учетных данных единого входа, будет автоматически выполняться подготовка на стороне ScaleX.</span><span class="sxs-lookup"><span data-stu-id="c2523-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c2523-238">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2523-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c2523-239">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c2523-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c2523-241">**Назначение пользователя Britta Simon приложению ScaleX Enterprise**</span><span class="sxs-lookup"><span data-stu-id="c2523-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="c2523-242">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c2523-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c2523-244">В списке приложений выберите **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="c2523-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="c2523-246">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c2523-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c2523-248">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c2523-248">Click **Add** button.</span></span> <span data-ttu-id="c2523-249">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c2523-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c2523-251">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c2523-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c2523-252">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c2523-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c2523-253">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c2523-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="c2523-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c2523-254">Testing single sign-on</span></span>

<span data-ttu-id="c2523-255">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c2523-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c2523-256">Щелкнув плитку ScaleX Enterprise на панели доступа, вы автоматически войдете в приложение ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c2523-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="c2523-257">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c2523-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c2523-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c2523-258">Additional resources</span></span>

* [<span data-ttu-id="c2523-259">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2523-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c2523-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c2523-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

