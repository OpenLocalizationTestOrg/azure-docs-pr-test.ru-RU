---
title: "Учебник. Интеграция Azure Active Directory с Cornerstone OnDemand | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с Cornerstone OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 85fd6eb4e93010d8f7477df236403e205e9f2d83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="eaeda-103">Руководство. Интеграция Azure Active Directory с Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="eaeda-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="eaeda-104">В этом учебнике вы узнаете, как toointegrate Cornerstone OnDemand с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eaeda-104">In this tutorial, you learn how toointegrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eaeda-105">Интеграция Cornerstone OnDemand с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="eaeda-105">Integrating Cornerstone OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eaeda-106">Можно управлять в Azure AD, имеющего доступ tooCornerstone по запросу</span><span class="sxs-lookup"><span data-stu-id="eaeda-106">You can control in Azure AD who has access tooCornerstone OnDemand</span></span>
- <span data-ttu-id="eaeda-107">Можно включить на пользователей tooautomatically get вошедшего tooCornerstone OnDemand (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeda-107">You can enable your users tooautomatically get signed-on tooCornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eaeda-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="eaeda-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eaeda-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eaeda-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eaeda-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="eaeda-110">Prerequisites</span></span>

<span data-ttu-id="eaeda-111">tooconfigure интеграция Azure AD с Cornerstone OnDemand требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="eaeda-111">tooconfigure Azure AD integration with Cornerstone OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="eaeda-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="eaeda-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eaeda-113">подписка Cornerstone OnDemand с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="eaeda-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eaeda-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="eaeda-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eaeda-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="eaeda-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eaeda-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="eaeda-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eaeda-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eaeda-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eaeda-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="eaeda-118">Scenario description</span></span>
<span data-ttu-id="eaeda-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="eaeda-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eaeda-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="eaeda-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eaeda-121">Добавление Cornerstone OnDemand из галереи hello</span><span class="sxs-lookup"><span data-stu-id="eaeda-121">Adding Cornerstone OnDemand from hello gallery</span></span>
2. <span data-ttu-id="eaeda-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeda-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-hello-gallery"></a><span data-ttu-id="eaeda-123">Добавление Cornerstone OnDemand из галереи hello</span><span class="sxs-lookup"><span data-stu-id="eaeda-123">Adding Cornerstone OnDemand from hello gallery</span></span>
<span data-ttu-id="eaeda-124">tooconfigure hello интеграции Cornerstone OnDemand в Azure AD, вы должны tooadd Cornerstone OnDemand из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="eaeda-124">tooconfigure hello integration of Cornerstone OnDemand into Azure AD, you need tooadd Cornerstone OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eaeda-125">**tooadd Cornerstone OnDemand из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="eaeda-125">**tooadd Cornerstone OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeda-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="eaeda-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eaeda-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eaeda-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="eaeda-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="eaeda-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="eaeda-133">Введите в поле поиска hello **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-133">In hello search box, type **Cornerstone OnDemand**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="eaeda-135">В панели результатов hello выберите **Cornerstone OnDemand**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="eaeda-135">In hello results panel, select **Cornerstone OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eaeda-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeda-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eaeda-138">В этом разделе описана настройка и проверка единого входа Azure AD в Cornerstone OnDemand для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eaeda-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eaeda-139">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в Cornerstone OnDemand — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaeda-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cornerstone OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="eaeda-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Cornerstone OnDemand должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="eaeda-140">In other words, a link relationship between an Azure AD user and hello related user in Cornerstone OnDemand needs toobe established.</span></span>

<span data-ttu-id="eaeda-141">В Cornerstone OnDemand, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="eaeda-141">In Cornerstone OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eaeda-142">tooconfigure и теста Azure AD единого входа с Cornerstone OnDemand, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="eaeda-142">tooconfigure and test Azure AD single sign-on with Cornerstone OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eaeda-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="eaeda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eaeda-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="eaeda-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eaeda-145">**[Создание тестового пользователя Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)**  -toohave аналог Саймон Britta в Cornerstone OnDemand, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="eaeda-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - toohave a counterpart of Britta Simon in Cornerstone OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eaeda-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="eaeda-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eaeda-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eaeda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eaeda-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeda-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eaeda-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="eaeda-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="eaeda-150">**tooconfigure Azure AD единого входа с Cornerstone OnDemand, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="eaeda-150">**tooconfigure Azure AD single sign-on with Cornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeda-151">В hello в hello портала Azure **Cornerstone OnDemand** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-151">In hello Azure portal, on hello **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="eaeda-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="eaeda-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="eaeda-155">На hello **Cornerstone OnDemand доменов и URL-адреса** выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="eaeda-155">On hello **Cornerstone OnDemand Domain and URLs** section, perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="eaeda-157">а.</span><span class="sxs-lookup"><span data-stu-id="eaeda-157">a.</span></span> <span data-ttu-id="eaeda-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="eaeda-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="eaeda-159">b.</span><span class="sxs-lookup"><span data-stu-id="eaeda-159">b.</span></span> <span data-ttu-id="eaeda-160">В **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="eaeda-160">In **Identifier** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eaeda-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="eaeda-161">These values are not real.</span></span> <span data-ttu-id="eaeda-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="eaeda-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eaeda-163">Обратитесь к [группа поддержки Cornerstone OnDemand клиента](mailTo:moreinfo@csod.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="eaeda-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="eaeda-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="eaeda-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="eaeda-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="eaeda-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eaeda-168">На hello **Cornerstone OnDemand конфигурации** щелкните **Настройка Cornerstone OnDemand** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="eaeda-168">On hello **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eaeda-169">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="eaeda-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="eaeda-171">tooconfigure единого входа на **Cornerstone OnDemand** стороны, необходимо загрузить hello toosend **сертификат**, **URL-адрес выхода** и **один SAML Вход URL-адрес службы** слишком[поддержки Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="eaeda-171">tooconfigure single sign-on on **Cornerstone OnDemand** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  too[Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="eaeda-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="eaeda-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eaeda-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="eaeda-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eaeda-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="eaeda-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eaeda-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eaeda-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eaeda-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeda-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="eaeda-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="eaeda-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="eaeda-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="eaeda-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeda-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="eaeda-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eaeda-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eaeda-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="eaeda-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eaeda-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="eaeda-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eaeda-188">а.</span><span class="sxs-lookup"><span data-stu-id="eaeda-188">a.</span></span> <span data-ttu-id="eaeda-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eaeda-190">b.</span><span class="sxs-lookup"><span data-stu-id="eaeda-190">b.</span></span> <span data-ttu-id="eaeda-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eaeda-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eaeda-192">c.</span><span class="sxs-lookup"><span data-stu-id="eaeda-192">c.</span></span> <span data-ttu-id="eaeda-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eaeda-194">d.</span><span class="sxs-lookup"><span data-stu-id="eaeda-194">d.</span></span> <span data-ttu-id="eaeda-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="eaeda-196">Создание тестового пользователя Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="eaeda-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="eaeda-197">В порядке tooenable toolog пользователей Azure AD в Cornerstone OnDemand их необходимо подготовить в Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="eaeda-197">In order tooenable Azure AD users toolog into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="eaeda-198">В случае hello объекта Cornerstone OnDemand Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="eaeda-198">In hello case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="eaeda-199">tooconfigure подготовки пользователей, отправлять информацию hello (например: имя, электронной почты) о пользователе hello Azure AD требуется tooprovision toohello [поддержки Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="eaeda-199">tooconfigure user provisioning, send hello information (e.g.: Name, Email) about hello Azure AD user you want tooprovision toohello [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="eaeda-200">Можно использовать любые другие Cornerstone OnDemand пользователя средства создания учетных записей или интерфейсы API, предоставляемые Cornerstone OnDemand tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="eaeda-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eaeda-201">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="eaeda-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eaeda-202">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCornerstone по запросу.</span><span class="sxs-lookup"><span data-stu-id="eaeda-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCornerstone OnDemand.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="eaeda-204">**tooassign tooCornerstone Britta Simon OnDemand, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="eaeda-204">**tooassign Britta Simon tooCornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeda-205">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="eaeda-207">В списке приложений hello выберите **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-207">In hello applications list, select **Cornerstone OnDemand**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="eaeda-209">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="eaeda-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-211">Click **Add** button.</span></span> <span data-ttu-id="eaeda-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="eaeda-214">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="eaeda-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eaeda-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eaeda-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="eaeda-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eaeda-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="eaeda-217">Testing single sign-on</span></span>

<span data-ttu-id="eaeda-218">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="eaeda-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eaeda-219">При выборе плитки Cornerstone OnDemand hello в hello панели доступа, вы должны получить приложение автоматически вошедшего tooyour Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="eaeda-219">When you click hello Cornerstone OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour Cornerstone OnDemand application.</span></span>
<span data-ttu-id="eaeda-220">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eaeda-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eaeda-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="eaeda-221">Additional resources</span></span>

* [<span data-ttu-id="eaeda-222">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eaeda-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eaeda-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eaeda-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

