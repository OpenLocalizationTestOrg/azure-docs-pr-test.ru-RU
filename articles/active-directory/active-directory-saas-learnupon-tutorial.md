---
title: "Руководство по интеграции Azure Active Directory с LearnUpon | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="268a5-103">Руководство. Интеграция Azure Active Directory с LearnUpon</span><span class="sxs-lookup"><span data-stu-id="268a5-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="268a5-104">В этом учебнике вы узнаете, как toointegrate LearnUpon с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="268a5-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="268a5-105">Интеграция с Azure AD LearnUpon предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="268a5-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="268a5-106">Можно управлять в Azure AD, имеющего доступ tooLearnUpon</span><span class="sxs-lookup"><span data-stu-id="268a5-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="268a5-107">Можно включить на пользователей tooautomatically get вошедшего tooLearnUpon (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="268a5-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="268a5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="268a5-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="268a5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="268a5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="268a5-110">Prerequisites</span></span>

<span data-ttu-id="268a5-111">tooconfigure интеграция Azure AD с LearnUpon требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="268a5-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="268a5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="268a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="268a5-113">подписка LearnUpon с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="268a5-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="268a5-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="268a5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="268a5-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="268a5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="268a5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="268a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="268a5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="268a5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="268a5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="268a5-118">Scenario description</span></span>
<span data-ttu-id="268a5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="268a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="268a5-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="268a5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="268a5-121">Добавление LearnUpon из галереи hello</span><span class="sxs-lookup"><span data-stu-id="268a5-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="268a5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="268a5-123">Добавление LearnUpon из галереи hello</span><span class="sxs-lookup"><span data-stu-id="268a5-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="268a5-124">tooconfigure hello интеграции LearnUpon в Azure AD, вы должны tooadd LearnUpon из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="268a5-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="268a5-125">**tooadd LearnUpon из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="268a5-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="268a5-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="268a5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="268a5-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="268a5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="268a5-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="268a5-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="268a5-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="268a5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="268a5-133">Введите в поле поиска hello **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="268a5-133">In hello search box, type **LearnUpon**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="268a5-135">В панели результатов hello выберите **LearnUpon**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="268a5-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="268a5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="268a5-138">В этом разделе описана настройка и проверка единого входа Azure AD в LearnUpon для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="268a5-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="268a5-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в LearnUpon является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="268a5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="268a5-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в LearnUpon должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="268a5-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="268a5-141">В LearnUpon, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="268a5-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="268a5-142">tooconfigure и теста Azure AD единого входа с LearnUpon, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="268a5-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="268a5-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="268a5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="268a5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="268a5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="268a5-145">**[Создание тестового пользователя LearnUpon](#creating-a-learnupon-test-user)**  -toohave аналог Саймон Britta в LearnUpon, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="268a5-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="268a5-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="268a5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="268a5-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="268a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="268a5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="268a5-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="268a5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="268a5-150">**tooconfigure Azure AD единого входа с LearnUpon, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="268a5-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="268a5-151">В hello в hello портала Azure **LearnUpon** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="268a5-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="268a5-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="268a5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="268a5-155">На hello **URL-адреса и домена LearnUpon** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="268a5-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="268a5-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="268a5-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="268a5-158">Обратите внимание на то, что это не Вещественное значение hello.</span><span class="sxs-lookup"><span data-stu-id="268a5-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="268a5-159">у вас есть tooupdate это значение с hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="268a5-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="268a5-160">обратитесь в службу tooget это значение [LearnUpon поддержки](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="268a5-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="268a5-161">На hello **сертификат подписи SAML** щелкните **сертификата (Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="268a5-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="268a5-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="268a5-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="268a5-165">На hello **конфигурации LearnUpon** щелкните **Настройка LearnUpon** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="268a5-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="268a5-166">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="268a5-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="268a5-168">Откройте другую страницу браузера и войдите в LearnUpon с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="268a5-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="268a5-169">Нажмите кнопку hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="268a5-169">Click hello **settings** tab.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="268a5-171">Нажмите кнопку **Single Sign On - SAML**, а затем нажмите кнопку **Общие параметры** tooconfigure параметры SAML.</span><span class="sxs-lookup"><span data-stu-id="268a5-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="268a5-173">В hello **Общие параметры** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="268a5-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="268a5-175">а.</span><span class="sxs-lookup"><span data-stu-id="268a5-175">a.</span></span> <span data-ttu-id="268a5-176">Щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="268a5-176">Select **Enabled**.</span></span>

    <span data-ttu-id="268a5-177">b.</span><span class="sxs-lookup"><span data-stu-id="268a5-177">b.</span></span> <span data-ttu-id="268a5-178">Для параметра **Версия** установите значение **2.0**.</span><span class="sxs-lookup"><span data-stu-id="268a5-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="268a5-179">c.</span><span class="sxs-lookup"><span data-stu-id="268a5-179">c.</span></span> <span data-ttu-id="268a5-180">Для параметра **Пропустить условия** установите значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="268a5-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="268a5-181">d.</span><span class="sxs-lookup"><span data-stu-id="268a5-181">d.</span></span> <span data-ttu-id="268a5-182">В hello **имя маркера блога SAML param** в текстовое поле имя типа hello запрос post параметр toohello вышеуказанных SAML потребителя URL-адрес, содержащий toobe утверждения SAML hello проверены и проверка подлинности — например  **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="268a5-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="268a5-183">д.</span><span class="sxs-lookup"><span data-stu-id="268a5-183">e.</span></span> <span data-ttu-id="268a5-184">В hello **формат идентификатора имени** текстовое значение hello типа, указывающее, где в пользователи hello утверждения SAML идентификатор (адрес электронной почты) находится — например **urn: oasis: имена: tc: SAML:1.1:nameid-формат: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="268a5-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="268a5-185">f.</span><span class="sxs-lookup"><span data-stu-id="268a5-185">f.</span></span> <span data-ttu-id="268a5-186">В hello **определить расположение поставщика** текстового поля, типа hello значение, указывающее, где hello отправляются tooif пользователи они щелкнуть значок данного загруженного на экране входа Azure портала.</span><span class="sxs-lookup"><span data-stu-id="268a5-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="268a5-187">ж.</span><span class="sxs-lookup"><span data-stu-id="268a5-187">g.</span></span> <span data-ttu-id="268a5-188">В hello **выход URL-адрес** текстовое поле, вставить hello **URL-адрес выхода** скопирован из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="268a5-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="268a5-189">h.</span><span class="sxs-lookup"><span data-stu-id="268a5-189">h.</span></span> <span data-ttu-id="268a5-190">Нажмите кнопку **управление отпечатков пальцев**и затем передать отпечаток пальца hello загруженного сертификата.</span><span class="sxs-lookup"><span data-stu-id="268a5-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="268a5-191">Нажмите кнопку **параметры пользователя**, а затем выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="268a5-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="268a5-193">а.</span><span class="sxs-lookup"><span data-stu-id="268a5-193">a.</span></span> <span data-ttu-id="268a5-194">В hello **формат идентификатора имени** в текстовое поле типа hello, сообщающего нам в вашей firstname пользователей hello утверждения SAML находится значение — например: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="268a5-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="268a5-195">b.</span><span class="sxs-lookup"><span data-stu-id="268a5-195">b.</span></span> <span data-ttu-id="268a5-196">В hello **последний формат идентификатора имени** в текстовое поле типа hello, сообщающего нам в вашей lastname пользователей hello утверждения SAML находится значение — например: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="268a5-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="268a5-197">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="268a5-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="268a5-198">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="268a5-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="268a5-199">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="268a5-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="268a5-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="268a5-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="268a5-201">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="268a5-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="268a5-203">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="268a5-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="268a5-204">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="268a5-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="268a5-206">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="268a5-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="268a5-208">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="268a5-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="268a5-210">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="268a5-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="268a5-212">а.</span><span class="sxs-lookup"><span data-stu-id="268a5-212">a.</span></span> <span data-ttu-id="268a5-213">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="268a5-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="268a5-214">b.</span><span class="sxs-lookup"><span data-stu-id="268a5-214">b.</span></span> <span data-ttu-id="268a5-215">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="268a5-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="268a5-216">c.</span><span class="sxs-lookup"><span data-stu-id="268a5-216">c.</span></span> <span data-ttu-id="268a5-217">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="268a5-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="268a5-218">d.</span><span class="sxs-lookup"><span data-stu-id="268a5-218">d.</span></span> <span data-ttu-id="268a5-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="268a5-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="268a5-220">Создание тестового пользователя LearnUpon</span><span class="sxs-lookup"><span data-stu-id="268a5-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="268a5-221">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="268a5-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="268a5-222">Приложение LearnUpon поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="268a5-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="268a5-223">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="268a5-223">There is no action item for you in this section.</span></span> <span data-ttu-id="268a5-224">Если он еще не существует во время попытки tooaccess LearnUpon создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="268a5-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="268a5-225">[Настройка единого входа в Azure AD](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="268a5-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="268a5-226">Если требуется toocreate пользователя вручную, необходимо toocontact [LearnUpon поддержки](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="268a5-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="268a5-227">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="268a5-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="268a5-228">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLearnUpon доступа.</span><span class="sxs-lookup"><span data-stu-id="268a5-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="268a5-230">**tooassign tooLearnUpon Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="268a5-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="268a5-231">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="268a5-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="268a5-233">В списке приложений hello выберите **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="268a5-233">In hello applications list, select **LearnUpon**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="268a5-235">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="268a5-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="268a5-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="268a5-237">Click **Add** button.</span></span> <span data-ttu-id="268a5-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="268a5-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="268a5-240">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="268a5-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="268a5-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="268a5-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="268a5-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="268a5-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="268a5-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="268a5-243">Testing single sign-on</span></span>

<span data-ttu-id="268a5-244">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="268a5-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="268a5-245">При нажатии кнопки hello LearnUpon плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour LearnUpon приложения.</span><span class="sxs-lookup"><span data-stu-id="268a5-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="268a5-246">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="268a5-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="268a5-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="268a5-247">Additional resources</span></span>

* [<span data-ttu-id="268a5-248">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="268a5-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="268a5-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="268a5-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

