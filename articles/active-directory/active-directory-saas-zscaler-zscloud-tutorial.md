---
title: "Руководство по интеграции Azure Active Directory с Zscaler ZSCloud | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="4a041-103">Руководство. Интеграция Azure Active Directory с Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="4a041-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="4a041-104">В этом учебнике вы узнаете, как toointegrate Zscaler ZSCloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a041-104">In this tutorial, you learn how toointegrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a041-105">Интеграция Zscaler ZSCloud с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4a041-105">Integrating Zscaler ZSCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a041-106">Можно управлять в Azure AD, имеющего доступ tooZscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="4a041-106">You can control in Azure AD who has access tooZscaler ZSCloud</span></span>
- <span data-ttu-id="4a041-107">Можно включить на пользователей tooautomatically get вошедшего tooZscaler ZSCloud (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a041-107">You can enable your users tooautomatically get signed-on tooZscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a041-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4a041-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4a041-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a041-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a041-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4a041-110">Prerequisites</span></span>

<span data-ttu-id="4a041-111">tooconfigure интеграция Azure AD с Zscaler ZSCloud, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4a041-111">tooconfigure Azure AD integration with Zscaler ZSCloud, you need hello following items:</span></span>

- <span data-ttu-id="4a041-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4a041-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a041-113">подписка с поддержкой единого входа Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a041-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a041-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4a041-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a041-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="4a041-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a041-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4a041-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a041-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a041-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a041-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4a041-118">Scenario description</span></span>
<span data-ttu-id="4a041-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4a041-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a041-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="4a041-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a041-121">Добавление Zscaler ZSCloud из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4a041-121">Adding Zscaler ZSCloud from hello gallery</span></span>
2. <span data-ttu-id="4a041-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a041-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a><span data-ttu-id="4a041-123">Добавление Zscaler ZSCloud из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4a041-123">Adding Zscaler ZSCloud from hello gallery</span></span>
<span data-ttu-id="4a041-124">tooconfigure hello интеграции Zscaler ZSCloud в Azure AD, вы должны tooadd Zscaler ZSCloud из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4a041-124">tooconfigure hello integration of Zscaler ZSCloud into Azure AD, you need tooadd Zscaler ZSCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a041-125">**tooadd Zscaler ZSCloud из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4a041-125">**tooadd Zscaler ZSCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a041-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4a041-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4a041-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="4a041-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4a041-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4a041-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4a041-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4a041-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4a041-133">Введите в поле поиска hello **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="4a041-133">In hello search box, type **Zscaler ZSCloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="4a041-135">В панели результатов hello выберите **Zscaler ZSCloud**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4a041-135">In hello results panel, select **Zscaler ZSCloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a041-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a041-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a041-138">Этот раздел описывает настройку и проверку единого входа Azure AD в Zscaler ZSCloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a041-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4a041-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Zscaler ZSCloud является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a041-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler ZSCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="4a041-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Zscaler ZSCloud должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="4a041-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler ZSCloud needs toobe established.</span></span>

<span data-ttu-id="4a041-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a041-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="4a041-142">tooconfigure и теста Azure AD единого входа с Zscaler ZSCloud, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4a041-142">tooconfigure and test Azure AD single sign-on with Zscaler ZSCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4a041-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="4a041-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4a041-144">**[Настройка параметров прокси-сервера](#configuring-proxy-settings)**  -tooconfigure hello параметров прокси-сервера обозревателя Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="4a041-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="4a041-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="4a041-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a041-146">**[Создание тестового пользователя Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave аналог Саймон Britta в Zscaler ZSCloud, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="4a041-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - toohave a counterpart of Britta Simon in Zscaler ZSCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a041-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="4a041-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a041-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4a041-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a041-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a041-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a041-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a041-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="4a041-151">**tooconfigure Azure AD единого входа с Zscaler ZSCloud, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4a041-151">**tooconfigure Azure AD single sign-on with Zscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a041-152">В hello в hello портала Azure **Zscaler ZSCloud** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4a041-152">In hello Azure portal, on hello **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4a041-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="4a041-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="4a041-156">На hello **Zscaler ZSCloud доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4a041-156">On hello **Zscaler ZSCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="4a041-158">В hello **URL-адрес входа** textbox hello введите URL-адрес, используемый вашей пользователей на toosign tooyour ZScaler ZSCloud приложения.</span><span class="sxs-lookup"><span data-stu-id="4a041-158">In hello **Sign-on URL** textbox, type hello URL used by your users toosign-on tooyour ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4a041-159">Имеется tooupdate это значение с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="4a041-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4a041-160">Обратитесь к [группы поддержки Zscaler ZSCloud клиента](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="4a041-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget this value.</span></span> 
 
4. <span data-ttu-id="4a041-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4a041-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="4a041-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4a041-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a041-165">На hello **Zscaler ZSCloud конфигурации** щелкните **Настройка Zscaler ZSCloud** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="4a041-165">On hello **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4a041-166">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="4a041-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="4a041-168">В другом окне браузера войдите в tooyour сайт ZScaler ZSCloud компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="4a041-168">In a different web browser window, log in tooyour ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="4a041-169">В меню в верхней части hello hello выберите **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="4a041-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="4a041-170">![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="4a041-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="4a041-171">В разделе **Manage Administrators & Roles** (Управление администраторами и ролями) щелкните **Manage Users & Authentication** (Управление пользователями и проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="4a041-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="4a041-172">![Управление пользователями и проверкой подлинности](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Управление пользователями и проверкой подлинности")</span><span class="sxs-lookup"><span data-stu-id="4a041-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="4a041-173">В hello **Выбор параметров проверки подлинности для вашей организации** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4a041-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="4a041-174">![Аутентификация](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="4a041-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="4a041-175">а.</span><span class="sxs-lookup"><span data-stu-id="4a041-175">a.</span></span> <span data-ttu-id="4a041-176">Выберите параметр **Проверка подлинности с помощью единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="4a041-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="4a041-177">b.</span><span class="sxs-lookup"><span data-stu-id="4a041-177">b.</span></span> <span data-ttu-id="4a041-178">Щелкните **Настроить параметры единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="4a041-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="4a041-179">На hello **SAML единого входа параметры настройки** странице диалогового окна, выполните следующие шаги hello и нажмите кнопку **сделать**</span><span class="sxs-lookup"><span data-stu-id="4a041-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="4a041-180">![Единый вход](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="4a041-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="4a041-181">а.</span><span class="sxs-lookup"><span data-stu-id="4a041-181">a.</span></span> <span data-ttu-id="4a041-182">Вставить hello **SAML единого входа URL-адрес службы** значение в hello **URL-адрес hello портала SAML toowhich пользователей будет отправлено для проверки подлинности** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="4a041-182">Paste hello **SAML Single Sign-On Service URL** value into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="4a041-183">b.</span><span class="sxs-lookup"><span data-stu-id="4a041-183">b.</span></span> <span data-ttu-id="4a041-184">В hello **атрибут, содержащий имя входа** введите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="4a041-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="4a041-185">c.</span><span class="sxs-lookup"><span data-stu-id="4a041-185">c.</span></span> <span data-ttu-id="4a041-186">tooupload загруженный сертификат, нажмите кнопку **PEM-файл Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="4a041-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="4a041-187">d.</span><span class="sxs-lookup"><span data-stu-id="4a041-187">d.</span></span> <span data-ttu-id="4a041-188">Выберите параметр **Включить автоматическую подготовку SAML**.</span><span class="sxs-lookup"><span data-stu-id="4a041-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="4a041-189">На hello **Настройка проверки подлинности пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4a041-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="4a041-190">![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="4a041-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="4a041-191">а.</span><span class="sxs-lookup"><span data-stu-id="4a041-191">a.</span></span> <span data-ttu-id="4a041-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4a041-192">Click **Save**.</span></span>

    <span data-ttu-id="4a041-193">b.</span><span class="sxs-lookup"><span data-stu-id="4a041-193">b.</span></span> <span data-ttu-id="4a041-194">Щелкните **Активировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="4a041-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="4a041-195">Настройка параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="4a041-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="4a041-196">параметры прокси-сервера tooconfigure hello в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="4a041-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="4a041-197">Запустите **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4a041-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="4a041-198">Выберите **обозревателя** из hello **средства** меню откройте hello **обозревателя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4a041-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="4a041-199">![Свойства браузера](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Свойства браузера")</span><span class="sxs-lookup"><span data-stu-id="4a041-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="4a041-200">Нажмите кнопку hello **подключений** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4a041-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="4a041-201">![Подключения](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Подключения")</span><span class="sxs-lookup"><span data-stu-id="4a041-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="4a041-202">Нажмите кнопку **параметры локальной сети** tooopen hello **параметры локальной сети** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4a041-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="4a041-203">В hello раздела прокси-сервера выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="4a041-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="4a041-204">![Прокси-сервер](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Прокси-сервер")</span><span class="sxs-lookup"><span data-stu-id="4a041-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="4a041-205">а.</span><span class="sxs-lookup"><span data-stu-id="4a041-205">a.</span></span> <span data-ttu-id="4a041-206">Установите флажок **Использовать прокси-сервер для локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="4a041-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="4a041-207">b.</span><span class="sxs-lookup"><span data-stu-id="4a041-207">b.</span></span> <span data-ttu-id="4a041-208">Введите в текстовое поле адрес hello **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="4a041-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="4a041-209">c.</span><span class="sxs-lookup"><span data-stu-id="4a041-209">c.</span></span> <span data-ttu-id="4a041-210">Введите в текстовое поле hello порт **80**.</span><span class="sxs-lookup"><span data-stu-id="4a041-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="4a041-211">d.</span><span class="sxs-lookup"><span data-stu-id="4a041-211">d.</span></span> <span data-ttu-id="4a041-212">Установите флаг **Не использовать прокси-сервер для локальных адресов**.</span><span class="sxs-lookup"><span data-stu-id="4a041-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="4a041-213">д.</span><span class="sxs-lookup"><span data-stu-id="4a041-213">e.</span></span> <span data-ttu-id="4a041-214">Нажмите кнопку **ОК** tooclose hello **параметры локальной сети (LAN)** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4a041-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="4a041-215">Нажмите кнопку **ОК** tooclose hello **обозревателя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4a041-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a041-216">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a041-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a041-217">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4a041-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4a041-219">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4a041-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a041-220">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4a041-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a041-222">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4a041-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a041-224">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="4a041-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a041-226">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4a041-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a041-228">а.</span><span class="sxs-lookup"><span data-stu-id="4a041-228">a.</span></span> <span data-ttu-id="4a041-229">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a041-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a041-230">b.</span><span class="sxs-lookup"><span data-stu-id="4a041-230">b.</span></span> <span data-ttu-id="4a041-231">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a041-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a041-232">c.</span><span class="sxs-lookup"><span data-stu-id="4a041-232">c.</span></span> <span data-ttu-id="4a041-233">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="4a041-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4a041-234">d.</span><span class="sxs-lookup"><span data-stu-id="4a041-234">d.</span></span> <span data-ttu-id="4a041-235">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4a041-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="4a041-236">Создание тестового пользователя Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="4a041-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="4a041-237">Пользователи toolog tooenable Azure AD в tooZScaler ZSCloud, они должны быть подготовленных tooZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a041-237">tooenable Azure AD users toolog in tooZScaler ZSCloud, they must be provisioned tooZScaler ZSCloud.</span></span>  
<span data-ttu-id="4a041-238">В случае ZScaler ZSCloud hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="4a041-238">In hello case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="4a041-239">tooconfigure подготовки пользователей, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="4a041-239">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="4a041-240">Войдите в tooyour **Zscaler** клиента.</span><span class="sxs-lookup"><span data-stu-id="4a041-240">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="4a041-241">Щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="4a041-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="4a041-242">![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="4a041-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="4a041-243">Щелкните **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="4a041-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="4a041-244">![Добавление](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="4a041-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="4a041-245">В hello **пользователей** щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="4a041-245">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="4a041-246">![Добавление](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="4a041-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="4a041-247">В hello раздел добавить пользователя выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="4a041-247">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="4a041-248">![Добавление пользователя](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="4a041-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="4a041-249">а.</span><span class="sxs-lookup"><span data-stu-id="4a041-249">a.</span></span> <span data-ttu-id="4a041-250">Hello тип **UserID**, **отображаемое имя пользователя**, **пароль**, **подтверждение пароля**, а затем выберите **группы**и hello **отдел** действительной учетной записи AAD, вы хотите tooprovision.</span><span class="sxs-lookup"><span data-stu-id="4a041-250">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="4a041-251">b.</span><span class="sxs-lookup"><span data-stu-id="4a041-251">b.</span></span> <span data-ttu-id="4a041-252">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4a041-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="4a041-253">Можно использовать любые другие ZScaler ZSCloud пользователя средства создания учетных записей или интерфейсы API, предоставляемые ZScaler ZSCloud tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="4a041-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4a041-254">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="4a041-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4a041-255">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooZscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a041-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler ZSCloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4a041-257">**tooassign Britta Simon tooZscaler ZSCloud, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4a041-257">**tooassign Britta Simon tooZscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a041-258">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4a041-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4a041-260">В списке приложений hello выберите **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="4a041-260">In hello applications list, select **Zscaler ZSCloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="4a041-262">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="4a041-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4a041-264">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4a041-264">Click **Add** button.</span></span> <span data-ttu-id="4a041-265">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4a041-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4a041-267">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="4a041-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4a041-268">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4a041-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a041-269">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4a041-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a041-270">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4a041-270">Testing single sign-on</span></span>

<span data-ttu-id="4a041-271">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="4a041-271">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>

<span data-ttu-id="4a041-272">При нажатии кнопки Zscaler ZSCloud плитки в панели доступа hello hello, вы должны получить tooyour автоматически подписан в приложение Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a041-272">When you click hello Zscaler ZSCloud tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler ZSCloud application.</span></span>

<span data-ttu-id="4a041-273">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a041-273">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4a041-274">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4a041-274">Additional resources</span></span>

* [<span data-ttu-id="4a041-275">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a041-275">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a041-276">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a041-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

