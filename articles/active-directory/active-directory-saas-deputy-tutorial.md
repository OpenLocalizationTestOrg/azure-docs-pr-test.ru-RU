---
title: "Учебник. Интеграция Azure Active Directory с Deputy | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и заместителем."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="bfb19-103">Руководство. Интеграция Azure Active Directory с Deputy</span><span class="sxs-lookup"><span data-stu-id="bfb19-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="bfb19-104">В этом учебнике вы узнаете, как toointegrate заместителем с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfb19-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfb19-105">Интеграция с Azure AD заместителем предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bfb19-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bfb19-106">Можно управлять в Azure AD, имеющего доступ tooDeputy</span><span class="sxs-lookup"><span data-stu-id="bfb19-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="bfb19-107">Можно включить на пользователей tooautomatically get вошедшего tooDeputy (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb19-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bfb19-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bfb19-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bfb19-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfb19-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfb19-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bfb19-110">Prerequisites</span></span>

<span data-ttu-id="bfb19-111">tooconfigure интеграция Azure AD с заместителем требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="bfb19-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="bfb19-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bfb19-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfb19-113">подписка Deputy с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bfb19-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfb19-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bfb19-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfb19-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="bfb19-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfb19-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bfb19-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfb19-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfb19-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfb19-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bfb19-118">Scenario description</span></span>
<span data-ttu-id="bfb19-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bfb19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfb19-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="bfb19-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfb19-121">Добавление заместителем из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bfb19-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="bfb19-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb19-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="bfb19-123">Добавление заместителем из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bfb19-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="bfb19-124">tooconfigure hello интеграции заместителем в Azure AD, вы должны tooadd заместителем из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bfb19-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bfb19-125">**tooadd заместителем из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bfb19-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb19-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bfb19-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bfb19-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bfb19-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bfb19-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bfb19-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bfb19-133">Введите в поле поиска hello **заместителем**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-133">In hello search box, type **Deputy**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="bfb19-135">В панели результатов hello выберите **заместителем**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bfb19-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bfb19-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb19-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bfb19-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Deputy с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfb19-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bfb19-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в заместителем является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfb19-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="bfb19-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в заместителем должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="bfb19-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="bfb19-141">В заместителем, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="bfb19-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bfb19-142">tooconfigure и теста Azure AD единого входа с заместителем, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bfb19-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bfb19-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="bfb19-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bfb19-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bfb19-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfb19-145">**[Создание тестового пользователя заместителем](#creating-a-deputy-test-user)**  -toohave аналог Саймон Britta в заместителем, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="bfb19-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfb19-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="bfb19-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfb19-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bfb19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bfb19-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb19-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bfb19-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении заместителем.</span><span class="sxs-lookup"><span data-stu-id="bfb19-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="bfb19-150">**tooconfigure Azure AD единого входа с заместителем, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bfb19-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb19-151">В hello в hello портала Azure **заместителем** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bfb19-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="bfb19-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="bfb19-155">На hello **заместителем доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="bfb19-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="bfb19-157">а.</span><span class="sxs-lookup"><span data-stu-id="bfb19-157">a.</span></span> <span data-ttu-id="bfb19-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="bfb19-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="bfb19-159">b.</span><span class="sxs-lookup"><span data-stu-id="bfb19-159">b.</span></span> <span data-ttu-id="bfb19-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="bfb19-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="bfb19-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="bfb19-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="bfb19-162">При необходимости приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="bfb19-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="bfb19-164">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="bfb19-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="bfb19-165">Суффикс региона Deputy необязательный, или следует использовать один из следующих: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an.</span><span class="sxs-lookup"><span data-stu-id="bfb19-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bfb19-166">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="bfb19-166">These values are not real.</span></span> <span data-ttu-id="bfb19-167">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="bfb19-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="bfb19-168">Обратитесь к [группа поддержки заместителем](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="bfb19-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="bfb19-169">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="bfb19-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="bfb19-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bfb19-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bfb19-173">На hello **конфигурации заместителем** щелкните **Настройка заместителем** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="bfb19-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bfb19-174">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="bfb19-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="bfb19-176">Перейдите на URL-адреса toohello:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="bfb19-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="bfb19-177">Go слишком**параметры безопасности** и нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="bfb19-179">На странице **Параметры безопасности** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="bfb19-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="bfb19-181">а.</span><span class="sxs-lookup"><span data-stu-id="bfb19-181">a.</span></span> <span data-ttu-id="bfb19-182">разрешите **вход с помощью учетных записей социальных сетей**;</span><span class="sxs-lookup"><span data-stu-id="bfb19-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="bfb19-183">b.</span><span class="sxs-lookup"><span data-stu-id="bfb19-183">b.</span></span> <span data-ttu-id="bfb19-184">Откройте сертификат в кодировке Base64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **OpenSSL сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="bfb19-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="bfb19-185">c.</span><span class="sxs-lookup"><span data-stu-id="bfb19-185">c.</span></span> <span data-ttu-id="bfb19-186">Введите в текстовое поле URL-адрес единого входа SAML hello`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="bfb19-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="bfb19-187">d.</span><span class="sxs-lookup"><span data-stu-id="bfb19-187">d.</span></span> <span data-ttu-id="bfb19-188">В текстовом поле URL-адрес единого входа SAML hello, замените `<your subdomain>` с дочернего домена.</span><span class="sxs-lookup"><span data-stu-id="bfb19-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="bfb19-189">д.</span><span class="sxs-lookup"><span data-stu-id="bfb19-189">e.</span></span> <span data-ttu-id="bfb19-190">В текстовом поле URL-адрес единого входа SAML hello, замените `<saml sso url>` с hello **SAML единого входа URL-адрес службы** было скопировано из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb19-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="bfb19-191">f.</span><span class="sxs-lookup"><span data-stu-id="bfb19-191">f.</span></span> <span data-ttu-id="bfb19-192">Нажмите кнопку **Сохранить параметры**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="bfb19-193">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="bfb19-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bfb19-194">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="bfb19-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bfb19-195">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfb19-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bfb19-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb19-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="bfb19-197">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb19-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bfb19-199">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bfb19-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb19-200">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bfb19-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bfb19-202">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bfb19-204">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="bfb19-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bfb19-206">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bfb19-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bfb19-208">а.</span><span class="sxs-lookup"><span data-stu-id="bfb19-208">a.</span></span> <span data-ttu-id="bfb19-209">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfb19-210">b.</span><span class="sxs-lookup"><span data-stu-id="bfb19-210">b.</span></span> <span data-ttu-id="bfb19-211">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bfb19-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bfb19-212">c.</span><span class="sxs-lookup"><span data-stu-id="bfb19-212">c.</span></span> <span data-ttu-id="bfb19-213">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bfb19-214">d.</span><span class="sxs-lookup"><span data-stu-id="bfb19-214">d.</span></span> <span data-ttu-id="bfb19-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="bfb19-216">Создание тестового пользователя приложения Deputy</span><span class="sxs-lookup"><span data-stu-id="bfb19-216">Creating a Deputy test user</span></span>

<span data-ttu-id="bfb19-217">Пользователи toolog tooenable Azure AD в tooDeputy, их необходимо подготовить в заместителем.</span><span class="sxs-lookup"><span data-stu-id="bfb19-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="bfb19-218">В случае с Deputy подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="bfb19-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="bfb19-219">tooprovision учетной записи пользователя, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="bfb19-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="bfb19-220">Войдите на сайте компании заместителем tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="bfb19-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="bfb19-221">На верхней панели навигации панели hello выберите **людей**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="bfb19-222">![Люди](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="bfb19-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="bfb19-223">Щелкните hello **добавьте людей** и нажмите кнопку **добавить один человек**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="bfb19-224">![Добавить участников](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "добавить участников")</span><span class="sxs-lookup"><span data-stu-id="bfb19-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="bfb19-225">Выполните следующие шаги hello и нажмите **сохранить и приглашать**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="bfb19-226">![Новый пользователь](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="bfb19-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="bfb19-227">а.</span><span class="sxs-lookup"><span data-stu-id="bfb19-227">a.</span></span> <span data-ttu-id="bfb19-228">В hello **имя** в текстовое поле имя типа hello пользователя как **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="bfb19-229">b.</span><span class="sxs-lookup"><span data-stu-id="bfb19-229">b.</span></span> <span data-ttu-id="bfb19-230">В hello **электронной почты** текстовом поле введите адрес электронной почты hello требуется tooprovision учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfb19-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="bfb19-231">c.</span><span class="sxs-lookup"><span data-stu-id="bfb19-231">c.</span></span> <span data-ttu-id="bfb19-232">В hello **работать на** в текстовое поле имя бизнеса типа hello.</span><span class="sxs-lookup"><span data-stu-id="bfb19-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="bfb19-233">d.</span><span class="sxs-lookup"><span data-stu-id="bfb19-233">d.</span></span> <span data-ttu-id="bfb19-234">Нажмите кнопку **Save & Invite** (Сохранить и пригласить).</span><span class="sxs-lookup"><span data-stu-id="bfb19-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="bfb19-235">Hello владельцем учетной записи AAD получит сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="bfb19-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="bfb19-236">Можно использовать любые другие заместителем пользователя средства создания учетных записей или интерфейсы API, предоставляемые заместителем tooprovision AAD учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="bfb19-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bfb19-237">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bfb19-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bfb19-238">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooDeputy доступа.</span><span class="sxs-lookup"><span data-stu-id="bfb19-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bfb19-240">**tooassign tooDeputy Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bfb19-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb19-241">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bfb19-243">В списке приложений hello выберите **заместителем**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-243">In hello applications list, select **Deputy**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="bfb19-245">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bfb19-247">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-247">Click **Add** button.</span></span> <span data-ttu-id="bfb19-248">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bfb19-250">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="bfb19-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bfb19-251">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfb19-252">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bfb19-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bfb19-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bfb19-253">Testing single sign-on</span></span>

<span data-ttu-id="bfb19-254">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="bfb19-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="bfb19-255">При нажатии кнопки hello заместителем плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour заместителем приложения.</span><span class="sxs-lookup"><span data-stu-id="bfb19-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bfb19-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bfb19-256">Additional resources</span></span>

* [<span data-ttu-id="bfb19-257">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfb19-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfb19-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfb19-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

