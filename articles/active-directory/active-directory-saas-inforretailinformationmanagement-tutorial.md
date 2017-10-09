---
title: "Руководство. Интеграция Azure Active Directory с приложением Infor Retail – Information Management | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и сведения розничной торговли — управление информацией."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 9cd8ab65d41d01832e0611f7f8254aa257120508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="c7436-103">Руководство. Интеграция Azure Active Directory с приложением Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="c7436-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="c7436-104">В этом учебнике вы узнаете, как toointegrate сведения розничной торговли — управление информацией с помощью Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7436-104">In this tutorial, you learn how toointegrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7436-105">Интеграция сведения розничной торговли — управление информацией с помощью Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c7436-105">Integrating Infor Retail – Information Management with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7436-106">Можно управлять в Azure AD, имеющего доступ tooInfor розничной торговли — управление информацией.</span><span class="sxs-lookup"><span data-stu-id="c7436-106">You can control in Azure AD who has access tooInfor Retail – Information Management.</span></span>
- <span data-ttu-id="c7436-107">Можно включить на пользователей tooautomatically get вошедшего tooInfor розничной торговли — управление информацией (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7436-107">You can enable your users tooautomatically get signed-on tooInfor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c7436-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c7436-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c7436-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7436-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7436-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7436-110">Prerequisites</span></span>

<span data-ttu-id="c7436-111">Интеграция Azure AD с розничной торговли сведения — управление tooconfigure требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c7436-111">tooconfigure Azure AD integration with Infor Retail – Information Management, you need hello following items:</span></span>

- <span data-ttu-id="c7436-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c7436-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7436-113">подписка Infor Retail – Information Management с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c7436-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7436-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c7436-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7436-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c7436-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7436-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c7436-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7436-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7436-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7436-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c7436-118">Scenario description</span></span>
<span data-ttu-id="c7436-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c7436-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7436-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c7436-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7436-121">Добавление сведения розничной торговли — управление из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c7436-121">Adding Infor Retail – Information Management from hello gallery</span></span>
2. <span data-ttu-id="c7436-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7436-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-hello-gallery"></a><span data-ttu-id="c7436-123">Добавление сведения розничной торговли — управление из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c7436-123">Adding Infor Retail – Information Management from hello gallery</span></span>
<span data-ttu-id="c7436-124">Интеграция hello tooconfigure сведения розничной торговли — управление в Azure AD необходимо tooadd сведения розничной торговли — управление из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c7436-124">tooconfigure hello integration of Infor Retail – Information Management into Azure AD, you need tooadd Infor Retail – Information Management from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7436-125">**tooadd сведения розничной торговли — управление из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c7436-125">**tooadd Infor Retail – Information Management from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7436-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c7436-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="c7436-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c7436-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7436-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7436-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="c7436-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c7436-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="c7436-133">Введите в поле поиска hello **сведения розничной торговли — Управление сведениями о**выберите **сведения розничной торговли — Управление сведениями о** из панели результатов щелкните **добавить** hello tooadd кнопки приложение.</span><span class="sxs-lookup"><span data-stu-id="c7436-133">In hello search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Сведения розничной торговли — управления к данным в списке результатов hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c7436-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7436-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c7436-136">В этом разделе описывается настройка и проверка единого входа Azure AD в Infor Retail – Information Management с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7436-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7436-137">Для единого входа toowork Azure AD необходима tooknow, какой пользователь hello аналога в розничных сведения — Управление сведениями о tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7436-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Infor Retail – Information Management is tooa user in Azure AD.</span></span> <span data-ttu-id="c7436-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в розничных сведения — управление должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c7436-138">In other words, a link relationship between an Azure AD user and hello related user in Infor Retail – Information Management needs toobe established.</span></span>

<span data-ttu-id="c7436-139">В окончательных сведения — управление, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c7436-139">In Infor Retail – Information Management, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c7436-140">tooconfigure и теста Azure AD единого входа с розничной торговли сведения — управление сведения, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="c7436-140">tooconfigure and test Azure AD single sign-on with Infor Retail – Information Management, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7436-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c7436-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7436-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c7436-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7436-143">**[Создание розничных сведения — управление тестового пользователя](#create-an-infor-retail--information-management-test-user)**  - toohave аналог Саймон Britta розничных сведения — управление, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c7436-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - toohave a counterpart of Britta Simon in Infor Retail – Information Management that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7436-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c7436-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7436-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c7436-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c7436-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7436-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c7436-147">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в ваш розничных сведения — приложение для управления сведения.</span><span class="sxs-lookup"><span data-stu-id="c7436-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="c7436-148">**tooconfigure Azure AD единого входа с розничной торговли сведения — управление, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c7436-148">**tooconfigure Azure AD single sign-on with Infor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7436-149">В hello в hello портала Azure **сведения розничной торговли — Управление сведениями о** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c7436-149">In hello Azure portal, on hello **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="c7436-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c7436-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="c7436-153">На hello **сведения розничной торговли — URL-адреса и сведения о домене управления** выполните следующие шаги при необходимости приложение hello tooconfigure в IDP инициировал режим hello:</span><span class="sxs-lookup"><span data-stu-id="c7436-153">On hello **Infor Retail – Information Management Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Поставщик удостоверений со сведениями для единого входа в разделе "Домены и URL-адреса приложения Infor Retail – Information Management"](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="c7436-155">а.</span><span class="sxs-lookup"><span data-stu-id="c7436-155">a.</span></span> <span data-ttu-id="c7436-156">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="c7436-156">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="c7436-157">b.</span><span class="sxs-lookup"><span data-stu-id="c7436-157">b.</span></span> <span data-ttu-id="c7436-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="c7436-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="c7436-159">Проверьте **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг при желании tooconfigure приложения hello в hello **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="c7436-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Поставщика услуг со сведениями для единого входа в разделе "Домены и URL-адреса приложения Infor Retail – Information Management"](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="c7436-161">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="c7436-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c7436-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c7436-162">These values are not real.</span></span> <span data-ttu-id="c7436-163">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="c7436-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c7436-164">Обратитесь к [сведения розничной торговли — группа поддержки сведения клиент управления](mailto:innovate@infor.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="c7436-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) tooget these values.</span></span> 

5. <span data-ttu-id="c7436-165">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c7436-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="c7436-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c7436-167">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c7436-169">tooconfigure единого входа на **сведения розничной торговли — Управление сведениями о** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[сведения розничной торговли — группа поддержки управления к данным ](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="c7436-169">tooconfigure single sign-on on **Infor Retail – Information Management** side, you need toosend hello downloaded **Metadata XML** too[Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="c7436-170">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="c7436-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c7436-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c7436-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7436-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c7436-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7436-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7436-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c7436-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7436-174">Create an Azure AD test user</span></span>

<span data-ttu-id="c7436-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c7436-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="c7436-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c7436-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7436-178">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c7436-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c7436-180">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c7436-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c7436-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c7436-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c7436-184">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c7436-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c7436-186">а.</span><span class="sxs-lookup"><span data-stu-id="c7436-186">a.</span></span> <span data-ttu-id="c7436-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7436-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7436-188">b.</span><span class="sxs-lookup"><span data-stu-id="c7436-188">b.</span></span> <span data-ttu-id="c7436-189">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c7436-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c7436-190">c.</span><span class="sxs-lookup"><span data-stu-id="c7436-190">c.</span></span> <span data-ttu-id="c7436-191">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="c7436-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c7436-192">d.</span><span class="sxs-lookup"><span data-stu-id="c7436-192">d.</span></span> <span data-ttu-id="c7436-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c7436-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="c7436-194">Создание тестового пользователя Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="c7436-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="c7436-195">В этом разделе описано, как создать пользователя Britta Simon в приложении Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="c7436-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="c7436-196">Можно работать с [сведения розничной торговли — группа поддержки управления к данным](mailto:innovate@infor.com) tooadd пользователей hello в hello сведения розничной торговли — платформы управления к данным.</span><span class="sxs-lookup"><span data-stu-id="c7436-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) tooadd hello users in hello Infor Retail – Information Management platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c7436-197">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c7436-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c7436-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooInfor розничной торговли — управление информацией.</span><span class="sxs-lookup"><span data-stu-id="c7436-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInfor Retail – Information Management.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="c7436-200">**tooassign Britta Simon tooInfor розничной торговли — управление, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="c7436-200">**tooassign Britta Simon tooInfor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7436-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7436-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c7436-203">В списке приложений hello выберите **сведения розничной торговли — Управление сведениями о**.</span><span class="sxs-lookup"><span data-stu-id="c7436-203">In hello applications list, select **Infor Retail – Information Management**.</span></span>

    ![Hello сведения розничной торговли — Управление сведениями о связи в списке приложений hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="c7436-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c7436-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="c7436-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7436-207">Click **Add** button.</span></span> <span data-ttu-id="c7436-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c7436-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="c7436-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c7436-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7436-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c7436-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7436-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c7436-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c7436-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c7436-213">Test single sign-on</span></span>

<span data-ttu-id="c7436-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c7436-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c7436-215">При нажатии кнопки hello сведения розничной торговли — Управление сведениями о плитки в панели доступа hello следует получать автоматически вошедшего tooyour сведения розничной торговли — приложение для управления сведения.</span><span class="sxs-lookup"><span data-stu-id="c7436-215">When you click hello Infor Retail – Information Management tile in hello Access Panel, you should get automatically signed-on tooyour Infor Retail – Information Management application.</span></span>
<span data-ttu-id="c7436-216">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7436-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c7436-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c7436-217">Additional resources</span></span>

* [<span data-ttu-id="c7436-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7436-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7436-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7436-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png

