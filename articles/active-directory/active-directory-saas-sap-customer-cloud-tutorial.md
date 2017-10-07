---
title: "Руководство по интеграции Azure Active Directory с SAP Cloud for Customer | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и облаком SAP для клиента."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="40baa-103">Руководство по интеграции Azure Active Directory с SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="40baa-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="40baa-104">В этом учебнике вы узнаете, как SAP toointegrate облака для клиента в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40baa-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40baa-105">Интеграция облака SAP для клиента в Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="40baa-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="40baa-106">Можно управлять в Azure AD, имеющего доступ tooSAP облака для клиента</span><span class="sxs-lookup"><span data-stu-id="40baa-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="40baa-107">Вы можете включить вашей пользователей tooautomatically get вошедшего tooSAP облака для клиента (Single Sign-On) учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="40baa-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40baa-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="40baa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="40baa-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40baa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40baa-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="40baa-110">Prerequisites</span></span>

<span data-ttu-id="40baa-111">tooconfigure интеграция Azure AD с облаком SAP для клиента требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="40baa-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="40baa-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="40baa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40baa-113">подписка SAP Cloud for Customer с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="40baa-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40baa-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="40baa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40baa-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="40baa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40baa-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="40baa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40baa-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40baa-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40baa-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="40baa-118">Scenario description</span></span>
<span data-ttu-id="40baa-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="40baa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40baa-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="40baa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40baa-121">Добавление облака SAP для клиента из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="40baa-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="40baa-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40baa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="40baa-123">Добавление облака SAP для клиента из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="40baa-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="40baa-124">tooconfigure hello интеграции облачных SAP для клиента в Azure AD, необходимо tooadd облака SAP для клиента из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="40baa-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="40baa-125">**tooadd облака SAP для клиента из коллекции hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="40baa-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="40baa-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="40baa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40baa-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="40baa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="40baa-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40baa-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="40baa-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="40baa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="40baa-133">Введите в поле поиска hello **облака SAP для клиента**.</span><span class="sxs-lookup"><span data-stu-id="40baa-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="40baa-135">В панели результатов hello выберите **облака SAP для клиента**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="40baa-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40baa-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40baa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40baa-138">В этом разделе описана настройка и проверка единого входа Azure AD в SAP Cloud for Customer с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40baa-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40baa-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в облаке SAP для клиента является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40baa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="40baa-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в облаке SAP для клиента должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="40baa-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="40baa-141">В облаке SAP для клиента, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="40baa-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="40baa-142">tooconfigure и тестирования Azure AD единого входа с облаком SAP для клиента, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="40baa-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="40baa-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="40baa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="40baa-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="40baa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40baa-145">**[Создание облака SAP для тестового пользователя клиента](#creating-a-sap-cloud-for-customer-test-user)**  -toohave аналог Саймон Britta в облаке SAP для клиента, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="40baa-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="40baa-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="40baa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40baa-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40baa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40baa-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40baa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40baa-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в облаке SAP для клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="40baa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="40baa-150">**tooconfigure Azure AD единого входа с облаком SAP для клиента, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="40baa-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="40baa-151">В hello в hello портала Azure **облака SAP для клиента** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="40baa-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="40baa-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="40baa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="40baa-155">На hello **облако SAP для домена клиента и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="40baa-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="40baa-157">а.</span><span class="sxs-lookup"><span data-stu-id="40baa-157">a.</span></span> <span data-ttu-id="40baa-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="40baa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="40baa-159">b.</span><span class="sxs-lookup"><span data-stu-id="40baa-159">b.</span></span> <span data-ttu-id="40baa-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="40baa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="40baa-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="40baa-161">These values are not real.</span></span> <span data-ttu-id="40baa-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="40baa-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="40baa-163">Обратитесь к [облако SAP для поддержки клиента клиента](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="40baa-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="40baa-164">На hello **атрибуты пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="40baa-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="40baa-166">а.</span><span class="sxs-lookup"><span data-stu-id="40baa-166">a.</span></span> <span data-ttu-id="40baa-167">В **идентификатор пользователя** список, выберите hello **ExtractMailPrefix()** функции.</span><span class="sxs-lookup"><span data-stu-id="40baa-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="40baa-168">b.</span><span class="sxs-lookup"><span data-stu-id="40baa-168">b.</span></span> <span data-ttu-id="40baa-169">Из hello **Mail** список, атрибут пользователя выберите hello требуется toouse вашей реализации.</span><span class="sxs-lookup"><span data-stu-id="40baa-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="40baa-170">Например если требуется toouse hello EmployeeID как уникальный идентификатор пользователя и хранящимся в hello ExtensionAttribute2 значение атрибута hello, выберите user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="40baa-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="40baa-171">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="40baa-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="40baa-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="40baa-173">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="40baa-175">На hello **облако SAP для конфигурации клиента** щелкните **Настройка облака SAP для клиента** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="40baa-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="40baa-176">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="40baa-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="40baa-178">tooget SSO настроен, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="40baa-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="40baa-179">а.</span><span class="sxs-lookup"><span data-stu-id="40baa-179">a.</span></span> <span data-ttu-id="40baa-180">Войдите на портал SAP Cloud for Customer с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="40baa-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="40baa-181">b.</span><span class="sxs-lookup"><span data-stu-id="40baa-181">b.</span></span> <span data-ttu-id="40baa-182">Перейдите toohello **приложения и общие задачи управления пользователя** и нажмите кнопку hello **поставщика удостоверений** вкладки.</span><span class="sxs-lookup"><span data-stu-id="40baa-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="40baa-183">c.</span><span class="sxs-lookup"><span data-stu-id="40baa-183">c.</span></span> <span data-ttu-id="40baa-184">Нажмите кнопку **нового поставщика удостоверений** и выберите hello метаданных XML-файл, загруженный с портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="40baa-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="40baa-185">Путем импорта метаданных hello, hello системы автоматически отправляет сертификат подписи требуется указать hello и сертификат шифрования.</span><span class="sxs-lookup"><span data-stu-id="40baa-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="40baa-187">d.</span><span class="sxs-lookup"><span data-stu-id="40baa-187">d.</span></span> <span data-ttu-id="40baa-188">Azure Active Directory требуется элемент hello URL-адрес службы утверждения потребителя в запросе SAML hello, поэтому выберите hello **включает утверждение потребителя URL-адрес службы** флажок.</span><span class="sxs-lookup"><span data-stu-id="40baa-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="40baa-189">д.</span><span class="sxs-lookup"><span data-stu-id="40baa-189">e.</span></span> <span data-ttu-id="40baa-190">Щелкните **Activate Single Sign-On**(Активировать единый вход).</span><span class="sxs-lookup"><span data-stu-id="40baa-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="40baa-191">Е.</span><span class="sxs-lookup"><span data-stu-id="40baa-191">f.</span></span> <span data-ttu-id="40baa-192">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="40baa-192">Save your changes.</span></span>
   
    <span data-ttu-id="40baa-193">ж.</span><span class="sxs-lookup"><span data-stu-id="40baa-193">g.</span></span> <span data-ttu-id="40baa-194">Нажмите кнопку hello **Мои системы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="40baa-194">Click hello **My System** tab.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="40baa-196">h.</span><span class="sxs-lookup"><span data-stu-id="40baa-196">h.</span></span> <span data-ttu-id="40baa-197">В текстовое поле **Azure AD Sign On URL** (URL-адрес входа Azure AD) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="40baa-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="40baa-199">i.</span><span class="sxs-lookup"><span data-stu-id="40baa-199">i.</span></span> <span data-ttu-id="40baa-200">Указать ли hello сотрудника можно вручную выбрать между войти с помощью идентификатора пользователя и пароль или единого входа, выбрав hello **Выбор поставщика удостоверений вручную**.</span><span class="sxs-lookup"><span data-stu-id="40baa-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="40baa-201">j.</span><span class="sxs-lookup"><span data-stu-id="40baa-201">j.</span></span> <span data-ttu-id="40baa-202">В hello **URL-адрес SSO** статьи, укажите hello URL-адрес, который должен использоваться с вашей toosign сотрудников в системе toohello.</span><span class="sxs-lookup"><span data-stu-id="40baa-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="40baa-203">В hello **tooEmployee URL-адрес отправки** список, можно выбрать между hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="40baa-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="40baa-204">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="40baa-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="40baa-205">Hello система отправляет только hello нормальная URL-адрес toohello сотрудника.</span><span class="sxs-lookup"><span data-stu-id="40baa-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="40baa-206">Сотрудник Hello не может войти в систему с помощью единого входа и должны использовать пароль или сертификат вместо.</span><span class="sxs-lookup"><span data-stu-id="40baa-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="40baa-207">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="40baa-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="40baa-208">Hello система отправляет только hello сотрудник toohello URL-адрес единого входа.</span><span class="sxs-lookup"><span data-stu-id="40baa-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="40baa-209">Сотрудник Hello можно войти в систему с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="40baa-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="40baa-210">Перенаправляет запрос проверки подлинности через hello поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="40baa-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="40baa-211">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="40baa-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="40baa-212">Если единый вход не активен, hello система отправляет hello нормальная URL-адрес toohello сотрудника.</span><span class="sxs-lookup"><span data-stu-id="40baa-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="40baa-213">Если активен единого входа, hello система проверяет, содержит ли сотрудника hello пароль.</span><span class="sxs-lookup"><span data-stu-id="40baa-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="40baa-214">Если пароль, URL-адрес единого входа и URL-адрес единого входа не отправляются toohello сотрудника.</span><span class="sxs-lookup"><span data-stu-id="40baa-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="40baa-215">Тем не менее если сотрудник hello не имеет пароля, toohello сотрудника отправляется только hello URL-адрес единого входа.</span><span class="sxs-lookup"><span data-stu-id="40baa-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="40baa-216">k.</span><span class="sxs-lookup"><span data-stu-id="40baa-216">k.</span></span> <span data-ttu-id="40baa-217">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="40baa-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="40baa-218">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="40baa-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="40baa-219">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="40baa-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="40baa-220">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="40baa-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40baa-221">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="40baa-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="40baa-222">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="40baa-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="40baa-224">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="40baa-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="40baa-225">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="40baa-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40baa-227">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="40baa-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40baa-229">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="40baa-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40baa-231">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="40baa-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40baa-233">а.</span><span class="sxs-lookup"><span data-stu-id="40baa-233">a.</span></span> <span data-ttu-id="40baa-234">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40baa-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40baa-235">b.</span><span class="sxs-lookup"><span data-stu-id="40baa-235">b.</span></span> <span data-ttu-id="40baa-236">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="40baa-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40baa-237">c.</span><span class="sxs-lookup"><span data-stu-id="40baa-237">c.</span></span> <span data-ttu-id="40baa-238">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="40baa-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="40baa-239">d.</span><span class="sxs-lookup"><span data-stu-id="40baa-239">d.</span></span> <span data-ttu-id="40baa-240">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="40baa-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="40baa-241">Создание тестового пользователя в SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="40baa-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="40baa-242">В этом разделе описано, как создать пользователя Britta Simon в приложении SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="40baa-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="40baa-243">Можно работать с [облако SAP для поддержки клиентов](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd пользователей hello в hello SAP облачной платформы клиента.</span><span class="sxs-lookup"><span data-stu-id="40baa-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="40baa-244">Убедитесь, что значение идентификатора имени должен совпадать с hello поле имени пользователя в hello SAP облачной платформы клиента.</span><span class="sxs-lookup"><span data-stu-id="40baa-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="40baa-245">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="40baa-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="40baa-246">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAP облака для клиента.</span><span class="sxs-lookup"><span data-stu-id="40baa-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="40baa-248">**tooassign tooSAP Britta Simon облака для клиента, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="40baa-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="40baa-249">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40baa-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="40baa-251">В списке приложений hello выберите **облака SAP для клиента**.</span><span class="sxs-lookup"><span data-stu-id="40baa-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="40baa-253">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="40baa-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="40baa-255">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="40baa-255">Click **Add** button.</span></span> <span data-ttu-id="40baa-256">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="40baa-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="40baa-258">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="40baa-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="40baa-259">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="40baa-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40baa-260">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="40baa-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40baa-261">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="40baa-261">Testing single sign-on</span></span>

<span data-ttu-id="40baa-262">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="40baa-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="40baa-263">При нажатии кнопки hello облака SAP для клиента плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour облака SAP для клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="40baa-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="40baa-264">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="40baa-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40baa-265">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="40baa-265">Additional resources</span></span>

* [<span data-ttu-id="40baa-266">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40baa-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40baa-267">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="40baa-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

