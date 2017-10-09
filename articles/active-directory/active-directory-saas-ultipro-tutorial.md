---
title: "Руководство. Интеграция Azure Active Directory с UltiPro | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и UltiPro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 8cb613228893e8cbf997957452d55d0ab7939171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="5ff81-103">Руководство. Интеграция Azure Active Directory с UltiPro</span><span class="sxs-lookup"><span data-stu-id="5ff81-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="5ff81-104">В этом учебнике вы узнаете, как toointegrate UltiPro с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ff81-104">In this tutorial, you learn how toointegrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ff81-105">Интеграция с Azure AD UltiPro предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5ff81-105">Integrating UltiPro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5ff81-106">Можно управлять в Azure AD, имеющего доступ tooUltiPro</span><span class="sxs-lookup"><span data-stu-id="5ff81-106">You can control in Azure AD who has access tooUltiPro</span></span>
- <span data-ttu-id="5ff81-107">Можно включить на пользователей tooautomatically get вошедшего tooUltiPro (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff81-107">You can enable your users tooautomatically get signed-on tooUltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ff81-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5ff81-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5ff81-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ff81-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ff81-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ff81-110">Prerequisites</span></span>

<span data-ttu-id="5ff81-111">tooconfigure интеграция Azure AD с UltiPro требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5ff81-111">tooconfigure Azure AD integration with UltiPro, you need hello following items:</span></span>

- <span data-ttu-id="5ff81-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5ff81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ff81-113">подписка UltiPro с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5ff81-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ff81-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5ff81-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ff81-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5ff81-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ff81-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5ff81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ff81-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ff81-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ff81-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5ff81-118">Scenario description</span></span>
<span data-ttu-id="5ff81-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5ff81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ff81-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5ff81-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ff81-121">Добавление UltiPro из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5ff81-121">Adding UltiPro from hello gallery</span></span>
2. <span data-ttu-id="5ff81-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-hello-gallery"></a><span data-ttu-id="5ff81-123">Добавление UltiPro из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5ff81-123">Adding UltiPro from hello gallery</span></span>
<span data-ttu-id="5ff81-124">tooconfigure hello интеграции UltiPro в Azure AD, вы должны tooadd UltiPro из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5ff81-124">tooconfigure hello integration of UltiPro into Azure AD, you need tooadd UltiPro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ff81-125">**tooadd UltiPro из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5ff81-125">**tooadd UltiPro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff81-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5ff81-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ff81-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5ff81-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5ff81-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5ff81-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5ff81-133">Введите в поле поиска hello **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-133">In hello search box, type **UltiPro**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="5ff81-135">В панели результатов hello выберите **UltiPro**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ff81-135">In hello results panel, select **UltiPro**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ff81-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff81-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ff81-138">В этом разделе описана настройка и проверка единого входа Azure AD в UltiPro с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ff81-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ff81-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в UltiPro является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ff81-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UltiPro is tooa user in Azure AD.</span></span> <span data-ttu-id="5ff81-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в UltiPro должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5ff81-140">In other words, a link relationship between an Azure AD user and hello related user in UltiPro needs toobe established.</span></span>

<span data-ttu-id="5ff81-141">В UltiPro, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="5ff81-141">In UltiPro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5ff81-142">tooconfigure и теста Azure AD единого входа с UltiPro, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5ff81-142">tooconfigure and test Azure AD single sign-on with UltiPro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ff81-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5ff81-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ff81-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5ff81-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ff81-145">**[Создание тестового пользователя UltiPro](#creating-a-ultipro-test-user)**  -toohave аналог Саймон Britta в UltiPro, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5ff81-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - toohave a counterpart of Britta Simon in UltiPro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ff81-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5ff81-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ff81-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5ff81-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ff81-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff81-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ff81-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении UltiPro.</span><span class="sxs-lookup"><span data-stu-id="5ff81-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="5ff81-150">**tooconfigure Azure AD единого входа с UltiPro, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5ff81-150">**tooconfigure Azure AD single sign-on with UltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff81-151">В hello в hello портала Azure **UltiPro** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-151">In hello Azure portal, on hello **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5ff81-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5ff81-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="5ff81-155">На hello **URL-адреса и домена UltiPro** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5ff81-155">On hello **UltiPro Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="5ff81-157">а.</span><span class="sxs-lookup"><span data-stu-id="5ff81-157">a.</span></span> <span data-ttu-id="5ff81-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="5ff81-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="5ff81-159">b.</span><span class="sxs-lookup"><span data-stu-id="5ff81-159">b.</span></span> <span data-ttu-id="5ff81-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="5ff81-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="5ff81-161">c.</span><span class="sxs-lookup"><span data-stu-id="5ff81-161">c.</span></span> <span data-ttu-id="5ff81-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="5ff81-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="5ff81-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5ff81-163">These values are not real.</span></span> <span data-ttu-id="5ff81-164">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="5ff81-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5ff81-165">Обратитесь к [группа поддержки клиента UltiPro](https://www.ultimatesoftware.com/ContactUs) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="5ff81-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) tooget these values.</span></span> 

5. <span data-ttu-id="5ff81-166">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ff81-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="5ff81-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5ff81-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="5ff81-170">На hello **конфигурации UltiPro** щелкните **Настройка UltiPro** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="5ff81-170">On hello **UltiPro Configuration** section, click **Configure UltiPro** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5ff81-171">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="5ff81-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="5ff81-173">tooconfigure единого входа на **UltiPro** стороны, необходимо загрузить hello toosend **Certificate(Base64), URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[UltiPro поддержки](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="5ff81-173">tooconfigure single sign-on on **UltiPro** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="5ff81-174">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5ff81-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5ff81-175">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5ff81-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5ff81-176">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ff81-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ff81-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ff81-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ff81-178">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff81-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5ff81-180">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5ff81-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff81-181">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5ff81-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ff81-183">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ff81-185">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="5ff81-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ff81-187">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5ff81-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ff81-189">а.</span><span class="sxs-lookup"><span data-stu-id="5ff81-189">a.</span></span> <span data-ttu-id="5ff81-190">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ff81-191">b.</span><span class="sxs-lookup"><span data-stu-id="5ff81-191">b.</span></span> <span data-ttu-id="5ff81-192">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ff81-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ff81-193">c.</span><span class="sxs-lookup"><span data-stu-id="5ff81-193">c.</span></span> <span data-ttu-id="5ff81-194">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5ff81-195">d.</span><span class="sxs-lookup"><span data-stu-id="5ff81-195">d.</span></span> <span data-ttu-id="5ff81-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="5ff81-197">Создание тестового пользователя UltiPro</span><span class="sxs-lookup"><span data-stu-id="5ff81-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="5ff81-198">В этом разделе описано, как создать пользователя Britta Simon в приложении UltiPro.</span><span class="sxs-lookup"><span data-stu-id="5ff81-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="5ff81-199">Работать с [UltiPro поддержки](https://www.ultimatesoftware.com/ContactUs) для добавления пользователей hello в платформе UltiPro hello.</span><span class="sxs-lookup"><span data-stu-id="5ff81-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add hello users in hello UltiPro platform.</span></span> <span data-ttu-id="5ff81-200">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="5ff81-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5ff81-201">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5ff81-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5ff81-202">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooUltiPro доступа.</span><span class="sxs-lookup"><span data-stu-id="5ff81-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUltiPro.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5ff81-204">**tooassign tooUltiPro Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5ff81-204">**tooassign Britta Simon tooUltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ff81-205">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5ff81-207">В списке приложений hello выберите **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-207">In hello applications list, select **UltiPro**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="5ff81-209">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5ff81-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-211">Click **Add** button.</span></span> <span data-ttu-id="5ff81-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5ff81-214">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5ff81-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5ff81-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ff81-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5ff81-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ff81-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5ff81-217">Testing single sign-on</span></span>

<span data-ttu-id="5ff81-218">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="5ff81-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="5ff81-219">При нажатии кнопки hello UltiPro плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour UltiPro приложения.</span><span class="sxs-lookup"><span data-stu-id="5ff81-219">When you click hello UltiPro tile in hello Access Panel, you should get automatically signed-on tooyour UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ff81-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5ff81-220">Additional resources</span></span>

* [<span data-ttu-id="5ff81-221">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ff81-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ff81-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ff81-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png

