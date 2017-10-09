---
title: "Руководство по интеграции Azure Active Directory с песочницей Salesforce | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и песочницы Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="d16ae-103">Учебник. Интеграция Azure Active Directory с песочницей Salesforce</span><span class="sxs-lookup"><span data-stu-id="d16ae-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="d16ae-104">В этом учебнике вы узнаете, как toointegrate песочницы Salesforce с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d16ae-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d16ae-105">Интеграция песочницы Salesforce с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d16ae-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d16ae-106">Можно управлять в Azure AD, имеющего доступ tooSalesforce "песочницы"</span><span class="sxs-lookup"><span data-stu-id="d16ae-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="d16ae-107">Можно включить на пользователей tooautomatically get вошедшего tooSalesforce "песочницы" (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="d16ae-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d16ae-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d16ae-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d16ae-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d16ae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d16ae-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d16ae-110">Prerequisites</span></span>

<span data-ttu-id="d16ae-111">tooconfigure интеграция Azure AD с песочницей Salesforce требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d16ae-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="d16ae-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d16ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d16ae-113">подписка Salesforce Sandbox с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d16ae-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d16ae-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d16ae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d16ae-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d16ae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d16ae-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d16ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d16ae-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d16ae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d16ae-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d16ae-118">Scenario description</span></span>
<span data-ttu-id="d16ae-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d16ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d16ae-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d16ae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d16ae-121">Добавление из галереи hello песочницы Salesforce</span><span class="sxs-lookup"><span data-stu-id="d16ae-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="d16ae-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d16ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="d16ae-123">Добавление из галереи hello песочницы Salesforce</span><span class="sxs-lookup"><span data-stu-id="d16ae-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="d16ae-124">tooconfigure hello интеграцией песочницы Salesforce с Azure AD, вы должны tooadd песочницы Salesforce из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d16ae-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d16ae-125">**tooadd песочницы Salesforce из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d16ae-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d16ae-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d16ae-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d16ae-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d16ae-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d16ae-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="d16ae-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d16ae-133">Введите в поле поиска hello **песочницы Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="d16ae-135">В панели результатов hello выберите **песочницы Salesforce**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d16ae-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d16ae-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d16ae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d16ae-138">В этом разделе описана настройка и проверка единого входа Azure AD в Salesforce Sandbox с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d16ae-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d16ae-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в песочницу Salesforce является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d16ae-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="d16ae-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в песочницу Salesforce должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d16ae-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="d16ae-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в песочницу Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d16ae-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="d16ae-142">tooconfigure и тестирования Azure AD единого входа с песочницей Salesforce, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d16ae-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d16ae-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d16ae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d16ae-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d16ae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d16ae-145">**[Создание тестового пользователя песочницы Salesforce](#creating-a-salesforce-sandbox-test-user)**  -toohave аналог Саймон Britta в песочницу Salesforce, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="d16ae-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d16ae-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d16ae-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d16ae-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d16ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d16ae-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d16ae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d16ae-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d16ae-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="d16ae-150">**tooconfigure Azure AD единого входа с песочницей Salesforce, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d16ae-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="d16ae-151">В hello в hello портала Azure **песочницы Salesforce** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d16ae-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d16ae-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="d16ae-155">На hello **URL-адреса и домен песочницы Salesforce** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d16ae-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="d16ae-157">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="d16ae-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d16ae-158">Это значение не реальными hello.</span><span class="sxs-lookup"><span data-stu-id="d16ae-158">This value is not hello real.</span></span> <span data-ttu-id="d16ae-159">Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента песочницы Salesforce](https://help.salesforce.com/support) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="d16ae-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="d16ae-160">Если вы уже настроили единого входа для другого экземпляра песочницы Salesforce в вашем каталоге, то необходимо также настроить hello **идентификатор** toohave hello совпадает со значением hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="d16ae-161">Hello **идентификатор** поле можно найти путем проверки hello **Показывать дополнительные параметры** флажок на hello **настроить URL-адрес приложения** hello диалогового окна</span><span class="sxs-lookup"><span data-stu-id="d16ae-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="d16ae-162">На hello **сертификат подписи SAML** щелкните **сертификат** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="d16ae-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="d16ae-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d16ae-164">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d16ae-166">На hello **конфигурации песочницы Salesforce** щелкните **настроить песочницу Salesforce** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="d16ae-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d16ae-167">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="d16ae-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="d16ae-168">![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="d16ae-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="d16ae-169">Откройте новую вкладку в браузере и войдите в учетную запись администратора песочницы Salesforce tooyour.</span><span class="sxs-lookup"><span data-stu-id="d16ae-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="d16ae-170">В меню в верхней части hello hello выберите **установки**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="d16ae-172">Hello hello левой панели навигации щелкните **управления безопасностью**, а затем нажмите кнопку **параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="d16ae-174">На hello раздел параметров единого входа, выполните следующие шаги hello: ![настройки единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="d16ae-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="d16ae-175">а.</span><span class="sxs-lookup"><span data-stu-id="d16ae-175">a.</span></span>  <span data-ttu-id="d16ae-176">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="d16ae-177">b.</span><span class="sxs-lookup"><span data-stu-id="d16ae-177">b.</span></span>  <span data-ttu-id="d16ae-178">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-178">Click **New**.</span></span>

12. <span data-ttu-id="d16ae-179">На hello SAML единого входа «параметры» выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d16ae-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="d16ae-181">a.In hello в текстовое поле имя, имя типа hello hello конфигурации (например: *SPSSOWAAD\_тест*).</span><span class="sxs-lookup"><span data-stu-id="d16ae-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="d16ae-182">b.</span><span class="sxs-lookup"><span data-stu-id="d16ae-182">b.</span></span> <span data-ttu-id="d16ae-183">Вставить **идентификатор сущности SMAL** значение в hello **издателя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d16ae-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="d16ae-184">c.</span><span class="sxs-lookup"><span data-stu-id="d16ae-184">c.</span></span> <span data-ttu-id="d16ae-185">В hello **идентификатор сущности** введите **https://test.salesforce.com** при hello первый экземпляр песочницы Salesforce, добавляется tooyour каталога.</span><span class="sxs-lookup"><span data-stu-id="d16ae-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="d16ae-186">При добавлении экземпляра песочницы Salesforce, а затем для hello **идентификатор сущности** типа в hello **на URL-адрес входа**, которые должны быть в следующем формате:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="d16ae-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="d16ae-187">d.</span><span class="sxs-lookup"><span data-stu-id="d16ae-187">d.</span></span> <span data-ttu-id="d16ae-188">Нажмите кнопку **Обзор** tooupload hello загрузить сертификат.</span><span class="sxs-lookup"><span data-stu-id="d16ae-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="d16ae-189">д.</span><span class="sxs-lookup"><span data-stu-id="d16ae-189">e.</span></span> <span data-ttu-id="d16ae-190">Как **типа удостоверения SAML**выберите **утверждение, содержащее hello идентификатор федерации из объекта пользователя hello**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="d16ae-191">f.</span><span class="sxs-lookup"><span data-stu-id="d16ae-191">f.</span></span> <span data-ttu-id="d16ae-192">Как **расположения удостоверения SAML**выберите **удостоверение находится в элемент hello NameIdentifier оператора Subject hello**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="d16ae-193">ж.</span><span class="sxs-lookup"><span data-stu-id="d16ae-193">g.</span></span> <span data-ttu-id="d16ae-194">Вставить **единого входа URL-адрес службы** в hello **URL-адрес входа поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d16ae-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="d16ae-195">h.</span><span class="sxs-lookup"><span data-stu-id="d16ae-195">h.</span></span> <span data-ttu-id="d16ae-196">SFDC не поддерживает выход SAML.</span><span class="sxs-lookup"><span data-stu-id="d16ae-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="d16ae-197">Чтобы избежать этого, вставьте «https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0» в hello **URL-адрес выхода поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d16ae-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="d16ae-198">i.</span><span class="sxs-lookup"><span data-stu-id="d16ae-198">i.</span></span> <span data-ttu-id="d16ae-199">В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="d16ae-200">j.</span><span class="sxs-lookup"><span data-stu-id="d16ae-200">j.</span></span> <span data-ttu-id="d16ae-201">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="d16ae-202">Включение домена</span><span class="sxs-lookup"><span data-stu-id="d16ae-202">Enable your domain</span></span>
<span data-ttu-id="d16ae-203">В этом разделе предполагается, что вы уже создали домен.</span><span class="sxs-lookup"><span data-stu-id="d16ae-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="d16ae-204">Дополнительные сведения см. в разделе [Define Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US) (Определение доменного имени).</span><span class="sxs-lookup"><span data-stu-id="d16ae-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="d16ae-205">**tooenable к домену, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="d16ae-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="d16ae-206">Hello панели навигации слева щелкните **Управление доменами**, а затем нажмите кнопку **Мой домен.**</span><span class="sxs-lookup"><span data-stu-id="d16ae-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="d16ae-208">Убедитесь в правильности настройки домена.</span><span class="sxs-lookup"><span data-stu-id="d16ae-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="d16ae-209">В hello **параметры страницы входа** щелкните **изменить**, затем, по мере **службы проверки подлинности**, выберите имя hello hello SAML единого входа параметр из предыдущего hello статьи, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="d16ae-211">Как только домен настроен, пользователям следует использовать hello домена URL-адрес toologin toohello песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d16ae-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="d16ae-212">значение hello tooget hello URL-адреса, щелкните профиль единого входа hello, созданный в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d16ae-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="d16ae-213">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="d16ae-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d16ae-214">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="d16ae-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d16ae-215">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d16ae-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d16ae-216">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d16ae-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="d16ae-217">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d16ae-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d16ae-219">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d16ae-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d16ae-220">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d16ae-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d16ae-222">hello toodisplay список пользователей перейти слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d16ae-224">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d16ae-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d16ae-226">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d16ae-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d16ae-228">а.</span><span class="sxs-lookup"><span data-stu-id="d16ae-228">a.</span></span> <span data-ttu-id="d16ae-229">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d16ae-230">b.</span><span class="sxs-lookup"><span data-stu-id="d16ae-230">b.</span></span> <span data-ttu-id="d16ae-231">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d16ae-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d16ae-232">c.</span><span class="sxs-lookup"><span data-stu-id="d16ae-232">c.</span></span> <span data-ttu-id="d16ae-233">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d16ae-234">d.</span><span class="sxs-lookup"><span data-stu-id="d16ae-234">d.</span></span> <span data-ttu-id="d16ae-235">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="d16ae-236">Создание тестового пользователя Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="d16ae-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="d16ae-237">В этом разделе вы создадите в Salesforce Sandbox пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d16ae-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="d16ae-238">Salesforce Sandbox поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d16ae-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="d16ae-239">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="d16ae-239">There is no action item for you in this section.</span></span> <span data-ttu-id="d16ae-240">Если пользователь еще не существует в песочницу Salesforce, создается новый, при попытке tooaccess песочницы Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d16ae-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d16ae-241">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d16ae-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d16ae-242">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSalesforce "песочницы".</span><span class="sxs-lookup"><span data-stu-id="d16ae-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d16ae-244">**tooassign tooSalesforce Britta Simon "песочницы", выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d16ae-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="d16ae-245">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d16ae-247">В списке приложений hello выберите **песочницы Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="d16ae-249">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d16ae-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-251">Click **Add** button.</span></span> <span data-ttu-id="d16ae-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d16ae-254">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d16ae-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d16ae-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d16ae-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d16ae-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d16ae-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d16ae-257">Testing single sign-on</span></span>

<span data-ttu-id="d16ae-258">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="d16ae-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="d16ae-259">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d16ae-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d16ae-260">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d16ae-260">Additional resources</span></span>

* [<span data-ttu-id="d16ae-261">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d16ae-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d16ae-262">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d16ae-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d16ae-263">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="d16ae-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

