---
title: "Руководство. Интеграция Azure Active Directory с MaxxPoint | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и MaxxPoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 03b13908add8d8c62f1d1480ed2288658fce14d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="45cf5-103">Руководство. Интеграция Azure Active Directory с MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="45cf5-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="45cf5-104">В этом учебнике вы узнаете, как toointegrate MaxxPoint с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="45cf5-104">In this tutorial, you learn how toointegrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45cf5-105">Интеграция с Azure AD MaxxPoint предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="45cf5-105">Integrating MaxxPoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="45cf5-106">Можно управлять в Azure AD, имеющего доступ tooMaxxPoint</span><span class="sxs-lookup"><span data-stu-id="45cf5-106">You can control in Azure AD who has access tooMaxxPoint</span></span>
- <span data-ttu-id="45cf5-107">Можно включить на пользователей tooautomatically get вошедшего tooMaxxPoint (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="45cf5-107">You can enable your users tooautomatically get signed-on tooMaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="45cf5-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="45cf5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="45cf5-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45cf5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45cf5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="45cf5-110">Prerequisites</span></span>

<span data-ttu-id="45cf5-111">tooconfigure интеграция Azure AD с MaxxPoint требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="45cf5-111">tooconfigure Azure AD integration with MaxxPoint, you need hello following items:</span></span>

- <span data-ttu-id="45cf5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="45cf5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="45cf5-113">подписка MaxxPoint с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="45cf5-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="45cf5-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="45cf5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="45cf5-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="45cf5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45cf5-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="45cf5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="45cf5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45cf5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45cf5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="45cf5-118">Scenario description</span></span>
<span data-ttu-id="45cf5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="45cf5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45cf5-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="45cf5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45cf5-121">Добавление MaxxPoint из галереи hello</span><span class="sxs-lookup"><span data-stu-id="45cf5-121">Adding MaxxPoint from hello gallery</span></span>
2. <span data-ttu-id="45cf5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="45cf5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-hello-gallery"></a><span data-ttu-id="45cf5-123">Добавление MaxxPoint из галереи hello</span><span class="sxs-lookup"><span data-stu-id="45cf5-123">Adding MaxxPoint from hello gallery</span></span>
<span data-ttu-id="45cf5-124">tooconfigure hello интеграции MaxxPoint в Azure AD, вы должны tooadd MaxxPoint из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="45cf5-124">tooconfigure hello integration of MaxxPoint into Azure AD, you need tooadd MaxxPoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="45cf5-125">**tooadd MaxxPoint из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="45cf5-125">**tooadd MaxxPoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="45cf5-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="45cf5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="45cf5-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="45cf5-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="45cf5-131">Нажмите кнопку **новое приложение** кнопку на hello верхней части диалогового окна tooadd новое приложение.</span><span class="sxs-lookup"><span data-stu-id="45cf5-131">Click **New application** button on hello top of dialog tooadd new application.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="45cf5-133">Введите в поле поиска hello **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-133">In hello search box, type **MaxxPoint**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="45cf5-135">В панели результатов hello выберите **MaxxPoint**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="45cf5-135">In hello results panel, select **MaxxPoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45cf5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="45cf5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45cf5-138">В этом разделе описана настройка и проверка единого входа Azure AD в MaxxPoint с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="45cf5-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="45cf5-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в MaxxPoint является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45cf5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MaxxPoint is tooa user in Azure AD.</span></span> <span data-ttu-id="45cf5-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в MaxxPoint должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="45cf5-140">In other words, a link relationship between an Azure AD user and hello related user in MaxxPoint needs toobe established.</span></span>

<span data-ttu-id="45cf5-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="45cf5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in MaxxPoint.</span></span>

<span data-ttu-id="45cf5-142">tooconfigure и теста Azure AD единого входа с MaxxPoint, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="45cf5-142">tooconfigure and test Azure AD single sign-on with MaxxPoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="45cf5-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="45cf5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="45cf5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="45cf5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="45cf5-145">**[Создание тестового пользователя MaxxPoint](#creating-a-maxxpoint-test-user)**  -toohave аналог Саймон Britta в MaxxPoint, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="45cf5-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - toohave a counterpart of Britta Simon in MaxxPoint that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="45cf5-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="45cf5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="45cf5-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="45cf5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="45cf5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="45cf5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="45cf5-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="45cf5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="45cf5-150">**tooconfigure Azure AD единого входа с MaxxPoint, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="45cf5-150">**tooconfigure Azure AD single sign-on with MaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="45cf5-151">В hello в hello портала Azure **MaxxPoint** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-151">In hello Azure portal, on hello **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="45cf5-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="45cf5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="45cf5-155">На hello **URL-адреса и домена MaxxPoint** статьи, при желании tooconfigure приложения hello в **инициированный IDP режим**, но не требуются какие-либо шаги tooperform.</span><span class="sxs-lookup"><span data-stu-id="45cf5-155">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, no need tooperform any steps.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="45cf5-157">На hello **URL-адреса и домена MaxxPoint** статьи, при желании tooconfigure приложения hello в **режиме, инициируемая SP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="45cf5-157">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="45cf5-159">а.</span><span class="sxs-lookup"><span data-stu-id="45cf5-159">a.</span></span> <span data-ttu-id="45cf5-160">Выберите параметр **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="45cf5-161">b.</span><span class="sxs-lookup"><span data-stu-id="45cf5-161">b.</span></span> <span data-ttu-id="45cf5-162">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="45cf5-162">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="45cf5-163">Обратите внимание на то, что это не Вещественное значение hello.</span><span class="sxs-lookup"><span data-stu-id="45cf5-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="45cf5-164">У вас есть tooupdate это значение с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="45cf5-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="45cf5-165">Вызов команды MaxxPoint на **888-728-0950** tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="45cf5-165">Call MaxxPoint team on **888-728-0950** tooget this value.</span></span>

5. <span data-ttu-id="45cf5-166">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="45cf5-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="45cf5-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="45cf5-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="45cf5-170">tooget SSO настроен для вашего приложения, вызывать службу поддержки MaxxPoint для **888-728-0950** и они будут поможет дальнейшей на способа загрузки их hello tooprovide **метаданные в формате XML** файла.</span><span class="sxs-lookup"><span data-stu-id="45cf5-170">tooget SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how tooprovide them hello downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="45cf5-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="45cf5-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="45cf5-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="45cf5-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="45cf5-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="45cf5-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45cf5-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="45cf5-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="45cf5-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="45cf5-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="45cf5-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="45cf5-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="45cf5-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="45cf5-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="45cf5-180">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="45cf5-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="45cf5-182">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="45cf5-182">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45cf5-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="45cf5-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="45cf5-186">а.</span><span class="sxs-lookup"><span data-stu-id="45cf5-186">a.</span></span> <span data-ttu-id="45cf5-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="45cf5-188">b.</span><span class="sxs-lookup"><span data-stu-id="45cf5-188">b.</span></span> <span data-ttu-id="45cf5-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="45cf5-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="45cf5-190">c.</span><span class="sxs-lookup"><span data-stu-id="45cf5-190">c.</span></span> <span data-ttu-id="45cf5-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="45cf5-192">d.</span><span class="sxs-lookup"><span data-stu-id="45cf5-192">d.</span></span> <span data-ttu-id="45cf5-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="45cf5-194">Создание тестового пользователя MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="45cf5-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="45cf5-195">В этом разделе описано, как создать пользователя Britta Simon в приложении MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="45cf5-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="45cf5-196">Обратитесь в службу поддержки MaxxPoint на **888-728-0950** tooadd пользователей hello в hello MaxxPoint приложения.</span><span class="sxs-lookup"><span data-stu-id="45cf5-196">Please call MaxxPoint support team on **888-728-0950** tooadd hello users in hello MaxxPoint application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="45cf5-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="45cf5-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="45cf5-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooMaxxPoint доступа.</span><span class="sxs-lookup"><span data-stu-id="45cf5-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooMaxxPoint.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="45cf5-200">**tooassign tooMaxxPoint Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="45cf5-200">**tooassign Britta Simon tooMaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="45cf5-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="45cf5-203">В списке приложений hello выберите **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-203">In hello applications list, select **MaxxPoint**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="45cf5-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="45cf5-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-207">Click **Add** button.</span></span> <span data-ttu-id="45cf5-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="45cf5-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="45cf5-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="45cf5-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45cf5-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="45cf5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="45cf5-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="45cf5-213">Testing single sign-on</span></span>

<span data-ttu-id="45cf5-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="45cf5-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="45cf5-215">При нажатии кнопки hello MaxxPoint плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour MaxxPoint приложения.</span><span class="sxs-lookup"><span data-stu-id="45cf5-215">When you click hello MaxxPoint tile in hello Access Panel, you should get automatically signed-on tooyour MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="45cf5-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="45cf5-216">Additional resources</span></span>

* [<span data-ttu-id="45cf5-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45cf5-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45cf5-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="45cf5-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png