---
title: "Руководство по интеграции Azure Active Directory с RFPIO | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="25b0c-103">Руководство по интеграции Azure Active Directory с RFPIO</span><span class="sxs-lookup"><span data-stu-id="25b0c-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="25b0c-104">В этом учебнике вы узнаете, как toointegrate RFPIO с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25b0c-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25b0c-105">Интеграция с Azure AD RFPIO предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="25b0c-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="25b0c-106">Позволяет контролировать в Azure AD, имеющего доступ tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="25b0c-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="25b0c-107">Можно включить на пользователей tooautomatically get вошедшего tooRFPIO (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25b0c-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="25b0c-108">Вы можете управлять учетными записями в одном централизованном месте--hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="25b0c-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="25b0c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25b0c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25b0c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="25b0c-110">Prerequisites</span></span>

<span data-ttu-id="25b0c-111">tooconfigure интеграция Azure AD с RFPIO требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="25b0c-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="25b0c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="25b0c-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="25b0c-113">подписка RFPIO с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="25b0c-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="25b0c-114">Не рекомендуется использовать в этом учебнике шаги hello tootest в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="25b0c-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="25b0c-115">tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="25b0c-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="25b0c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="25b0c-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="25b0c-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25b0c-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25b0c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="25b0c-118">Scenario description</span></span>
<span data-ttu-id="25b0c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="25b0c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25b0c-120">сценарий Hello, описанные в этом учебнике состоит из двух основных компонентов.</span><span class="sxs-lookup"><span data-stu-id="25b0c-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25b0c-121">Добавление RFPIO из галереи hello.</span><span class="sxs-lookup"><span data-stu-id="25b0c-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="25b0c-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25b0c-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="25b0c-123">Добавление RFPIO из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="25b0c-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="25b0c-124">tooconfigure hello интеграции RFPIO в Azure AD, вы должны tooadd RFPIO из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="25b0c-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="25b0c-125">tooadd RFPIO из галереи hello</span><span class="sxs-lookup"><span data-stu-id="25b0c-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="25b0c-126">В hello  **[портал Azure](https://portal.azure.com)**, на левой панели навигации hello, выберите hello **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="25b0c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="25b0c-128">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="25b0c-130">tooadd нового приложения, выберите hello **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="25b0c-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="25b0c-132">Введите в поле поиска hello **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-132">In hello search box, type **RFPIO**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="25b0c-134">Hello панели результатов выберите **RFPIO**, а затем выберите hello **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="25b0c-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="25b0c-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="25b0c-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="25b0c-137">В этом разделе описана настройка и проверка единого входа Azure AD в приложение RFPIO с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25b0c-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25b0c-138">Для единого входа toowork Azure AD необходима tooknow какие hello отношение установлено между пользователя аналога в RFPIO и пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25b0c-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="25b0c-139">Другими словами связи между пользователя Azure AD и связанных пользователей hello в RFPIO должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="25b0c-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="25b0c-140">В RFPIO, присвойте значение hello **имя пользователя** в Azure AD в качестве значения hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="25b0c-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="25b0c-141">tooconfigure и теста Azure AD единого входа с RFPIO, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="25b0c-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="25b0c-142">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="25b0c-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="25b0c-143">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**--tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="25b0c-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25b0c-144">**[Создание тестового пользователя RFPIO](#creating-a-rfpio-test-user)**  --toohave аналог Саймон Britta в RFPIO, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="25b0c-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="25b0c-145">**[Назначить hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="25b0c-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25b0c-146">**[Тестирование единого входа](#testing-single-sign-on)**  tooverify--Если конфигурация hello работает.</span><span class="sxs-lookup"><span data-stu-id="25b0c-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="25b0c-147">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="25b0c-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="25b0c-148">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении RFPIO.</span><span class="sxs-lookup"><span data-stu-id="25b0c-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="25b0c-149">**tooconfigure Azure AD единого входа с RFPIO, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="25b0c-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="25b0c-150">В hello в hello портала Azure **RFPIO** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="25b0c-152">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="25b0c-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="25b0c-154">На hello **RFPIO доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="25b0c-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="25b0c-156">а.</span><span class="sxs-lookup"><span data-stu-id="25b0c-156">a.</span></span> <span data-ttu-id="25b0c-157">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="25b0c-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="25b0c-159">b.</span><span class="sxs-lookup"><span data-stu-id="25b0c-159">b.</span></span> <span data-ttu-id="25b0c-160">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="25b0c-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="25b0c-161">c.</span><span class="sxs-lookup"><span data-stu-id="25b0c-161">c.</span></span> <span data-ttu-id="25b0c-162">В hello **состояние ретрансляции** текстовом поле введите строковое значение.</span><span class="sxs-lookup"><span data-stu-id="25b0c-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="25b0c-163">Обратитесь к [RFPIO поддержки](https://www.rfpio.com/contact/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="25b0c-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="25b0c-164">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="25b0c-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="25b0c-165">При необходимости приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="25b0c-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="25b0c-167">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="25b0c-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="25b0c-168">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="25b0c-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="25b0c-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="25b0c-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="25b0c-172">В другом окне браузера, toohello входа **RFPIO** веб-сайта от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="25b0c-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="25b0c-173">Щелкните раскрывающийся список левом углу нижней hello.</span><span class="sxs-lookup"><span data-stu-id="25b0c-173">Click on hello bottom left corner dropdown.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="25b0c-175">Щелкните hello **параметры организации**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-175">Click on hello **Organization Settings**.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="25b0c-177">Щелкните hello **функции и ИНТЕГРАЦИИ**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="25b0c-179">В hello **Настройка единого входа SAML** щелкните **изменить**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="25b0c-181">В этом разделе выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="25b0c-181">In this Section perform following actions:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="25b0c-183">а.</span><span class="sxs-lookup"><span data-stu-id="25b0c-183">a.</span></span> <span data-ttu-id="25b0c-184">Скопируйте содержимое hello hello **загружены метаданные в формате XML** и вставьте его в hello **конфигурацию удостоверения** поля.</span><span class="sxs-lookup"><span data-stu-id="25b0c-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="25b0c-185">загрузить содержимое hello toocopy **метаданные в формате XML** используйте **Notepad ++** или правильную **редактора XML**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="25b0c-186">b.</span><span class="sxs-lookup"><span data-stu-id="25b0c-186">b.</span></span> <span data-ttu-id="25b0c-187">Щелкните **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-187">Click **Validate**.</span></span>

    <span data-ttu-id="25b0c-188">c.</span><span class="sxs-lookup"><span data-stu-id="25b0c-188">c.</span></span> <span data-ttu-id="25b0c-189">После нажатии кнопки **проверки**, зеркало **SAML(Enabled)** tooon.</span><span class="sxs-lookup"><span data-stu-id="25b0c-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="25b0c-190">d.</span><span class="sxs-lookup"><span data-stu-id="25b0c-190">d.</span></span> <span data-ttu-id="25b0c-191">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="25b0c-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="25b0c-192">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="25b0c-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="25b0c-193">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="25b0c-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="25b0c-194">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25b0c-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="25b0c-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="25b0c-195">Create an Azure AD test user</span></span>
<span data-ttu-id="25b0c-196">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="25b0c-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="25b0c-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="25b0c-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="25b0c-199">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="25b0c-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="25b0c-201">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="25b0c-203">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="25b0c-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25b0c-205">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="25b0c-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="25b0c-207">а.</span><span class="sxs-lookup"><span data-stu-id="25b0c-207">a.</span></span> <span data-ttu-id="25b0c-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25b0c-209">b.</span><span class="sxs-lookup"><span data-stu-id="25b0c-209">b.</span></span> <span data-ttu-id="25b0c-210">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="25b0c-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="25b0c-211">c.</span><span class="sxs-lookup"><span data-stu-id="25b0c-211">c.</span></span> <span data-ttu-id="25b0c-212">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="25b0c-213">d.</span><span class="sxs-lookup"><span data-stu-id="25b0c-213">d.</span></span> <span data-ttu-id="25b0c-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="25b0c-215">Создание тестового пользователя RFPIO</span><span class="sxs-lookup"><span data-stu-id="25b0c-215">Create a RFPIO test user</span></span>

<span data-ttu-id="25b0c-216">Пользователи toolog tooenable Azure AD в tooRFPIO, их необходимо подготовить в RFPIO.</span><span class="sxs-lookup"><span data-stu-id="25b0c-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="25b0c-217">В случае RFPIO hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="25b0c-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="25b0c-218">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="25b0c-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="25b0c-219">Войдите в систему tooyour RFPIO сайт компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="25b0c-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="25b0c-220">Щелкните раскрывающийся список левом углу нижней hello.</span><span class="sxs-lookup"><span data-stu-id="25b0c-220">Click on hello bottom left corner dropdown.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="25b0c-222">Щелкните hello **параметры организации**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-222">Click on hello **Organization Settings**.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="25b0c-224">Щелкните **TEAM MEMBERS** (Участники команды).</span><span class="sxs-lookup"><span data-stu-id="25b0c-224">Click **TEAM MEMBERS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="25b0c-226">Щелкните **ADD MEMBERS** (Добавить участников).</span><span class="sxs-lookup"><span data-stu-id="25b0c-226">Click on **ADD MEMBERS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="25b0c-228">В hello **добавить новые элементы** раздела.</span><span class="sxs-lookup"><span data-stu-id="25b0c-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="25b0c-229">выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="25b0c-229">Perform following actions:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="25b0c-231">а.</span><span class="sxs-lookup"><span data-stu-id="25b0c-231">a.</span></span> <span data-ttu-id="25b0c-232">Ввод **адрес электронной почты** в hello **введите один адрес электронной почты в строке** поля.</span><span class="sxs-lookup"><span data-stu-id="25b0c-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="25b0c-233">b.</span><span class="sxs-lookup"><span data-stu-id="25b0c-233">b.</span></span> <span data-ttu-id="25b0c-234">Выберите **роль** в соответствии с требованиями.</span><span class="sxs-lookup"><span data-stu-id="25b0c-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="25b0c-235">c.</span><span class="sxs-lookup"><span data-stu-id="25b0c-235">c.</span></span> <span data-ttu-id="25b0c-236">Щелкните **ADD MEMBERS** (Добавить участников).</span><span class="sxs-lookup"><span data-stu-id="25b0c-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="25b0c-237">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="25b0c-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="25b0c-238">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="25b0c-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="25b0c-239">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooRFPIO доступа.</span><span class="sxs-lookup"><span data-stu-id="25b0c-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="25b0c-241">**tooassign tooRFPIO Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="25b0c-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="25b0c-242">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="25b0c-244">В списке приложений hello выберите **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-244">In hello applications list, select **RFPIO**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="25b0c-246">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="25b0c-248">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-248">Click **Add** button.</span></span> <span data-ttu-id="25b0c-249">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="25b0c-251">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="25b0c-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="25b0c-252">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25b0c-253">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="25b0c-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="25b0c-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="25b0c-254">Test single sign-on</span></span>

<span data-ttu-id="25b0c-255">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="25b0c-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="25b0c-256">При нажатии кнопки RFPIO плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour RFPIO приложения.</span><span class="sxs-lookup"><span data-stu-id="25b0c-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="25b0c-257">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="25b0c-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25b0c-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="25b0c-258">Additional resources</span></span>

* [<span data-ttu-id="25b0c-259">Список учебников о том, как toointegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25b0c-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25b0c-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="25b0c-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

