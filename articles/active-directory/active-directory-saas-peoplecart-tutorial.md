---
title: "Руководство по интеграции Azure Active Directory с Peoplecart | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Peoplecart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 481c7246a63f669ab39cb4ec652cebf40ba35f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="f8dc0-103">Руководство по интеграции Azure Active Directory с Peoplecart</span><span class="sxs-lookup"><span data-stu-id="f8dc0-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="f8dc0-104">В этом учебнике вы узнаете, как toointegrate Peoplecart с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-104">In this tutorial, you learn how toointegrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8dc0-105">Интеграция с Azure AD Peoplecart предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-105">Integrating Peoplecart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f8dc0-106">Можно управлять в Azure AD, имеющего доступ tooPeoplecart</span><span class="sxs-lookup"><span data-stu-id="f8dc0-106">You can control in Azure AD who has access tooPeoplecart</span></span>
- <span data-ttu-id="f8dc0-107">Можно включить на пользователей tooautomatically get вошедшего tooPeoplecart (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8dc0-107">You can enable your users tooautomatically get signed-on tooPeoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8dc0-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f8dc0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f8dc0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8dc0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f8dc0-110">Prerequisites</span></span>

<span data-ttu-id="f8dc0-111">tooconfigure интеграция Azure AD с Peoplecart требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-111">tooconfigure Azure AD integration with Peoplecart, you need hello following items:</span></span>

- <span data-ttu-id="f8dc0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f8dc0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8dc0-113">подписка Peoplecart с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8dc0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8dc0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8dc0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8dc0-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8dc0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f8dc0-118">Scenario description</span></span>
<span data-ttu-id="f8dc0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8dc0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8dc0-121">Добавление Peoplecart из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f8dc0-121">Adding Peoplecart from hello gallery</span></span>
2. <span data-ttu-id="f8dc0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8dc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-hello-gallery"></a><span data-ttu-id="f8dc0-123">Добавление Peoplecart из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f8dc0-123">Adding Peoplecart from hello gallery</span></span>
<span data-ttu-id="f8dc0-124">tooconfigure hello интеграции Peoplecart в Azure AD, вы должны tooadd Peoplecart из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-124">tooconfigure hello integration of Peoplecart into Azure AD, you need tooadd Peoplecart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f8dc0-125">**tooadd Peoplecart из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-125">**tooadd Peoplecart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8dc0-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="f8dc0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f8dc0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="f8dc0-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="f8dc0-133">Введите в поле поиска hello **Peoplecart**выберите **Peoplecart** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-133">In hello search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Peoplecart в списке результатов hello](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f8dc0-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8dc0-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f8dc0-136">В этом разделе описана настройка и проверка единого входа Azure AD в Peoplecart с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f8dc0-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Peoplecart является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Peoplecart is tooa user in Azure AD.</span></span> <span data-ttu-id="f8dc0-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Peoplecart должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-138">In other words, a link relationship between an Azure AD user and hello related user in Peoplecart needs toobe established.</span></span>

<span data-ttu-id="f8dc0-139">В Peoplecart, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-139">In Peoplecart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f8dc0-140">tooconfigure и теста Azure AD единого входа с Peoplecart, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-140">tooconfigure and test Azure AD single sign-on with Peoplecart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f8dc0-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f8dc0-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8dc0-143">**[Создание тестового пользователя Peoplecart](#create-a-peoplecart-test-user)**  -toohave аналог Саймон Britta в Peoplecart, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - toohave a counterpart of Britta Simon in Peoplecart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8dc0-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8dc0-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f8dc0-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8dc0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f8dc0-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="f8dc0-148">**tooconfigure Azure AD единого входа с Peoplecart, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-148">**tooconfigure Azure AD single sign-on with Peoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8dc0-149">В hello в hello портала Azure **Peoplecart** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-149">In hello Azure portal, on hello **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f8dc0-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="f8dc0-153">На hello **URL-адреса и домена Peoplecart** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-153">On hello **Peoplecart Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="f8dc0-155">а.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-155">a.</span></span> <span data-ttu-id="f8dc0-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="f8dc0-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="f8dc0-157">b.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-157">b.</span></span> <span data-ttu-id="f8dc0-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="f8dc0-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f8dc0-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-159">These values are not real.</span></span> <span data-ttu-id="f8dc0-160">Обновить эти значения с hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-160">Update these values with hello actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="f8dc0-161">Обратитесь к [группа поддержки клиента Peoplecart](https://peoplecart.com/ContactUs.aspx) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) tooget these values.</span></span> 
 
4. <span data-ttu-id="f8dc0-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="f8dc0-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f8dc0-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f8dc0-166">На hello **конфигурации Peoplecart** щелкните **Настройка Peoplecart** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-166">On hello **Peoplecart Configuration** section, click **Configure Peoplecart** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f8dc0-167">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="f8dc0-169">tooconfigure единого входа на **Peoplecart** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **SAML единого входа URL-адрес службы** слишком[ Группа поддержки Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-169">tooconfigure single sign-on on **Peoplecart** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="f8dc0-170">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f8dc0-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f8dc0-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f8dc0-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f8dc0-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8dc0-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f8dc0-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8dc0-174">Create an Azure AD test user</span></span>
<span data-ttu-id="f8dc0-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="f8dc0-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8dc0-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8dc0-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8dc0-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f8dc0-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8dc0-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8dc0-186">а.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-186">a.</span></span> <span data-ttu-id="f8dc0-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8dc0-188">b.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-188">b.</span></span> <span data-ttu-id="f8dc0-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8dc0-190">c.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-190">c.</span></span> <span data-ttu-id="f8dc0-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f8dc0-192">d.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-192">d.</span></span> <span data-ttu-id="f8dc0-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="f8dc0-194">Создание тестового пользователя Peoplecart</span><span class="sxs-lookup"><span data-stu-id="f8dc0-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="f8dc0-195">В этом разделе описано, как создать пользователя Britta Simon в приложении Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="f8dc0-196">Работать с [Peoplecart поддержки](https://peoplecart.com/ContactUs.aspx) tooadd hello пользователей на платформе Peoplecart hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) tooadd hello users in hello Peoplecart platform.</span></span> <span data-ttu-id="f8dc0-197">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f8dc0-198">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f8dc0-198">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f8dc0-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPeoplecart доступа.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeoplecart.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="f8dc0-201">**tooassign tooPeoplecart Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-201">**tooassign Britta Simon tooPeoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8dc0-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f8dc0-204">В списке приложений hello выберите **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-204">In hello applications list, select **Peoplecart**.</span></span>

    ![ссылка Peoplecart Hello в списке приложений hello](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="f8dc0-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="f8dc0-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-208">Click **Add** button.</span></span> <span data-ttu-id="f8dc0-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="f8dc0-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f8dc0-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8dc0-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f8dc0-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f8dc0-214">Test single sign-on</span></span>

<span data-ttu-id="f8dc0-215">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f8dc0-216">При нажатии кнопки hello Peoplecart плитки в панели доступа hello, должно появиться страница входа Peoplecart приложения.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-216">When you click hello Peoplecart tile in hello Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="f8dc0-217">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8dc0-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f8dc0-218">Additional resources</span></span>

* [<span data-ttu-id="f8dc0-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8dc0-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8dc0-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8dc0-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

