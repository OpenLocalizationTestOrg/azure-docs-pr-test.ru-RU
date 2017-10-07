---
title: "Руководство по интеграции Azure Active Directory с Zscaler Beta | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zscaler Beta."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1471c2b51ca5684a11acd40f4e450521605bb786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="c40ea-103">Руководство по интеграции Azure Active Directory с Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="c40ea-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="c40ea-104">В этом учебнике вы узнаете, как toointegrate Zscaler Beta с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c40ea-104">In this tutorial, you learn how toointegrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c40ea-105">Интеграция Zscaler Beta с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c40ea-105">Integrating Zscaler Beta with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c40ea-106">Можно управлять в Azure AD, имеющего доступ tooZscaler бета-версии</span><span class="sxs-lookup"><span data-stu-id="c40ea-106">You can control in Azure AD who has access tooZscaler Beta</span></span>
- <span data-ttu-id="c40ea-107">Можно включить на пользователей tooautomatically get вошедшего tooZscaler бета-версии (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c40ea-107">You can enable your users tooautomatically get signed-on tooZscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c40ea-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c40ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c40ea-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c40ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c40ea-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c40ea-110">Prerequisites</span></span>

<span data-ttu-id="c40ea-111">tooconfigure интеграция Azure AD с Zscaler Beta, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c40ea-111">tooconfigure Azure AD integration with Zscaler Beta, you need hello following items:</span></span>

- <span data-ttu-id="c40ea-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c40ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c40ea-113">подписка Zscaler Beta с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c40ea-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c40ea-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c40ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c40ea-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c40ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c40ea-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c40ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c40ea-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c40ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c40ea-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c40ea-118">Scenario description</span></span>
<span data-ttu-id="c40ea-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c40ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c40ea-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c40ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c40ea-121">Добавление Zscaler Beta из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c40ea-121">Adding Zscaler Beta from hello gallery</span></span>
2. <span data-ttu-id="c40ea-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c40ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-hello-gallery"></a><span data-ttu-id="c40ea-123">Добавление Zscaler Beta из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c40ea-123">Adding Zscaler Beta from hello gallery</span></span>
<span data-ttu-id="c40ea-124">tooconfigure hello интеграции Zscaler Beta в Azure AD, вы должны tooadd Zscaler Beta из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c40ea-124">tooconfigure hello integration of Zscaler Beta into Azure AD, you need tooadd Zscaler Beta from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c40ea-125">**tooadd Zscaler Beta из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c40ea-125">**tooadd Zscaler Beta from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c40ea-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c40ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c40ea-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c40ea-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c40ea-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c40ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c40ea-133">Введите в поле поиска hello **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-133">In hello search box, type **Zscaler Beta**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. <span data-ttu-id="c40ea-135">В панели результатов hello выберите **Zscaler Beta**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c40ea-135">In hello results panel, select **Zscaler Beta**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c40ea-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c40ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c40ea-138">В этом разделе описана настройка и проверка единого входа Azure AD в Zscaler Beta с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c40ea-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c40ea-139">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в Zscaler Beta — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c40ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Beta is tooa user in Azure AD.</span></span> <span data-ttu-id="c40ea-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Zscaler Beta должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c40ea-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Beta needs toobe established.</span></span>

<span data-ttu-id="c40ea-141">В Zscaler Beta, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c40ea-141">In Zscaler Beta, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c40ea-142">tooconfigure и теста Azure AD единого входа с Zscaler Beta, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c40ea-142">tooconfigure and test Azure AD single sign-on with Zscaler Beta, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c40ea-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c40ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c40ea-144">**[Настройка параметров прокси-сервера](#configuring-proxy-settings)**  -tooconfigure hello параметров прокси-сервера обозревателя Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c40ea-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="c40ea-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c40ea-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="c40ea-146">**[Создание тестового пользователя Zscaler Beta](#creating-a-zscaler-beta-test-user)**  -toohave аналог Саймон Britta в Zscaler Beta, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c40ea-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - toohave a counterpart of Britta Simon in Zscaler Beta that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="c40ea-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c40ea-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="c40ea-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c40ea-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c40ea-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c40ea-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c40ea-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="c40ea-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="c40ea-151">**tooconfigure Azure AD единого входа с Zscaler Beta, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c40ea-151">**tooconfigure Azure AD single sign-on with Zscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="c40ea-152">В hello в hello портала Azure **Zscaler Beta** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-152">In hello Azure portal, on hello **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c40ea-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c40ea-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. <span data-ttu-id="c40ea-156">На hello **Zscaler Beta доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c40ea-156">On hello **Zscaler Beta Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="c40ea-158">В текстовом поле URL-адрес hello вход введите hello URL-адреса, используемые вашей пользователей на toosign tooyour приложение Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="c40ea-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c40ea-159">Имеется tooupdate это значение с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="c40ea-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c40ea-160">Обратитесь к [группы поддержки Zscaler бета-версии клиента](https://www.zscaler.com/company/contact) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="c40ea-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="c40ea-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c40ea-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. <span data-ttu-id="c40ea-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c40ea-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c40ea-165">На hello **Zscaler Beta конфигурации** щелкните **Настройка Zscaler Beta** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c40ea-165">On hello **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c40ea-166">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c40ea-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. <span data-ttu-id="c40ea-168">В другом окне браузера войдите в tooyour сайт Zscaler Beta компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c40ea-168">In a different web browser window, log in tooyour Zscaler Beta company site as an administrator.</span></span>

8. <span data-ttu-id="c40ea-169">В меню в верхней части hello hello выберите **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="c40ea-170">![Администрирование](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="c40ea-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="c40ea-171">В разделе **Manage Administrators & Roles** (Управление администраторами и ролями) щелкните **Manage Users & Authentication** (Управление пользователями и проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="c40ea-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="c40ea-172">![Управление пользователями и проверкой подлинности](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Управление пользователями и проверкой подлинности")</span><span class="sxs-lookup"><span data-stu-id="c40ea-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="c40ea-173">В hello **Выбор параметров проверки подлинности для вашей организации** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c40ea-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="c40ea-174">![Аутентификация](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="c40ea-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="c40ea-175">а.</span><span class="sxs-lookup"><span data-stu-id="c40ea-175">a.</span></span> <span data-ttu-id="c40ea-176">Выберите параметр **Проверка подлинности с помощью единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="c40ea-177">b.</span><span class="sxs-lookup"><span data-stu-id="c40ea-177">b.</span></span> <span data-ttu-id="c40ea-178">Щелкните **Настроить параметры единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="c40ea-179">На hello **SAML единого входа параметры настройки** странице диалогового окна, выполните следующие шаги hello и нажмите кнопку **сделать**</span><span class="sxs-lookup"><span data-stu-id="c40ea-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="c40ea-180">![Единый вход](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="c40ea-180">![Single Sign-On](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="c40ea-181">а.</span><span class="sxs-lookup"><span data-stu-id="c40ea-181">a.</span></span> <span data-ttu-id="c40ea-182">Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес hello портала SAML toowhich пользователей будет отправлено для проверки подлинности** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="c40ea-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="c40ea-183">b.</span><span class="sxs-lookup"><span data-stu-id="c40ea-183">b.</span></span> <span data-ttu-id="c40ea-184">В hello **атрибут, содержащий имя входа** введите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="c40ea-185">c.</span><span class="sxs-lookup"><span data-stu-id="c40ea-185">c.</span></span> <span data-ttu-id="c40ea-186">tooupload загруженный сертификат, нажмите кнопку **PEM-файл Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="c40ea-187">d.</span><span class="sxs-lookup"><span data-stu-id="c40ea-187">d.</span></span> <span data-ttu-id="c40ea-188">Выберите параметр **Включить автоматическую подготовку SAML**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="c40ea-189">На hello **Настройка проверки подлинности пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c40ea-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="c40ea-190">![Администрирование](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="c40ea-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="c40ea-191">а.</span><span class="sxs-lookup"><span data-stu-id="c40ea-191">a.</span></span> <span data-ttu-id="c40ea-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-192">Click **Save**.</span></span>

    <span data-ttu-id="c40ea-193">b.</span><span class="sxs-lookup"><span data-stu-id="c40ea-193">b.</span></span> <span data-ttu-id="c40ea-194">Щелкните **Активировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="c40ea-195">Настройка параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="c40ea-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="c40ea-196">параметры прокси-сервера tooconfigure hello в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c40ea-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="c40ea-197">Запустите **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="c40ea-198">Выберите **обозревателя** из hello **средства** меню откройте hello **обозревателя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c40ea-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="c40ea-199">![Свойства браузера](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Свойства браузера")</span><span class="sxs-lookup"><span data-stu-id="c40ea-199">![Internet Options](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="c40ea-200">Нажмите кнопку hello **подключений** вкладки.</span><span class="sxs-lookup"><span data-stu-id="c40ea-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="c40ea-201">![Подключения](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Подключения")</span><span class="sxs-lookup"><span data-stu-id="c40ea-201">![Connections](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="c40ea-202">Нажмите кнопку **параметры локальной сети** tooopen hello **параметры локальной сети** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c40ea-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="c40ea-203">В hello раздела прокси-сервера выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c40ea-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="c40ea-204">![Прокси-сервер](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Прокси-сервер")</span><span class="sxs-lookup"><span data-stu-id="c40ea-204">![Proxy server](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="c40ea-205">а.</span><span class="sxs-lookup"><span data-stu-id="c40ea-205">a.</span></span> <span data-ttu-id="c40ea-206">Установите флажок **Использовать прокси-сервер для локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="c40ea-207">b.</span><span class="sxs-lookup"><span data-stu-id="c40ea-207">b.</span></span> <span data-ttu-id="c40ea-208">Введите в текстовое поле адрес hello **gateway.zscalerbeta.net**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-208">In hello Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="c40ea-209">c.</span><span class="sxs-lookup"><span data-stu-id="c40ea-209">c.</span></span> <span data-ttu-id="c40ea-210">Введите в текстовое поле hello порт **80**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="c40ea-211">d.</span><span class="sxs-lookup"><span data-stu-id="c40ea-211">d.</span></span> <span data-ttu-id="c40ea-212">Установите флаг **Не использовать прокси-сервер для локальных адресов**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="c40ea-213">д.</span><span class="sxs-lookup"><span data-stu-id="c40ea-213">e.</span></span> <span data-ttu-id="c40ea-214">Нажмите кнопку **ОК** tooclose hello **параметры локальной сети (LAN)** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c40ea-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="c40ea-215">Нажмите кнопку **ОК** tooclose hello **обозревателя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c40ea-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="c40ea-216">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c40ea-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c40ea-217">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c40ea-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c40ea-218">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c40ea-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c40ea-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c40ea-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="c40ea-220">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c40ea-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c40ea-222">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c40ea-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c40ea-223">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c40ea-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c40ea-225">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c40ea-227">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c40ea-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c40ea-229">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c40ea-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c40ea-231">а.</span><span class="sxs-lookup"><span data-stu-id="c40ea-231">a.</span></span> <span data-ttu-id="c40ea-232">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c40ea-233">b.</span><span class="sxs-lookup"><span data-stu-id="c40ea-233">b.</span></span> <span data-ttu-id="c40ea-234">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c40ea-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c40ea-235">c.</span><span class="sxs-lookup"><span data-stu-id="c40ea-235">c.</span></span> <span data-ttu-id="c40ea-236">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c40ea-237">d.</span><span class="sxs-lookup"><span data-stu-id="c40ea-237">d.</span></span> <span data-ttu-id="c40ea-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="c40ea-239">Создание тестового пользователя Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="c40ea-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="c40ea-240">Пользователи toolog tooenable Azure AD в tooZscaler бета-версии, они должны быть подготовленных tooZscaler бета-версии.</span><span class="sxs-lookup"><span data-stu-id="c40ea-240">tooenable Azure AD users toolog in tooZscaler Beta, they must be provisioned tooZscaler Beta.</span></span> <span data-ttu-id="c40ea-241">В случае Zscaler Beta hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="c40ea-241">In hello case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="c40ea-242">tooconfigure подготовки пользователей, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c40ea-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="c40ea-243">Войдите в tooyour **Zscaler Beta** клиента.</span><span class="sxs-lookup"><span data-stu-id="c40ea-243">Log in tooyour **Zscaler Beta** tenant.</span></span>

2. <span data-ttu-id="c40ea-244">Щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="c40ea-245">![Администрирование](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="c40ea-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="c40ea-246">Щелкните **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="c40ea-247">![Добавление](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="c40ea-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="c40ea-248">В hello **пользователей** щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="c40ea-249">![Добавление](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="c40ea-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="c40ea-250">В hello раздел добавить пользователя выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="c40ea-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="c40ea-251">![Добавление пользователя](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="c40ea-251">![Add User](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="c40ea-252">а.</span><span class="sxs-lookup"><span data-stu-id="c40ea-252">a.</span></span> <span data-ttu-id="c40ea-253">Hello тип **UserID**, **отображаемое имя пользователя**, **пароль**, **подтверждение пароля**, а затем выберите **группы**и hello **отдел** из допустимых Azure AD счета, tooprovision.</span><span class="sxs-lookup"><span data-stu-id="c40ea-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="c40ea-254">b.</span><span class="sxs-lookup"><span data-stu-id="c40ea-254">b.</span></span> <span data-ttu-id="c40ea-255">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="c40ea-256">Можно использовать любые другие Zscaler Beta пользователя средства создания учетных записей или интерфейсы API, предоставляемые Zscaler Beta tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c40ea-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c40ea-257">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c40ea-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c40ea-258">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooZscaler бета-версии.</span><span class="sxs-lookup"><span data-stu-id="c40ea-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Beta.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c40ea-260">**tooassign tooZscaler Britta Simon бета-версии, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="c40ea-260">**tooassign Britta Simon tooZscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="c40ea-261">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c40ea-263">В списке приложений hello выберите **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-263">In hello applications list, select **Zscaler Beta**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. <span data-ttu-id="c40ea-265">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c40ea-267">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-267">Click **Add** button.</span></span> <span data-ttu-id="c40ea-268">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c40ea-270">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c40ea-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c40ea-271">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c40ea-272">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c40ea-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c40ea-273">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c40ea-273">Testing single sign-on</span></span>

<span data-ttu-id="c40ea-274">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c40ea-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c40ea-275">При нажатии кнопки Zscaler Beta плитки в панели доступа hello hello, вы должны получить tooyour автоматически подписан в приложение Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="c40ea-275">When you click hello Zscaler Beta tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Beta application.</span></span>
<span data-ttu-id="c40ea-276">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c40ea-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c40ea-277">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c40ea-277">Additional resources</span></span>

* [<span data-ttu-id="c40ea-278">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c40ea-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c40ea-279">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c40ea-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

