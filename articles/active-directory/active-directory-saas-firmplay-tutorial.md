---
title: "Руководство. Интеграция Azure Active Directory с FirmPlay — Employee Advocacy for Recruiting | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FirmPlay - представительство найму сотрудников."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="aab40-103">Руководство. Интеграция Azure Active Directory с FirmPlay — Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="aab40-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="aab40-104">В этом учебнике вы узнаете, как toointegrate FirmPlay - сотрудник представительство найму с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aab40-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aab40-105">Интеграция FirmPlay - сотрудник представительство найму с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="aab40-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aab40-106">Можно управлять в Azure AD, имеющего доступ tooFirmPlay - сотрудник представительство найму</span><span class="sxs-lookup"><span data-stu-id="aab40-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="aab40-107">Ваш пользователей tooautomatically get вошедшего tooFirmPlay - сотрудник представительство найму (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="aab40-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aab40-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="aab40-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="aab40-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aab40-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aab40-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aab40-110">Prerequisites</span></span>

<span data-ttu-id="aab40-111">Интеграция Azure AD с FirmPlay - сотрудник представительство найму, tooconfigure требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="aab40-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="aab40-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="aab40-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aab40-113">подписка на FirmPlay — Employee Advocacy for Recruiting с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="aab40-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="aab40-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="aab40-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="aab40-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="aab40-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aab40-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="aab40-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="aab40-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aab40-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="aab40-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="aab40-118">Scenario description</span></span>
<span data-ttu-id="aab40-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="aab40-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aab40-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="aab40-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aab40-121">Добавление FirmPlay - сотрудник представительство найму из галереи hello</span><span class="sxs-lookup"><span data-stu-id="aab40-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="aab40-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="aab40-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="aab40-123">Добавление FirmPlay - сотрудник представительство найму из галереи hello</span><span class="sxs-lookup"><span data-stu-id="aab40-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="aab40-124">Интеграция hello tooconfigure FirmPlay - сотрудник представительство найму в Azure AD необходимо tooadd FirmPlay - сотрудник представительство найму из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="aab40-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aab40-125">**tooadd FirmPlay - сотрудник представительство найму из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="aab40-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aab40-126">В hello ** [портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="aab40-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aab40-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="aab40-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aab40-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="aab40-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="aab40-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="aab40-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="aab40-133">Введите в поле поиска hello **FirmPlay - сотрудник представительство найму**.</span><span class="sxs-lookup"><span data-stu-id="aab40-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="aab40-135">В панели результатов hello выберите **FirmPlay - сотрудник представительство найму**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="aab40-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aab40-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="aab40-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aab40-138">В этом разделе описана настройка и проверка единого входа Azure AD в FirmPlay — Employee Advocacy for Recruiting с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aab40-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aab40-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FirmPlay - сотрудник представительство найму является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aab40-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="aab40-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в FirmPlay - сотрудник представительство найму должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="aab40-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="aab40-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **имя пользователя** в FirmPlay - представительство найму сотрудников.</span><span class="sxs-lookup"><span data-stu-id="aab40-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="aab40-142">tooconfigure и теста Azure AD единого входа с FirmPlay - сотрудник представительство найму, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="aab40-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aab40-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="aab40-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aab40-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="aab40-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aab40-145">**[Создание сотрудника представительство найму тестового пользователя FirmPlay -](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user) ** -toohave аналог Саймон Britta в FirmPlay: операции Employee для сотрудников, то есть связанные представление ей toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aab40-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="aab40-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="aab40-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aab40-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="aab40-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aab40-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="aab40-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aab40-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в вашей FirmPlay - приложение по найму представительство сотрудника.</span><span class="sxs-lookup"><span data-stu-id="aab40-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="aab40-150">**tooconfigure Azure AD единого входа с FirmPlay - сотрудник представительство найму, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="aab40-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="aab40-151">На портале управления Azure hello на hello **FirmPlay - сотрудник представительство найму** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="aab40-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="aab40-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="aab40-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="aab40-155">На hello **FirmPlay - представительство сотрудников о приеме на работу домена и URL-адреса** раздела hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="aab40-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="aab40-157">Обратите внимание на то, что это не Вещественное значение hello.</span><span class="sxs-lookup"><span data-stu-id="aab40-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="aab40-158">У вас есть tooupdate это значение с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="aab40-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="aab40-159">Обратитесь к [FirmPlay - сотрудник представительство группа поддержки по найму](mailto:engineering@firmplay.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="aab40-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="aab40-160">На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="aab40-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="aab40-162">На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**.</span><span class="sxs-lookup"><span data-stu-id="aab40-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="aab40-163">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="aab40-163">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="aab40-165">На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="aab40-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="aab40-167">На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aab40-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="aab40-169">На hello **сертификат подписи SAML** щелкните **сертификата (base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="aab40-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="aab40-171">На hello **FirmPlay - представительство конфигурации о приеме на работу сотрудника** щелкните **FirmPlay Настройка - сотрудник представительство найму** tooopen **Настройкавхода**диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="aab40-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="aab40-174">tooget SSO настроен для вашего приложения, обратитесь в службу [FirmPlay - сотрудник представительство группа поддержки по найму](mailto:engineering@firmplay.com) и предоставить им hello следующее:</span><span class="sxs-lookup"><span data-stu-id="aab40-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="aab40-175">• hello загружены **файл сертификата**</span><span class="sxs-lookup"><span data-stu-id="aab40-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="aab40-176">• hello **SAML единого входа URL-адрес службы**</span><span class="sxs-lookup"><span data-stu-id="aab40-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="aab40-177">• hello **SAML идентификатор сущности**</span><span class="sxs-lookup"><span data-stu-id="aab40-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="aab40-178">• hello **URL-адрес выхода**</span><span class="sxs-lookup"><span data-stu-id="aab40-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aab40-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="aab40-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="aab40-180">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="aab40-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="aab40-182">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="aab40-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aab40-183">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="aab40-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aab40-185">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="aab40-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aab40-187">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="aab40-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aab40-189">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="aab40-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aab40-191">а.</span><span class="sxs-lookup"><span data-stu-id="aab40-191">a.</span></span> <span data-ttu-id="aab40-192">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aab40-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aab40-193">b.</span><span class="sxs-lookup"><span data-stu-id="aab40-193">b.</span></span> <span data-ttu-id="aab40-194">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aab40-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aab40-195">c.</span><span class="sxs-lookup"><span data-stu-id="aab40-195">c.</span></span> <span data-ttu-id="aab40-196">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="aab40-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aab40-197">d.</span><span class="sxs-lookup"><span data-stu-id="aab40-197">d.</span></span> <span data-ttu-id="aab40-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="aab40-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="aab40-199">Создание тестового пользователя FirmPlay — Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="aab40-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="aab40-200">В этом разделе вы создадите тестового пользователя FirmPlay — Employee Advocacy for Recruiting с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aab40-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="aab40-201">Обратитесь [FirmPlay - сотрудник представительство группа поддержки по найму](mailto:engineering@firmplay.com) tooadd пользователей hello в hello FirmPlay - сотрудник представительство найму платформы.</span><span class="sxs-lookup"><span data-stu-id="aab40-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aab40-202">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="aab40-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aab40-203">В этом разделе Включить toouse Britta Simon Azure единого входа, предоставляя свой доступ tooFirmPlay - представительство найму сотрудников.</span><span class="sxs-lookup"><span data-stu-id="aab40-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="aab40-205">**tooassign tooFirmPlay Britta Simon - сотрудник представительство найму, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="aab40-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="aab40-206">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="aab40-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="aab40-208">В списке приложений hello выберите **FirmPlay - сотрудник представительство найму**.</span><span class="sxs-lookup"><span data-stu-id="aab40-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="aab40-210">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="aab40-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="aab40-212">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="aab40-212">Click **Add** button.</span></span> <span data-ttu-id="aab40-213">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="aab40-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="aab40-215">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="aab40-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aab40-216">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="aab40-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aab40-217">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="aab40-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="aab40-218">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="aab40-218">Testing single sign-on</span></span>

<span data-ttu-id="aab40-219">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="aab40-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aab40-220">При нажатии кнопки hello FirmPlay - сотрудник представительство найму плитки в панели доступа hello следует получать автоматически вошедшего tooyour FirmPlay - приложение по найму представительство сотрудника.</span><span class="sxs-lookup"><span data-stu-id="aab40-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="aab40-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="aab40-221">Additional resources</span></span>

* [<span data-ttu-id="aab40-222">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aab40-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aab40-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aab40-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png