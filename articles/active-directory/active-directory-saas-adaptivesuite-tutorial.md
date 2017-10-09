---
title: "Руководство по интеграции Azure Active Directory с Adaptive Suite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и адаптивной Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="10c79-103">Руководство. Интеграция Azure Active Directory с Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="10c79-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="10c79-104">В этом учебнике вы узнаете, как toointegrate адаптивной Suite с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="10c79-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10c79-105">Интеграция с Azure AD адаптивной Suite предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="10c79-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="10c79-106">Можно управлять в Azure AD, имеющего доступ tooAdaptive Suite</span><span class="sxs-lookup"><span data-stu-id="10c79-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="10c79-107">Можно включить на пользователей tooautomatically get вошедшего tooAdaptive набора (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="10c79-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="10c79-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="10c79-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="10c79-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="10c79-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10c79-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="10c79-110">Prerequisites</span></span>

<span data-ttu-id="10c79-111">tooconfigure интеграция Azure AD с адаптивной Suite необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="10c79-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="10c79-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="10c79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10c79-113">подписка Adaptive Suite с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="10c79-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10c79-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="10c79-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10c79-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="10c79-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10c79-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="10c79-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="10c79-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="10c79-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10c79-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="10c79-118">Scenario description</span></span>
<span data-ttu-id="10c79-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="10c79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10c79-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="10c79-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10c79-121">Добавление адаптивной набор из галереи hello</span><span class="sxs-lookup"><span data-stu-id="10c79-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="10c79-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="10c79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="10c79-123">Добавление адаптивной набор из галереи hello</span><span class="sxs-lookup"><span data-stu-id="10c79-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="10c79-124">tooconfigure hello интеграции адаптивной Suite в Azure AD, вы должны tooadd адаптивной набор из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="10c79-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="10c79-125">**tooadd адаптивной набор из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="10c79-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="10c79-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="10c79-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="10c79-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="10c79-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="10c79-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="10c79-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="10c79-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="10c79-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="10c79-133">Введите в поле поиска hello **адаптивной Suite**.</span><span class="sxs-lookup"><span data-stu-id="10c79-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="10c79-135">В панели результатов hello выберите **адаптивной Suite**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="10c79-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="10c79-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="10c79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="10c79-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Adaptive Suite с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10c79-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="10c79-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в адаптивной Suite является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10c79-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="10c79-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в адаптивной Suite должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="10c79-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="10c79-141">Адаптивная пакета, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="10c79-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="10c79-142">tooconfigure и теста Azure AD единого входа с адаптивной Suite, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="10c79-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="10c79-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="10c79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="10c79-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="10c79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10c79-145">**[Создание тестового пользователя, прошедшего адаптивной Suite](#creating-an-adaptive-suite-test-user)**  -toohave аналог Саймон Britta адаптивной набора, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="10c79-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="10c79-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="10c79-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10c79-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="10c79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="10c79-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="10c79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="10c79-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении адаптивной Suite.</span><span class="sxs-lookup"><span data-stu-id="10c79-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="10c79-150">**tooconfigure Azure AD единого входа с адаптивной Suite выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="10c79-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="10c79-151">В hello в hello портала Azure **адаптивной Suite** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="10c79-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="10c79-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="10c79-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="10c79-155">На hello **URL-адреса и домена адаптивной Suite** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="10c79-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="10c79-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="10c79-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="10c79-158">Это значение можно получить из hello адаптивной Suite **настройки единого входа SAML** страницы.</span><span class="sxs-lookup"><span data-stu-id="10c79-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="10c79-159">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="10c79-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="10c79-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="10c79-161">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="10c79-163">На hello **адаптивной настройку пакета** щелкните **настройки адаптивной Suite** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="10c79-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="10c79-164">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="10c79-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="10c79-166">В другом окне браузера Войдите на сайте компании tooyour адаптивной Suite в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="10c79-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="10c79-167">Go слишком**администратора**.</span><span class="sxs-lookup"><span data-stu-id="10c79-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="10c79-168">![Администратор](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="10c79-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="10c79-169">В hello **пользователям и ролям** щелкните **Управление параметрами единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="10c79-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="10c79-170">![Управление параметрами единого входа SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Управление параметрами единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="10c79-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="10c79-171">На hello **настройки единого входа SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="10c79-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="10c79-172">![Параметры единого входа SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="10c79-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="10c79-173">а.</span><span class="sxs-lookup"><span data-stu-id="10c79-173">a.</span></span> <span data-ttu-id="10c79-174">В hello **имя поставщика удостоверений** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="10c79-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="10c79-175">b.</span><span class="sxs-lookup"><span data-stu-id="10c79-175">b.</span></span> <span data-ttu-id="10c79-176">Вставить hello **идентификатор сущности SAML** значение копируется из портала Azure hello **поставщика удостоверений идентификатор сущности** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="10c79-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="10c79-177">c.</span><span class="sxs-lookup"><span data-stu-id="10c79-177">c.</span></span> <span data-ttu-id="10c79-178">Вставить hello **SAML единого входа URL-адрес службы** значение копируется из портала Azure hello **поставщика удостоверений URL-адрес SSO** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="10c79-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="10c79-179">d.</span><span class="sxs-lookup"><span data-stu-id="10c79-179">d.</span></span> <span data-ttu-id="10c79-180">Вставить hello **SAML единого входа URL-адрес службы** значение копируется из портала Azure hello **URL-адрес выхода Custom** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="10c79-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="10c79-181">д.</span><span class="sxs-lookup"><span data-stu-id="10c79-181">e.</span></span> <span data-ttu-id="10c79-182">tooupload загруженный сертификат, нажмите кнопку **выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="10c79-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="10c79-183">f.</span><span class="sxs-lookup"><span data-stu-id="10c79-183">f.</span></span> <span data-ttu-id="10c79-184">Выберите следующие hello для:</span><span class="sxs-lookup"><span data-stu-id="10c79-184">Select hello following, for:</span></span>
    * <span data-ttu-id="10c79-185">Для параметра **SAML user id** (Идентификатор пользователя SAML) выберите значение **User’s Adaptive Insights user name** (Имя пользователя Adaptive Insights).</span><span class="sxs-lookup"><span data-stu-id="10c79-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="10c79-186">Для параметра **SAML user id location** (Расположение идентификатора пользователя SAML) выберите значение **User id in NameID of Subject** (Идентификатор пользователя из NameID в Subject).</span><span class="sxs-lookup"><span data-stu-id="10c79-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="10c79-187">Для параметра **SAML NameID format** (Формат NameID SAML) выберите значение **Адрес электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="10c79-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="10c79-188">Для параметра **Включить SAML** выберите значение **Allow SAML SSO and direct Adaptive Insights login** (Разрешить единый вход SAML и прямой вход Adaptive Insights).</span><span class="sxs-lookup"><span data-stu-id="10c79-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="10c79-189">g.</span><span class="sxs-lookup"><span data-stu-id="10c79-189">g.</span></span> <span data-ttu-id="10c79-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="10c79-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="10c79-191">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="10c79-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="10c79-192">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="10c79-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="10c79-193">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10c79-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="10c79-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="10c79-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="10c79-195">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="10c79-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="10c79-197">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="10c79-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="10c79-198">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="10c79-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="10c79-200">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="10c79-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="10c79-202">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="10c79-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="10c79-204">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="10c79-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="10c79-206">а.</span><span class="sxs-lookup"><span data-stu-id="10c79-206">a.</span></span> <span data-ttu-id="10c79-207">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="10c79-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="10c79-208">b.</span><span class="sxs-lookup"><span data-stu-id="10c79-208">b.</span></span> <span data-ttu-id="10c79-209">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="10c79-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="10c79-210">c.</span><span class="sxs-lookup"><span data-stu-id="10c79-210">c.</span></span> <span data-ttu-id="10c79-211">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="10c79-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="10c79-212">d.</span><span class="sxs-lookup"><span data-stu-id="10c79-212">d.</span></span> <span data-ttu-id="10c79-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="10c79-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="10c79-214">Создание тестового пользователя Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="10c79-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="10c79-215">Пользователи toolog tooenable Azure AD в tooAdaptive Suite, их необходимо подготовить в адаптивной набор.</span><span class="sxs-lookup"><span data-stu-id="10c79-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="10c79-216">В случае hello адаптивной набора Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="10c79-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="10c79-217">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="10c79-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="10c79-218">Войдите в tooyour **адаптивной Suite** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="10c79-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="10c79-219">Go слишком**администратора**.</span><span class="sxs-lookup"><span data-stu-id="10c79-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="10c79-220">![Администратор](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="10c79-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="10c79-221">В hello **пользователям и ролям** щелкните **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="10c79-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="10c79-222">![Добавление пользователя](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="10c79-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="10c79-223">В hello **нового пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="10c79-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="10c79-224">![Отправка](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Отправка")</span><span class="sxs-lookup"><span data-stu-id="10c79-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="10c79-225">а.</span><span class="sxs-lookup"><span data-stu-id="10c79-225">a.</span></span> <span data-ttu-id="10c79-226">Тип hello **имя**, **входа**, **электронной почты**, **пароль** действительного пользователя Azure Active Directory требуется tooprovision в связанных hello текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="10c79-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="10c79-227">b.</span><span class="sxs-lookup"><span data-stu-id="10c79-227">b.</span></span> <span data-ttu-id="10c79-228">Выберите **Роль**.</span><span class="sxs-lookup"><span data-stu-id="10c79-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="10c79-229">c.</span><span class="sxs-lookup"><span data-stu-id="10c79-229">c.</span></span> <span data-ttu-id="10c79-230">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="10c79-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="10c79-231">Можно использовать любые другие адаптивной Suite пользователя средства создания учетных записей или интерфейсы API, предоставляемые tooprovision адаптивной набора учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="10c79-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="10c79-232">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="10c79-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="10c79-233">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAdaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="10c79-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="10c79-235">**tooassign tooAdaptive Britta Simon Suite, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="10c79-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="10c79-236">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="10c79-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="10c79-238">В списке приложений hello выберите **адаптивной Suite**.</span><span class="sxs-lookup"><span data-stu-id="10c79-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="10c79-240">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="10c79-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="10c79-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="10c79-242">Click **Add** button.</span></span> <span data-ttu-id="10c79-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="10c79-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="10c79-245">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="10c79-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="10c79-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="10c79-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10c79-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="10c79-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="10c79-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="10c79-248">Testing single sign-on</span></span>

<span data-ttu-id="10c79-249">Цель этого раздела Hello является tootest к Microsoft Azure AD Single Sign-On конфигурации с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="10c79-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="10c79-250">При выборе плитки адаптивной Suite hello в hello панели доступа, вы должны получить tooyour автоматически вошедшего адаптивной набора приложений.</span><span class="sxs-lookup"><span data-stu-id="10c79-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="10c79-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="10c79-251">Additional resources</span></span>

* [<span data-ttu-id="10c79-252">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10c79-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10c79-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="10c79-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

