---
title: "Руководство по интеграции Azure Active Directory с Tangoe Command Premium Mobile | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Tangoe команда Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="0cf77-103">Учебник. Интеграция Azure Active Directory с Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="0cf77-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="0cf77-104">В этом учебнике вы узнаете, как toointegrate Tangoe команда Premium мобильные приложения с помощью Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0cf77-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0cf77-105">Интеграция с Azure AD Premium Mobile Tangoe команда предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0cf77-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0cf77-106">Можно управлять в Azure AD, имеющего доступ tooTangoe Mobile Premium команды</span><span class="sxs-lookup"><span data-stu-id="0cf77-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="0cf77-107">Ваш пользователей tooautomatically get вошедшего tooTangoe Mobile Premium команды (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf77-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0cf77-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0cf77-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0cf77-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0cf77-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cf77-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0cf77-110">Prerequisites</span></span>

<span data-ttu-id="0cf77-111">tooconfigure интеграция Azure AD с Mobile Premium команда Tangoe требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0cf77-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="0cf77-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0cf77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0cf77-113">подписка Tangoe Command Premium Mobile с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0cf77-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0cf77-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0cf77-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0cf77-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0cf77-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0cf77-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0cf77-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0cf77-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0cf77-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0cf77-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0cf77-118">Scenario description</span></span>
<span data-ttu-id="0cf77-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0cf77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0cf77-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0cf77-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0cf77-121">Добавление мобильных Premium Tangoe команды из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="0cf77-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="0cf77-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf77-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="0cf77-123">Добавление мобильных Premium Tangoe команды из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="0cf77-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="0cf77-124">tooconfigure hello интеграции Mobile Premium Tangoe команды в Azure AD, вы должны tooadd Mobile Premium Tangoe команды из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0cf77-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0cf77-125">**tooadd Tangoe Mobile Premium команды из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="0cf77-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf77-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0cf77-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0cf77-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0cf77-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0cf77-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0cf77-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0cf77-133">Введите в поле поиска hello **Tangoe команда Premium Mobile**выберите **Mobile Premium команда Tangoe** из панели «результат» нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0cf77-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="0cf77-134">Добавление Tangoe Command Premium Mobile из коллекции</span><span class="sxs-lookup"><span data-stu-id="0cf77-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0cf77-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf77-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0cf77-136">В этом разделе описана настройка и проверка единого входа Azure AD в Tangoe Command Premium Mobile с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0cf77-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0cf77-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Tangoe команда Premium Mobile является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cf77-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="0cf77-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Tangoe команда Premium Mobile должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0cf77-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="0cf77-139">В мобильных Premium Tangoe команды, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="0cf77-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0cf77-140">tooconfigure и тестирования Azure AD единого входа с Mobile Premium Tangoe команды, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="0cf77-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0cf77-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0cf77-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0cf77-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0cf77-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0cf77-143">**[Создание тестового пользователя Mobile Premium команда Tangoe](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave аналог Саймон Britta в Tangoe команда Premium Mobile, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="0cf77-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0cf77-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0cf77-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0cf77-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0cf77-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0cf77-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf77-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0cf77-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Tangoe команда Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="0cf77-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="0cf77-148">**tooconfigure Azure AD единого входа с мобильных устройств Tangoe команда Premium, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0cf77-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf77-149">В hello в hello портала Azure **Mobile Premium команда Tangoe** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0cf77-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0cf77-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="0cf77-153">На hello **Tangoe команда Premium Mobile домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0cf77-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![Домены и URL-адреса приложения Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="0cf77-155">а.</span><span class="sxs-lookup"><span data-stu-id="0cf77-155">a.</span></span> <span data-ttu-id="0cf77-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="0cf77-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="0cf77-157">b.</span><span class="sxs-lookup"><span data-stu-id="0cf77-157">b.</span></span> <span data-ttu-id="0cf77-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="0cf77-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0cf77-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0cf77-159">These values are not real.</span></span> <span data-ttu-id="0cf77-160">Обновите эти значения с hello фактический URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="0cf77-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="0cf77-161">Обратитесь к [Tangoe команда Premium мобильного клиента поддержки](https://www.tangoe.com/contact-2/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="0cf77-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="0cf77-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0cf77-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="0cf77-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0cf77-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="0cf77-166">На hello **конфигурация мобильных Premium команда Tangoe** щелкните **Настройка Mobile Premium Tangoe команда** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="0cf77-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0cf77-167">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="0cf77-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Раздел настройки Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="0cf77-169">tooget SSO настроен для вашего приложения, обратитесь в службу вашей [группа поддержки Tangoe команда Premium мобильного клиента](https://www.tangoe.com/contact-2/) и предоставляют hello следующее:</span><span class="sxs-lookup"><span data-stu-id="0cf77-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="0cf77-170">Hello скачанный файл метаданных</span><span class="sxs-lookup"><span data-stu-id="0cf77-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="0cf77-171">Hello **SAML идентификатор сущности**</span><span class="sxs-lookup"><span data-stu-id="0cf77-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="0cf77-172">Hello **SAML единого входа URL-адрес службы**</span><span class="sxs-lookup"><span data-stu-id="0cf77-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="0cf77-173">Hello **URL-адрес выхода**</span><span class="sxs-lookup"><span data-stu-id="0cf77-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="0cf77-174">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="0cf77-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0cf77-175">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0cf77-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0cf77-176">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0cf77-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0cf77-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf77-177">Create an Azure AD test user</span></span>
<span data-ttu-id="0cf77-178">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0cf77-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0cf77-180">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0cf77-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf77-181">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0cf77-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0cf77-183">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Выберите "Пользователи и группы" > "Все пользователи".](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0cf77-185">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="0cf77-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Добавить пользователя](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0cf77-187">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0cf77-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0cf77-189">а.</span><span class="sxs-lookup"><span data-stu-id="0cf77-189">a.</span></span> <span data-ttu-id="0cf77-190">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0cf77-191">b.</span><span class="sxs-lookup"><span data-stu-id="0cf77-191">b.</span></span> <span data-ttu-id="0cf77-192">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0cf77-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0cf77-193">c.</span><span class="sxs-lookup"><span data-stu-id="0cf77-193">c.</span></span> <span data-ttu-id="0cf77-194">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0cf77-195">d.</span><span class="sxs-lookup"><span data-stu-id="0cf77-195">d.</span></span> <span data-ttu-id="0cf77-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="0cf77-197">Создание тестового пользователя Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="0cf77-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="0cf77-198">В этом разделе мы создадим пользователя Britta Simon в приложении Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="0cf77-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="0cf77-199">Mobile Premium команда Tangoe приложению все пользователи toobe hello, подготовить в приложении hello перед выполнением единого входа.</span><span class="sxs-lookup"><span data-stu-id="0cf77-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="0cf77-200">Так что произведите работы с hello [Tangoe команда Premium мобильного клиента поддержки](https://www.tangoe.com/contact-2/) tooprovision этих пользователей в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="0cf77-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0cf77-201">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0cf77-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0cf77-202">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooTangoe Mobile Premium команды.</span><span class="sxs-lookup"><span data-stu-id="0cf77-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0cf77-204">**tooassign tooTangoe Britta Simon команда мобильных Premium, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="0cf77-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf77-205">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0cf77-207">В списке приложений hello выберите **Mobile Premium команды Tangoe**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile в списке приложений](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="0cf77-209">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0cf77-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-211">Click **Add** button.</span></span> <span data-ttu-id="0cf77-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0cf77-214">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0cf77-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0cf77-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0cf77-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0cf77-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0cf77-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0cf77-217">Test single sign-on</span></span>

<span data-ttu-id="0cf77-218">В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0cf77-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0cf77-219">Если щелкнуть плитку Tangoe команда Premium Mobile hello в hello панели доступа, следует получать автоматически вошедшего tooyour Tangoe команда Premium мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="0cf77-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="0cf77-220">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0cf77-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0cf77-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0cf77-221">Additional resources</span></span>

* [<span data-ttu-id="0cf77-222">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0cf77-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0cf77-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0cf77-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

