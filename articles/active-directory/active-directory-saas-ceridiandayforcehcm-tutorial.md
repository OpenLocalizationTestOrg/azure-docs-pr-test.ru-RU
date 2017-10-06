---
title: "Руководство. Интеграция Azure Active Directory с Ceridian Dayforce HCM | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="e5af4-103">Учебник. Интеграция Azure Active Directory с Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="e5af4-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="e5af4-104">В этом учебнике вы узнаете, как toointegrate HCM Dayforce Ceridian с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e5af4-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5af4-105">Интеграция с Azure AD Ceridian Dayforce HCM предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e5af4-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e5af4-106">Можно управлять в Azure AD, имеющего доступ tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="e5af4-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="e5af4-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooCeridian HCM Dayforce (Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="e5af4-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e5af4-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e5af4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e5af4-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5af4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5af4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e5af4-110">Prerequisites</span></span>

<span data-ttu-id="e5af4-111">tooconfigure интеграция Azure AD с Ceridian Dayforce HCM требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="e5af4-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="e5af4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e5af4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5af4-113">подписка Ceridian Dayforce HCM с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e5af4-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5af4-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e5af4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5af4-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="e5af4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5af4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e5af4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5af4-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5af4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5af4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e5af4-118">Scenario description</span></span>
<span data-ttu-id="e5af4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e5af4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5af4-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="e5af4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5af4-121">Добавление Ceridian Dayforce HCM из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e5af4-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="e5af4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5af4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="e5af4-123">Добавление Ceridian Dayforce HCM из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e5af4-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="e5af4-124">tooconfigure hello интеграции Ceridian Dayforce HCM в Azure AD, вы должны tooadd Ceridian Dayforce HCM из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e5af4-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e5af4-125">**tooadd HCM Dayforce Ceridian из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="e5af4-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5af4-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e5af4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="e5af4-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e5af4-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="e5af4-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e5af4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="e5af4-133">Введите в поле поиска hello **Ceridian Dayforce HCM**выберите **Ceridian Dayforce HCM** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e5af4-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![HCM Dayforce Ceridian в списке результатов hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e5af4-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5af4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e5af4-136">В этом разделе описана настройка и проверка единого входа Azure AD в Ceridian Dayforce HCM с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5af4-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e5af4-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Ceridian Dayforce HCM является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5af4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="e5af4-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Ceridian Dayforce HCM должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="e5af4-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="e5af4-139">В Ceridian Dayforce HCM, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="e5af4-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e5af4-140">tooconfigure и теста Azure AD единого входа с Ceridian Dayforce HCM, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e5af4-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e5af4-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="e5af4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e5af4-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e5af4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5af4-143">**[Создание тестового пользователя Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user) ** -toohave аналог Саймон Britta в Ceridian Dayforce HCM, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e5af4-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e5af4-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="e5af4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5af4-145">**[Тестирование единого входа](#test-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e5af4-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e5af4-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5af4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e5af4-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="e5af4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="e5af4-148">**tooconfigure Azure AD единого входа с Ceridian Dayforce HCM, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e5af4-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5af4-149">В hello в hello портала Azure **Ceridian Dayforce HCM** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="e5af4-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="e5af4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="e5af4-153">На hello **URL-адреса и домена HCM Dayforce Ceridian** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e5af4-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="e5af4-155">а.</span><span class="sxs-lookup"><span data-stu-id="e5af4-155">a.</span></span> <span data-ttu-id="e5af4-156">В hello **на URL-адрес входа** textbox hello введите URL-адрес, используемый вашей пользователей на toosign tooyour Ceridian Dayforce HCM приложения.</span><span class="sxs-lookup"><span data-stu-id="e5af4-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="e5af4-157">Среда</span><span class="sxs-lookup"><span data-stu-id="e5af4-157">Environment</span></span> | <span data-ttu-id="e5af4-158">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e5af4-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="e5af4-159">Рабочая среда</span><span class="sxs-lookup"><span data-stu-id="e5af4-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="e5af4-160">Тестирование</span><span class="sxs-lookup"><span data-stu-id="e5af4-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="e5af4-161">b.</span><span class="sxs-lookup"><span data-stu-id="e5af4-161">b.</span></span> <span data-ttu-id="e5af4-162">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="e5af4-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="e5af4-163">Среда</span><span class="sxs-lookup"><span data-stu-id="e5af4-163">Environment</span></span> | <span data-ttu-id="e5af4-164">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e5af4-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="e5af4-165">Рабочая среда</span><span class="sxs-lookup"><span data-stu-id="e5af4-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="e5af4-166">Тестирование</span><span class="sxs-lookup"><span data-stu-id="e5af4-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="e5af4-167">c.</span><span class="sxs-lookup"><span data-stu-id="e5af4-167">c.</span></span> <span data-ttu-id="e5af4-168">В hello **URL-адрес ответа** textbox hello введите URL-адрес, используемый Azure AD toopost hello ответа.</span><span class="sxs-lookup"><span data-stu-id="e5af4-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="e5af4-169">Среда</span><span class="sxs-lookup"><span data-stu-id="e5af4-169">Environment</span></span> | <span data-ttu-id="e5af4-170">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e5af4-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="e5af4-171">Рабочая среда</span><span class="sxs-lookup"><span data-stu-id="e5af4-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="e5af4-172">Тестирование</span><span class="sxs-lookup"><span data-stu-id="e5af4-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="e5af4-173">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e5af4-173">These values are not real.</span></span> <span data-ttu-id="e5af4-174">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="e5af4-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="e5af4-175">Обратитесь к [группа поддержки клиента HCM Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="e5af4-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="e5af4-176">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e5af4-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="e5af4-178">Приложение Ceridian Dayforce HCM ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="e5af4-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="e5af4-179">Работать с [Ceridian Dayforce HCM поддержки](https://www.ceridian.com/contact-us/index.html) первый идентификатор пользователя hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="e5af4-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="e5af4-180">Корпорация Майкрософт рекомендует использовать hello **«name»** атрибут в качестве идентификатора пользователя.</span><span class="sxs-lookup"><span data-stu-id="e5af4-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="e5af4-181">Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** раздел на странице интеграции приложений.</span><span class="sxs-lookup"><span data-stu-id="e5af4-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="e5af4-182">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="e5af4-182">hello following screenshot shows an example for this.</span></span>  

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="e5af4-184">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="e5af4-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="e5af4-185">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="e5af4-185">Attribute Name</span></span>  | <span data-ttu-id="e5af4-186">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="e5af4-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="e5af4-187">name</span><span class="sxs-lookup"><span data-stu-id="e5af4-187">name</span></span>  | <span data-ttu-id="e5af4-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="e5af4-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="e5af4-189">а.</span><span class="sxs-lookup"><span data-stu-id="e5af4-189">a.</span></span> <span data-ttu-id="e5af4-190">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e5af4-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="e5af4-193">b.</span><span class="sxs-lookup"><span data-stu-id="e5af4-193">b.</span></span> <span data-ttu-id="e5af4-194">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="e5af4-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="e5af4-195">c.</span><span class="sxs-lookup"><span data-stu-id="e5af4-195">c.</span></span> <span data-ttu-id="e5af4-196">В hello **значение** список, атрибут пользователя выберите hello требуется toouse вашей реализации.</span><span class="sxs-lookup"><span data-stu-id="e5af4-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="e5af4-197">Например, если нужно toouse hello EmployeeID как уникальный идентификатор пользователя, и значение атрибута hello были сохранены в hello ExtensionAttribute2, выберите **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="e5af4-198">d.</span><span class="sxs-lookup"><span data-stu-id="e5af4-198">d.</span></span> <span data-ttu-id="e5af4-199">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-199">Click **Ok**.</span></span>

7. <span data-ttu-id="e5af4-200">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e5af4-200">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="e5af4-202">На hello **Ceridian Dayforce HCM конфигурации** щелкните **Настройка HCM Dayforce Ceridian** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="e5af4-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e5af4-203">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="e5af4-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="e5af4-205">tooconfigure единого входа на **Ceridian Dayforce HCM** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Ceridian Dayforce HCM поддержки](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="e5af4-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="e5af4-206">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="e5af4-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e5af4-207">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="e5af4-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e5af4-208">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e5af4-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e5af4-209">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5af4-209">Create an Azure AD test user</span></span>

<span data-ttu-id="e5af4-210">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e5af4-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="e5af4-212">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e5af4-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5af4-213">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e5af4-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e5af4-215">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e5af4-217">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e5af4-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e5af4-219">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e5af4-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e5af4-221">а.</span><span class="sxs-lookup"><span data-stu-id="e5af4-221">a.</span></span> <span data-ttu-id="e5af4-222">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5af4-223">b.</span><span class="sxs-lookup"><span data-stu-id="e5af4-223">b.</span></span> <span data-ttu-id="e5af4-224">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e5af4-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e5af4-225">c.</span><span class="sxs-lookup"><span data-stu-id="e5af4-225">c.</span></span> <span data-ttu-id="e5af4-226">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="e5af4-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e5af4-227">d.</span><span class="sxs-lookup"><span data-stu-id="e5af4-227">d.</span></span> <span data-ttu-id="e5af4-228">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="e5af4-229">Создание тестового пользователя Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="e5af4-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="e5af4-230">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="e5af4-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="e5af4-231">Работать с hello [Ceridian Dayforce HCM поддержки](https://www.ceridian.com/contact-us/index.html) tooget пользователей, добавленных в hello Ceridian Dayforce HCM приложения.</span><span class="sxs-lookup"><span data-stu-id="e5af4-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e5af4-232">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="e5af4-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e5af4-233">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="e5af4-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e5af4-235">**tooassign Britta Simon tooCeridian Dayforce HCM выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="e5af4-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5af4-236">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e5af4-238">В списке приложений hello выберите **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="e5af4-240">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e5af4-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-242">Click **Add** button.</span></span> <span data-ttu-id="e5af4-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e5af4-245">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e5af4-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e5af4-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5af4-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e5af4-248">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="e5af4-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e5af4-249">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="e5af4-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="e5af4-251">**tooassign Britta Simon tooCeridian Dayforce HCM выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="e5af4-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5af4-252">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e5af4-254">В списке приложений hello выберите **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![ссылка Ceridian Dayforce HCM Hello в списке приложений hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="e5af4-256">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="e5af4-258">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-258">Click **Add** button.</span></span> <span data-ttu-id="e5af4-259">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="e5af4-261">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e5af4-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e5af4-262">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5af4-263">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e5af4-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e5af4-264">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e5af4-264">Test single sign-on</span></span>

<span data-ttu-id="e5af4-265">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="e5af4-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="e5af4-266">При нажатии кнопки hello Ceridian Dayforce HCM плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Ceridian Dayforce HCM приложения.</span><span class="sxs-lookup"><span data-stu-id="e5af4-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e5af4-267">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e5af4-267">Additional resources</span></span>

* [<span data-ttu-id="e5af4-268">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5af4-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5af4-269">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e5af4-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

