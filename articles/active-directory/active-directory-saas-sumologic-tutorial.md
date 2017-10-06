---
title: "Руководство по интеграции Azure Active Directory с SumoLogic | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="43525-103">Руководство. Интеграция Azure Active Directory с SumoLogic</span><span class="sxs-lookup"><span data-stu-id="43525-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="43525-104">В этом учебнике вы узнаете, как toointegrate SumoLogic с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43525-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43525-105">Интеграция SumoLogic с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="43525-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="43525-106">Можно управлять в Azure AD, имеющего доступ tooSumoLogic</span><span class="sxs-lookup"><span data-stu-id="43525-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="43525-107">Можно включить на пользователей tooautomatically get вошедшего tooSumoLogic (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="43525-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43525-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="43525-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="43525-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43525-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43525-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="43525-110">Prerequisites</span></span>

<span data-ttu-id="43525-111">tooconfigure интеграция Azure AD с SumoLogic требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="43525-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="43525-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="43525-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43525-113">подписка с поддержкой единого входа SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="43525-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43525-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="43525-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43525-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="43525-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43525-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="43525-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43525-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43525-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43525-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="43525-118">Scenario description</span></span>
<span data-ttu-id="43525-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="43525-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43525-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="43525-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43525-121">Добавление SumoLogic из галереи hello</span><span class="sxs-lookup"><span data-stu-id="43525-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="43525-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="43525-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="43525-123">Добавление SumoLogic из галереи hello</span><span class="sxs-lookup"><span data-stu-id="43525-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="43525-124">tooconfigure hello интеграции SumoLogic в Azure AD, вы должны tooadd SumoLogic из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="43525-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="43525-125">**tooadd SumoLogic из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43525-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="43525-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="43525-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43525-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="43525-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="43525-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="43525-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="43525-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="43525-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="43525-133">Введите в поле поиска hello **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="43525-133">In hello search box, type **SumoLogic**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="43525-135">В панели результатов hello выберите **SumoLogic**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="43525-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43525-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="43525-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43525-138">В этом разделе описана настройка и проверка единого входа Azure AD в SumoLogic с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43525-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="43525-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SumoLogic является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43525-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="43525-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в SumoLogic должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="43525-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="43525-141">В SumoLogic, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="43525-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="43525-142">tooconfigure и теста Azure AD единого входа с SumoLogic, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="43525-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="43525-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="43525-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="43525-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="43525-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43525-145">**[Создание тестового пользователя SumoLogic](#creating-a-sumologic-test-user) ** -toohave аналог Саймон Britta в SumoLogic, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="43525-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="43525-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="43525-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43525-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="43525-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43525-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="43525-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43525-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в SumoLogic приложения.</span><span class="sxs-lookup"><span data-stu-id="43525-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="43525-150">**Azure AD tooconfigure единого входа с SumoLogic, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43525-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="43525-151">В hello в hello портала Azure **SumoLogic** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="43525-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="43525-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="43525-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="43525-155">На hello **URL-адреса и домена SumoLogic** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="43525-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="43525-157">а.</span><span class="sxs-lookup"><span data-stu-id="43525-157">a.</span></span> <span data-ttu-id="43525-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="43525-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="43525-159">b.</span><span class="sxs-lookup"><span data-stu-id="43525-159">b.</span></span> <span data-ttu-id="43525-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="43525-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="43525-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="43525-161">These values are not real.</span></span> <span data-ttu-id="43525-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="43525-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="43525-163">Обратитесь к [группа поддержки клиент SumoLogic](https://www.sumologic.com/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="43525-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="43525-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="43525-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="43525-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="43525-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="43525-168">На hello **конфигурации SumoLogic** щелкните **Настройка SumoLogic** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="43525-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="43525-169">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="43525-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="43525-171">В другом окне браузера Войдите на сайте компании SumoLogic tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="43525-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="43525-172">Go слишком**управление \> безопасности**.</span><span class="sxs-lookup"><span data-stu-id="43525-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="43525-173">![Управление](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Управление")</span><span class="sxs-lookup"><span data-stu-id="43525-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="43525-174">Нажмите кнопку **SAML**.</span><span class="sxs-lookup"><span data-stu-id="43525-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="43525-175">![Глобальные параметры безопасности](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Глобальные параметры безопасности")</span><span class="sxs-lookup"><span data-stu-id="43525-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="43525-176">Из hello **выберите настройку или создайте новую** выберите **Azure AD**, а затем нажмите кнопку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="43525-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="43525-177">![Настройка SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Настройка SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="43525-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="43525-178">На hello **Настройка SAML 2.0** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="43525-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="43525-179">![Настройка SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Настройка SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="43525-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="43525-180">а.</span><span class="sxs-lookup"><span data-stu-id="43525-180">a.</span></span> <span data-ttu-id="43525-181">В hello **имя конфигурации** введите **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="43525-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="43525-182">b.</span><span class="sxs-lookup"><span data-stu-id="43525-182">b.</span></span> <span data-ttu-id="43525-183">Выберите **Режим отладки**.</span><span class="sxs-lookup"><span data-stu-id="43525-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="43525-184">c.</span><span class="sxs-lookup"><span data-stu-id="43525-184">c.</span></span> <span data-ttu-id="43525-185">В hello **издателя** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="43525-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="43525-186">d.</span><span class="sxs-lookup"><span data-stu-id="43525-186">d.</span></span> <span data-ttu-id="43525-187">В hello **URL-адрес запроса Authn** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="43525-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="43525-188">д.</span><span class="sxs-lookup"><span data-stu-id="43525-188">e.</span></span> <span data-ttu-id="43525-189">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте весь сертификат в hello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="43525-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="43525-190">f.</span><span class="sxs-lookup"><span data-stu-id="43525-190">f.</span></span> <span data-ttu-id="43525-191">В поле **Email Attribute** (Атрибут электронной почты) задайте значение **Use SAML subject** (Использовать субъект SAML).</span><span class="sxs-lookup"><span data-stu-id="43525-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="43525-192">g.</span><span class="sxs-lookup"><span data-stu-id="43525-192">g.</span></span> <span data-ttu-id="43525-193">Выберите пункт **Конфигурация входа, инициируемая поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="43525-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="43525-194">h.</span><span class="sxs-lookup"><span data-stu-id="43525-194">h.</span></span> <span data-ttu-id="43525-195">В hello **путь входа** введите **Azure** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="43525-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="43525-196">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="43525-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="43525-197">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="43525-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="43525-198">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="43525-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43525-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="43525-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="43525-200">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="43525-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="43525-202">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43525-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="43525-203">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="43525-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43525-205">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="43525-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43525-207">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="43525-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43525-209">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="43525-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43525-211">а.</span><span class="sxs-lookup"><span data-stu-id="43525-211">a.</span></span> <span data-ttu-id="43525-212">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43525-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43525-213">b.</span><span class="sxs-lookup"><span data-stu-id="43525-213">b.</span></span> <span data-ttu-id="43525-214">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43525-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43525-215">c.</span><span class="sxs-lookup"><span data-stu-id="43525-215">c.</span></span> <span data-ttu-id="43525-216">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="43525-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="43525-217">d.</span><span class="sxs-lookup"><span data-stu-id="43525-217">d.</span></span> <span data-ttu-id="43525-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="43525-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="43525-219">Создание тестового пользователя SumoLogic</span><span class="sxs-lookup"><span data-stu-id="43525-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="43525-220">В порядке tooenable toolog пользователей Azure AD в tooSumoLogic они должны быть подготовленных tooSumoLogic.</span><span class="sxs-lookup"><span data-stu-id="43525-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="43525-221">В случае SumoLogic hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="43525-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="43525-222">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43525-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="43525-223">Войдите в tooyour **SumoLogic** клиента.</span><span class="sxs-lookup"><span data-stu-id="43525-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="43525-224">Go слишком**управление \> пользователей**.</span><span class="sxs-lookup"><span data-stu-id="43525-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="43525-225">![Пользователи](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="43525-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="43525-226">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="43525-226">Click **Add**.</span></span>
   
    <span data-ttu-id="43525-227">![Пользователи](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="43525-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="43525-228">На hello **нового пользователя** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="43525-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="43525-229">![Новый пользователь](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="43525-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="43525-230">а.</span><span class="sxs-lookup"><span data-stu-id="43525-230">a.</span></span> <span data-ttu-id="43525-231">Тип hello связанные данные для учетной записи hello Azure AD, которые должны tooprovision hello **имя**, **Фамилия**, и **электронной почты** текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="43525-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="43525-232">b.</span><span class="sxs-lookup"><span data-stu-id="43525-232">b.</span></span> <span data-ttu-id="43525-233">Выберите роль.</span><span class="sxs-lookup"><span data-stu-id="43525-233">Select a role.</span></span>
  
    <span data-ttu-id="43525-234">c.</span><span class="sxs-lookup"><span data-stu-id="43525-234">c.</span></span> <span data-ttu-id="43525-235">Для параметра **Status** (Состояние) выберите значение **Active** (Активно).</span><span class="sxs-lookup"><span data-stu-id="43525-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="43525-236">d.</span><span class="sxs-lookup"><span data-stu-id="43525-236">d.</span></span> <span data-ttu-id="43525-237">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="43525-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="43525-238">Можно использовать любые другие SumoLogic пользователя средства создания учетных записей или API, предоставленные SumoLogic tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="43525-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="43525-239">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="43525-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="43525-240">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSumoLogic доступа.</span><span class="sxs-lookup"><span data-stu-id="43525-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="43525-242">**tooassign tooSumoLogic Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="43525-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="43525-243">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="43525-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="43525-245">В списке приложений hello выберите **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="43525-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="43525-247">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="43525-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="43525-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="43525-249">Click **Add** button.</span></span> <span data-ttu-id="43525-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="43525-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="43525-252">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="43525-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="43525-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="43525-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43525-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="43525-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43525-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="43525-255">Testing single sign-on</span></span>

<span data-ttu-id="43525-256">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="43525-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="43525-257">При нажатии кнопки hello SumoLogic плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="43525-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43525-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="43525-258">Additional resources</span></span>

* [<span data-ttu-id="43525-259">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43525-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43525-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43525-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

