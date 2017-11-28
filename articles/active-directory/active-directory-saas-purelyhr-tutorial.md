---
title: "Руководство по интеграции Azure Active Directory с PurelyHR | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="ae3f5-103">Руководство. Интеграция Azure Active Directory с PurelyHR</span><span class="sxs-lookup"><span data-stu-id="ae3f5-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="ae3f5-104">В этом учебнике вы узнаете, как toointegrate PurelyHR с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae3f5-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae3f5-105">Интеграция с Azure AD PurelyHR предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ae3f5-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ae3f5-106">Можно управлять в Azure AD, имеющего доступ tooPurelyHR</span><span class="sxs-lookup"><span data-stu-id="ae3f5-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="ae3f5-107">Можно включить на пользователей tooautomatically get вошедшего tooPurelyHR (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae3f5-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae3f5-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ae3f5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ae3f5-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae3f5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae3f5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ae3f5-110">Prerequisites</span></span>

<span data-ttu-id="ae3f5-111">tooconfigure интеграция Azure AD с PurelyHR требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ae3f5-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="ae3f5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ae3f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae3f5-113">подписка PurelyHR с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae3f5-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae3f5-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ae3f5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae3f5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae3f5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae3f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae3f5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ae3f5-118">Scenario description</span></span>
<span data-ttu-id="ae3f5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae3f5-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ae3f5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae3f5-121">Добавление PurelyHR из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ae3f5-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="ae3f5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae3f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="ae3f5-123">Добавление PurelyHR из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ae3f5-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="ae3f5-124">tooconfigure hello интеграции PurelyHR в Azure AD, вы должны tooadd PurelyHR из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ae3f5-125">**tooadd PurelyHR из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ae3f5-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae3f5-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae3f5-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ae3f5-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ae3f5-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ae3f5-133">Введите в поле поиска hello **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-133">In hello search box, type **PurelyHR**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="ae3f5-135">В панели результатов hello выберите **PurelyHR**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae3f5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae3f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae3f5-138">В этом разделе описана настройка и проверка единого входа Azure AD в PurelyHR с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae3f5-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PurelyHR является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="ae3f5-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в PurelyHR должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="ae3f5-141">В PurelyHR, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ae3f5-142">tooconfigure и теста Azure AD единого входа с PurelyHR, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ae3f5-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ae3f5-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ae3f5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae3f5-145">**[Создание тестового пользователя PurelyHR](#creating-a-purelyhr-test-user)**  -toohave аналог Саймон Britta в PurelyHR, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae3f5-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae3f5-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae3f5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae3f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae3f5-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="ae3f5-150">**tooconfigure Azure AD единого входа с PurelyHR, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ae3f5-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae3f5-151">В hello в hello портала Azure **PurelyHR** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ae3f5-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="ae3f5-155">На hello **PurelyHR доменов и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="ae3f5-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="ae3f5-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="ae3f5-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="ae3f5-158">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="ae3f5-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="ae3f5-160">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="ae3f5-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="ae3f5-161">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-161">These values are not hello real.</span></span> <span data-ttu-id="ae3f5-162">Обновите эти значения с hello фактический URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="ae3f5-163">Обратитесь к [группа поддержки клиента PurelyHR](http://support.purelyhr.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="ae3f5-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="ae3f5-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ae3f5-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="ae3f5-168">На hello **конфигурации PurelyHR** щелкните **Настройка PurelyHR** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ae3f5-169">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ae3f5-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="ae3f5-171">tooconfigure единого входа на **PurelyHR** стороны, веб-сайт tootheir входа в систему с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="ae3f5-172">Откройте hello **мониторинга** параметры hello в hello инструментов и выберите команду **настройки единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="ae3f5-173">Вставить hello значения в полях hello, как описано ниже-</span><span class="sxs-lookup"><span data-stu-id="ae3f5-173">Paste hello values in hello boxes as described below-</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="ae3f5-175">а.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-175">a.</span></span> <span data-ttu-id="ae3f5-176">Откройте hello **Certificate(Bas64)** загружен из hello портал Azure в Блокноте и скопируйте значение сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="ae3f5-177">Вставить hello копируется значение hello **сертификат X.509** поле.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="ae3f5-178">b.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-178">b.</span></span> <span data-ttu-id="ae3f5-179">В hello **URL-адрес поставщика удостоверений издателя** вставьте hello **идентификатор сущности SAML** копируются hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="ae3f5-180">c.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-180">c.</span></span> <span data-ttu-id="ae3f5-181">В hello **URL-адрес конечной точки поставщика удостоверений** вставьте hello **SAML единого входа URL-адрес службы** копируются hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="ae3f5-182">d.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-182">d.</span></span> <span data-ttu-id="ae3f5-183">Проверьте hello **автоматическое создание пользователей** флажок tooenable автоматической подготовки пользователей в PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="ae3f5-184">д.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-184">e.</span></span> <span data-ttu-id="ae3f5-185">Нажмите кнопку **сохранить изменения** toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="ae3f5-186">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ae3f5-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ae3f5-187">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ae3f5-188">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae3f5-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae3f5-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae3f5-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae3f5-190">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ae3f5-192">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ae3f5-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae3f5-193">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae3f5-195">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae3f5-197">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ae3f5-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae3f5-199">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ae3f5-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae3f5-201">а.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-201">a.</span></span> <span data-ttu-id="ae3f5-202">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae3f5-203">b.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-203">b.</span></span> <span data-ttu-id="ae3f5-204">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae3f5-205">c.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-205">c.</span></span> <span data-ttu-id="ae3f5-206">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ae3f5-207">d.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-207">d.</span></span> <span data-ttu-id="ae3f5-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="ae3f5-209">Создание тестового пользователя PurelyHR</span><span class="sxs-lookup"><span data-stu-id="ae3f5-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="ae3f5-210">Пользователи toolog tooenable Azure AD в tooPurelyHR, их необходимо подготовить в PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="ae3f5-211">В PurelyHR подготовка пользователей осуществляется автоматически, при этом никакие ручные действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ae3f5-212">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ae3f5-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ae3f5-213">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPurelyHR доступа.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ae3f5-215">**tooassign tooPurelyHR Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ae3f5-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae3f5-216">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ae3f5-218">В списке приложений hello выберите **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-218">In hello applications list, select **PurelyHR**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="ae3f5-220">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ae3f5-222">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-222">Click **Add** button.</span></span> <span data-ttu-id="ae3f5-223">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ae3f5-225">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ae3f5-226">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae3f5-227">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae3f5-228">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ae3f5-228">Testing single sign-on</span></span>

<span data-ttu-id="ae3f5-229">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ae3f5-230">Нажмите кнопку hello запоминаются LMS плитки в панели доступа hello вы получаете автоматически вошедшего tooyour запоминаются LMS приложения.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="ae3f5-231">Дополнительные сведения о панели доступа hello см. в разделе.</span><span class="sxs-lookup"><span data-stu-id="ae3f5-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="ae3f5-232">[Введение toohello панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ae3f5-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae3f5-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ae3f5-233">Additional resources</span></span>

* [<span data-ttu-id="ae3f5-234">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae3f5-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae3f5-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae3f5-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

