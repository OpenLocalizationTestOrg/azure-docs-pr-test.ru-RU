---
title: "Руководство. Интеграция Azure Active Directory с PlanMyLeave | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="ffacb-103">Руководство. Интеграция Azure Active Directory с PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="ffacb-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="ffacb-104">В этом учебнике вы узнаете, как toointegrate PlanMyLeave с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ffacb-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ffacb-105">Интеграция с Azure AD PlanMyLeave предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ffacb-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ffacb-106">Можно управлять в Azure AD, имеющего доступ tooPlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="ffacb-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="ffacb-107">Можно включить на пользователей tooautomatically get вошедшего tooPlanMyLeave (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffacb-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ffacb-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="ffacb-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="ffacb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ffacb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffacb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ffacb-110">Prerequisites</span></span>

<span data-ttu-id="ffacb-111">tooconfigure интеграция Azure AD с PlanMyLeave требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ffacb-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="ffacb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ffacb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ffacb-113">подписка PlanMyLeave с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ffacb-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="ffacb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ffacb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="ffacb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ffacb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ffacb-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="ffacb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ffacb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffacb-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ffacb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ffacb-118">Scenario description</span></span>
<span data-ttu-id="ffacb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ffacb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ffacb-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ffacb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ffacb-121">Добавление PlanMyLeave из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ffacb-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="ffacb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffacb-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="ffacb-123">Добавление PlanMyLeave из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ffacb-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="ffacb-124">tooconfigure hello интеграции PlanMyLeave в Azure AD, вы должны tooadd PlanMyLeave из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ffacb-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ffacb-125">**tooadd PlanMyLeave из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ffacb-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffacb-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ffacb-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ffacb-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ffacb-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ffacb-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ffacb-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ffacb-133">Введите в поле поиска hello **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="ffacb-135">В панели результатов hello выберите **PlanMyLeave**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ffacb-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ffacb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffacb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ffacb-138">В этом разделе описана настройка и проверка единого входа Azure AD в PlanMyLeave с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffacb-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ffacb-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PlanMyLeave является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffacb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="ffacb-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в PlanMyLeave должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ffacb-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="ffacb-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="ffacb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="ffacb-142">tooconfigure и теста Azure AD единого входа с PlanMyLeave, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ffacb-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ffacb-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ffacb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ffacb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ffacb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ffacb-145">**[Создание тестового пользователя PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave аналог Саймон Britta в PlanMyLeave, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="ffacb-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ffacb-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ffacb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ffacb-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ffacb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ffacb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffacb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ffacb-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="ffacb-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="ffacb-150">**tooconfigure Azure AD единого входа с PlanMyLeave, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ffacb-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffacb-151">На портале управления Azure hello на hello **PlanMyLeave** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ffacb-153">На hello **единого входа** странице диалогового окна как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ffacb-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="ffacb-155">На hello **URL-адреса и домена PlanMyLeave** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ffacb-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="ffacb-157">а.</span><span class="sxs-lookup"><span data-stu-id="ffacb-157">a.</span></span> <span data-ttu-id="ffacb-158">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="ffacb-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="ffacb-159">b.</span><span class="sxs-lookup"><span data-stu-id="ffacb-159">b.</span></span> <span data-ttu-id="ffacb-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="ffacb-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ffacb-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="ffacb-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="ffacb-162">У вас есть tooupdate входа эти значения с hello фактический URL-адрес и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ffacb-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="ffacb-163">Обратитесь к [PlanMyLeave поддержки](mailto:support@planmyleave.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ffacb-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="ffacb-164">На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="ffacb-166">На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="ffacb-167">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-167">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="ffacb-169">На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ffacb-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="ffacb-171">На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ffacb-173">На hello **сертификат подписи SAML** щелкните **сертификата (base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ffacb-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="ffacb-175">На hello **конфигурации PlanMyLeave** щелкните **Настройка PlanMyLeave** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ffacb-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="ffacb-178">В другом окне веб-браузера войдите в свой клиент PlanMyLeave в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ffacb-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="ffacb-179">Go слишком**настройки системы**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-179">Go too**System Setup**.</span></span> <span data-ttu-id="ffacb-180">Затем на hello **Управление безопасностью** щелкните **параметры SAML компании** .</span><span class="sxs-lookup"><span data-stu-id="ffacb-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="ffacb-182">На hello **параметры SAML** щелкните значок редактора.</span><span class="sxs-lookup"><span data-stu-id="ffacb-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="ffacb-184">На hello **обновления параметры SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ffacb-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="ffacb-186">а.</span><span class="sxs-lookup"><span data-stu-id="ffacb-186">a.</span></span>  <span data-ttu-id="ffacb-187">В hello **URL-адрес входа** текстовое поле, помещение значения hello **SAML единого входа URL-адрес службы** из окна конфигурации приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffacb-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="ffacb-188">b.</span><span class="sxs-lookup"><span data-stu-id="ffacb-188">b.</span></span>  <span data-ttu-id="ffacb-189">Откройте в блокноте файл загруженный сертификат, копировать только содержимое hello между hello---Begin Certificate---и---End certificate---его в буфер обмена, а затем вставьте его toohello **сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ffacb-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="ffacb-190">c.</span><span class="sxs-lookup"><span data-stu-id="ffacb-190">c.</span></span> <span data-ttu-id="ffacb-191">Значение»**включаются**«слишком»**Да**».</span><span class="sxs-lookup"><span data-stu-id="ffacb-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="ffacb-192">d.</span><span class="sxs-lookup"><span data-stu-id="ffacb-192">d.</span></span> <span data-ttu-id="ffacb-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ffacb-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffacb-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="ffacb-195">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ffacb-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ffacb-197">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ffacb-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffacb-198">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ffacb-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ffacb-200">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="ffacb-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ffacb-202">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ffacb-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ffacb-204">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ffacb-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ffacb-206">а.</span><span class="sxs-lookup"><span data-stu-id="ffacb-206">a.</span></span> <span data-ttu-id="ffacb-207">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ffacb-208">b.</span><span class="sxs-lookup"><span data-stu-id="ffacb-208">b.</span></span> <span data-ttu-id="ffacb-209">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ffacb-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ffacb-210">c.</span><span class="sxs-lookup"><span data-stu-id="ffacb-210">c.</span></span> <span data-ttu-id="ffacb-211">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ffacb-212">d.</span><span class="sxs-lookup"><span data-stu-id="ffacb-212">d.</span></span> <span data-ttu-id="ffacb-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="ffacb-214">Создание тестового пользователя PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="ffacb-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="ffacb-215">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="ffacb-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="ffacb-216">Приложение PlanMyLeave поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ffacb-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ffacb-217">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="ffacb-217">There is no action item for you in this section.</span></span> <span data-ttu-id="ffacb-218">Если он еще не существует во время попытки tooaccess PlanMyLeave создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="ffacb-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="ffacb-219">Если требуется toocreate пользователя вручную, необходимо toocontact [PlanMyLeave поддержки](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="ffacb-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ffacb-220">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ffacb-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ffacb-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooPlanMyLeave доступа.</span><span class="sxs-lookup"><span data-stu-id="ffacb-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ffacb-223">**tooassign tooPlanMyLeave Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ffacb-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffacb-224">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ffacb-226">В списке приложений hello выберите **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="ffacb-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ffacb-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-230">Click **Add** button.</span></span> <span data-ttu-id="ffacb-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ffacb-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ffacb-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ffacb-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ffacb-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="ffacb-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ffacb-236">Testing single sign-on</span></span>

<span data-ttu-id="ffacb-237">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ffacb-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ffacb-238">При нажатии кнопки hello PlanMyLeave плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour PlanMyLeave приложения.</span><span class="sxs-lookup"><span data-stu-id="ffacb-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ffacb-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ffacb-239">Additional resources</span></span>

* [<span data-ttu-id="ffacb-240">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffacb-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffacb-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ffacb-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png