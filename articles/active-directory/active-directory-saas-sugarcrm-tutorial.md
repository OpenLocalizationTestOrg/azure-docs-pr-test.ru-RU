---
title: "Руководство по интеграции Azure Active Directory с SugarCRM | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="921b5-103">Руководство по интеграции Azure Active Directory с SugarCRM</span><span class="sxs-lookup"><span data-stu-id="921b5-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="921b5-104">В этом учебнике вы узнаете, как toointegrate Sugar CRM с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="921b5-104">In this tutorial, you learn how toointegrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="921b5-105">Интеграция Sugar CRM с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="921b5-105">Integrating Sugar CRM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="921b5-106">Можно управлять в Azure AD, имеющего доступ tooSugar CRM</span><span class="sxs-lookup"><span data-stu-id="921b5-106">You can control in Azure AD who has access tooSugar CRM</span></span>
- <span data-ttu-id="921b5-107">Можно включить на пользователей tooautomatically get вошедшего tooSugar CRM (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="921b5-107">You can enable your users tooautomatically get signed-on tooSugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="921b5-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="921b5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="921b5-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="921b5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="921b5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="921b5-110">Prerequisites</span></span>

<span data-ttu-id="921b5-111">tooconfigure интеграция Azure AD с Sugar CRM требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="921b5-111">tooconfigure Azure AD integration with Sugar CRM, you need hello following items:</span></span>

- <span data-ttu-id="921b5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="921b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="921b5-113">Подписка SugarCRM с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="921b5-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="921b5-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="921b5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="921b5-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="921b5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="921b5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="921b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="921b5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="921b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="921b5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="921b5-118">Scenario description</span></span>
<span data-ttu-id="921b5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="921b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="921b5-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="921b5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="921b5-121">Добавление Sugar CRM из галереи hello</span><span class="sxs-lookup"><span data-stu-id="921b5-121">Adding Sugar CRM from hello gallery</span></span>
2. <span data-ttu-id="921b5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="921b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-hello-gallery"></a><span data-ttu-id="921b5-123">Добавление Sugar CRM из галереи hello</span><span class="sxs-lookup"><span data-stu-id="921b5-123">Adding Sugar CRM from hello gallery</span></span>
<span data-ttu-id="921b5-124">tooconfigure hello интеграции Sugar CRM в Azure AD, вы должны tooadd Sugar CRM из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="921b5-124">tooconfigure hello integration of Sugar CRM into Azure AD, you need tooadd Sugar CRM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="921b5-125">**tooadd Sugar CRM из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="921b5-125">**tooadd Sugar CRM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="921b5-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="921b5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="921b5-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="921b5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="921b5-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="921b5-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="921b5-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="921b5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="921b5-133">Введите в поле поиска hello **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="921b5-133">In hello search box, type **Sugar CRM**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="921b5-135">В панели результатов hello выберите **Sugar CRM**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="921b5-135">In hello results panel, select **Sugar CRM**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="921b5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="921b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="921b5-138">В этом разделе описана настройка и проверка единого входа Azure AD в SugarCRM с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="921b5-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="921b5-139">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в Sugar CRM — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="921b5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sugar CRM is tooa user in Azure AD.</span></span> <span data-ttu-id="921b5-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Sugar CRM должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="921b5-140">In other words, a link relationship between an Azure AD user and hello related user in Sugar CRM needs toobe established.</span></span>

<span data-ttu-id="921b5-141">В Sugar CRM, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="921b5-141">In Sugar CRM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="921b5-142">tooconfigure и теста Azure AD единого входа с Sugar CRM, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="921b5-142">tooconfigure and test Azure AD single sign-on with Sugar CRM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="921b5-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="921b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="921b5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="921b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="921b5-145">**[Создание тестового пользователя Sugar CRM](#creating-a-sugar-crm-test-user)**  -toohave аналог Саймон Britta в Sugar CRM, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="921b5-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - toohave a counterpart of Britta Simon in Sugar CRM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="921b5-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="921b5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="921b5-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="921b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="921b5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="921b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="921b5-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="921b5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="921b5-150">**tooconfigure Azure AD единого входа с Sugar CRM, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="921b5-150">**tooconfigure Azure AD single sign-on with Sugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="921b5-151">В hello в hello портала Azure **Sugar CRM** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="921b5-151">In hello Azure portal, on hello **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="921b5-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="921b5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="921b5-155">На hello **URL-адреса и домена Sugar CRM** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="921b5-155">On hello **Sugar CRM Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="921b5-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="921b5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="921b5-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="921b5-158">hello value is not real.</span></span> <span data-ttu-id="921b5-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="921b5-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="921b5-160">Обратитесь к [группа поддержки клиент Sugar CRM](https://support.sugarcrm.com/) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="921b5-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="921b5-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="921b5-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="921b5-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="921b5-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="921b5-165">На hello **конфигурации Sugar CRM** щелкните **Настройка Sugar CRM** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="921b5-165">On hello **Sugar CRM Configuration** section, click **Configure Sugar CRM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="921b5-166">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="921b5-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="921b5-168">В другом окне браузера Войдите на сайте компании Sugar CRM tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="921b5-168">In a different web browser window, log in tooyour Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="921b5-169">Go слишком**администратора**.</span><span class="sxs-lookup"><span data-stu-id="921b5-169">Go too**Admin**.</span></span>
   
    <span data-ttu-id="921b5-170">![Администратор](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="921b5-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="921b5-171">В hello **администрирования** щелкните **управления паролями**.</span><span class="sxs-lookup"><span data-stu-id="921b5-171">In hello **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="921b5-172">![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="921b5-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="921b5-173">Установите флажок **Включить проверку подлинности SAML**.</span><span class="sxs-lookup"><span data-stu-id="921b5-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="921b5-174">![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="921b5-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="921b5-175">В hello **проверку подлинности SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="921b5-175">In hello **SAML Authentication** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="921b5-176">![Аутентификация SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Аутентификация SAML")</span><span class="sxs-lookup"><span data-stu-id="921b5-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="921b5-177">а.</span><span class="sxs-lookup"><span data-stu-id="921b5-177">a.</span></span> <span data-ttu-id="921b5-178">В hello **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="921b5-178">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="921b5-179">b.</span><span class="sxs-lookup"><span data-stu-id="921b5-179">b.</span></span> <span data-ttu-id="921b5-180">В hello **URL-адрес SLO** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="921b5-180">In hello **SLO URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="921b5-181">c.</span><span class="sxs-lookup"><span data-stu-id="921b5-181">c.</span></span> <span data-ttu-id="921b5-182">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте весь сертификат в hello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="921b5-182">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="921b5-183">d.</span><span class="sxs-lookup"><span data-stu-id="921b5-183">d.</span></span> <span data-ttu-id="921b5-184">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="921b5-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="921b5-185">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="921b5-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="921b5-186">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="921b5-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="921b5-187">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="921b5-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="921b5-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="921b5-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="921b5-189">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="921b5-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="921b5-191">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="921b5-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="921b5-192">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="921b5-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="921b5-194">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="921b5-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="921b5-196">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="921b5-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="921b5-198">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="921b5-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="921b5-200">а.</span><span class="sxs-lookup"><span data-stu-id="921b5-200">a.</span></span> <span data-ttu-id="921b5-201">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="921b5-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="921b5-202">b.</span><span class="sxs-lookup"><span data-stu-id="921b5-202">b.</span></span> <span data-ttu-id="921b5-203">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="921b5-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="921b5-204">c.</span><span class="sxs-lookup"><span data-stu-id="921b5-204">c.</span></span> <span data-ttu-id="921b5-205">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="921b5-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="921b5-206">d.</span><span class="sxs-lookup"><span data-stu-id="921b5-206">d.</span></span> <span data-ttu-id="921b5-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="921b5-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="921b5-208">Создание тестового пользователя SugarCRM</span><span class="sxs-lookup"><span data-stu-id="921b5-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="921b5-209">В порядке tooenable toolog пользователей Azure AD в tooSugar CRM они должны быть подготовленных tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="921b5-209">In order tooenable Azure AD users toolog in tooSugar CRM, they must be provisioned tooSugar CRM.</span></span>

<span data-ttu-id="921b5-210">В случае hello Sugar CRM Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="921b5-210">In hello case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="921b5-211">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="921b5-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="921b5-212">Войдите в tooyour **Sugar CRM** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="921b5-212">Log in tooyour **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="921b5-213">Go слишком**администратора**.</span><span class="sxs-lookup"><span data-stu-id="921b5-213">Go too**Admin**.</span></span>
   
    <span data-ttu-id="921b5-214">![Администратор](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="921b5-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="921b5-215">В hello **администрирования** щелкните **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="921b5-215">In hello **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="921b5-216">![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="921b5-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="921b5-217">Go слишком**пользователей \> создать нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="921b5-217">Go too**Users \> Create New User**.</span></span>
   
    <span data-ttu-id="921b5-218">![Создание пользователя](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="921b5-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="921b5-219">На hello **профиля пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="921b5-219">On hello **User Profile** tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="921b5-220">![Новый пользователь](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="921b5-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="921b5-221">а.</span><span class="sxs-lookup"><span data-stu-id="921b5-221">a.</span></span> <span data-ttu-id="921b5-222">Тип hello **имя пользователя**, **Фамилия**, и **адрес электронной почты** действительного пользователя Azure Active Directory в hello связанные текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="921b5-222">Type hello **user name**, **last name**, and **email address** of a valid Azure Active Directory user into hello related textboxes.</span></span>
  
6. <span data-ttu-id="921b5-223">Для параметра **Status** (Состояние) выберите значение **Active** (Активно).</span><span class="sxs-lookup"><span data-stu-id="921b5-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="921b5-224">На вкладку "пароль" hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="921b5-224">On hello Password tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="921b5-225">![Новый пользователь](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="921b5-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="921b5-226">а.</span><span class="sxs-lookup"><span data-stu-id="921b5-226">a.</span></span> <span data-ttu-id="921b5-227">Введите пароль hello в hello, связанные с текстового поля.</span><span class="sxs-lookup"><span data-stu-id="921b5-227">Type hello password into hello related textbox.</span></span>

    <span data-ttu-id="921b5-228">b.</span><span class="sxs-lookup"><span data-stu-id="921b5-228">b.</span></span> <span data-ttu-id="921b5-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="921b5-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="921b5-230">Можно использовать любые другие Sugar CRM пользователя средства создания учетных записей или интерфейсы API, предоставляемые Sugar CRM tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="921b5-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="921b5-231">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="921b5-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="921b5-232">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="921b5-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSugar CRM.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="921b5-234">**tooassign tooSugar Britta Simon CRM, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="921b5-234">**tooassign Britta Simon tooSugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="921b5-235">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="921b5-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="921b5-237">В списке приложений hello выберите **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="921b5-237">In hello applications list, select **Sugar CRM**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="921b5-239">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="921b5-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="921b5-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="921b5-241">Click **Add** button.</span></span> <span data-ttu-id="921b5-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="921b5-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="921b5-244">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="921b5-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="921b5-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="921b5-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="921b5-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="921b5-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="921b5-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="921b5-247">Testing single sign-on</span></span>

<span data-ttu-id="921b5-248">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="921b5-248">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="921b5-249">При выборе плитки Sugar CRM hello в hello панели доступа, следует получать автоматически вошедшего tooyour приложение Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="921b5-249">When you click hello Sugar CRM tile in hello Access Panel, you should get automatically signed-on tooyour Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="921b5-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="921b5-250">Additional resources</span></span>

* [<span data-ttu-id="921b5-251">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="921b5-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="921b5-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="921b5-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

