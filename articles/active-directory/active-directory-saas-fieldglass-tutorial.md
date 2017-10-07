---
title: "Руководство по интеграции Azure Active Directory с Fieldglass | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Fieldglass."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2510195f-d5b1-4684-b3da-283fb8619df2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d953996bc3bf5721b8280dae4b9992aef7934b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fieldglass"></a><span data-ttu-id="3f4ec-103">Руководство по интеграции Azure Active Directory с Fieldglass</span><span class="sxs-lookup"><span data-stu-id="3f4ec-103">Tutorial: Azure Active Directory integration with Fieldglass</span></span>

<span data-ttu-id="3f4ec-104">В этом учебнике вы узнаете, как toointegrate Fieldglass с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f4ec-104">In this tutorial, you learn how toointegrate Fieldglass with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f4ec-105">Интеграция с Azure AD Fieldglass предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3f4ec-105">Integrating Fieldglass with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3f4ec-106">Можно управлять в Azure AD, имеющего доступ tooFieldglass</span><span class="sxs-lookup"><span data-stu-id="3f4ec-106">You can control in Azure AD who has access tooFieldglass</span></span>
- <span data-ttu-id="3f4ec-107">Можно включить на пользователей tooautomatically get вошедшего tooFieldglass (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f4ec-107">You can enable your users tooautomatically get signed-on tooFieldglass (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f4ec-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3f4ec-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3f4ec-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f4ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f4ec-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3f4ec-110">Prerequisites</span></span>

<span data-ttu-id="3f4ec-111">tooconfigure интеграция Azure AD с Fieldglass требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3f4ec-111">tooconfigure Azure AD integration with Fieldglass, you need hello following items:</span></span>

- <span data-ttu-id="3f4ec-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3f4ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f4ec-113">подписка на Fieldglass с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-113">A Fieldglass single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f4ec-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f4ec-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3f4ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f4ec-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f4ec-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f4ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f4ec-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3f4ec-118">Scenario description</span></span>
<span data-ttu-id="3f4ec-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f4ec-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3f4ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f4ec-121">Добавление Fieldglass из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3f4ec-121">Adding Fieldglass from hello gallery</span></span>
2. <span data-ttu-id="3f4ec-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f4ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fieldglass-from-hello-gallery"></a><span data-ttu-id="3f4ec-123">Добавление Fieldglass из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3f4ec-123">Adding Fieldglass from hello gallery</span></span>
<span data-ttu-id="3f4ec-124">tooconfigure hello интеграции Fieldglass в Azure AD, вы должны tooadd Fieldglass из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-124">tooconfigure hello integration of Fieldglass into Azure AD, you need tooadd Fieldglass from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3f4ec-125">**tooadd Fieldglass из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f4ec-125">**tooadd Fieldglass from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f4ec-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f4ec-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3f4ec-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3f4ec-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3f4ec-133">Введите в поле поиска hello **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-133">In hello search box, type **Fieldglass**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_search.png)

5. <span data-ttu-id="3f4ec-135">В панели результатов hello выберите **Fieldglass**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-135">In hello results panel, select **Fieldglass**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f4ec-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f4ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3f4ec-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Fieldglass для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-138">In this section, you configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3f4ec-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Fieldglass является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fieldglass is tooa user in Azure AD.</span></span> <span data-ttu-id="3f4ec-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Fieldglass должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-140">In other words, a link relationship between an Azure AD user and hello related user in Fieldglass needs toobe established.</span></span>

<span data-ttu-id="3f4ec-141">В Fieldglass, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-141">In Fieldglass, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3f4ec-142">tooconfigure и теста Azure AD единого входа с Fieldglass, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3f4ec-142">tooconfigure and test Azure AD single sign-on with Fieldglass, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3f4ec-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3f4ec-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f4ec-145">**[Создание тестового пользователя Fieldglass](#creating-a-fieldglass-test-user)**  -toohave аналог Саймон Britta в Fieldglass, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-145">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - toohave a counterpart of Britta Simon in Fieldglass that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f4ec-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f4ec-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f4ec-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f4ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f4ec-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fieldglass application.</span></span>

<span data-ttu-id="3f4ec-150">**tooconfigure Azure AD единого входа с Fieldglass, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f4ec-150">**tooconfigure Azure AD single sign-on with Fieldglass, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f4ec-151">В hello в hello портала Azure **Fieldglass** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-151">In hello Azure portal, on hello **Fieldglass** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3f4ec-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_samlbase.png)

3. <span data-ttu-id="3f4ec-155">На hello **URL-адреса и домена Fieldglass** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3f4ec-155">On hello **Fieldglass Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_url.png)

    <span data-ttu-id="3f4ec-157">а.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-157">a.</span></span> <span data-ttu-id="3f4ec-158">В hello **идентификатор** текстовом поле введите URL-адрес как `https://www.fieldglass.com` или следовать шаблону hello:`https://<company name>.fgvms.com`</span><span class="sxs-lookup"><span data-stu-id="3f4ec-158">In hello **Identifier** textbox, type a URL as  `https://www.fieldglass.com` or follow hello pattern:  `https://<company name>.fgvms.com`</span></span>

    <span data-ttu-id="3f4ec-159">b.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-159">b.</span></span> <span data-ttu-id="3f4ec-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="3f4ec-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://www.fieldglass.net/<company name>`|
    | `https://<company name>.fgvms.com/<company name>`|

    > [!NOTE] 
    > <span data-ttu-id="3f4ec-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-161">These values are not real.</span></span> <span data-ttu-id="3f4ec-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="3f4ec-163">Обратитесь к [Fieldglass поддержки](http://www.fieldglass.com/solutions/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-163">Contact [Fieldglass support team](http://www.fieldglass.com/solutions/support) tooget these values.</span></span>
 
4. <span data-ttu-id="3f4ec-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_certificate.png) 

5. <span data-ttu-id="3f4ec-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3f4ec-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3f4ec-168">На hello **конфигурации Fieldglass** щелкните **Настройка Fieldglass** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-168">On hello **Fieldglass Configuration** section, click **Configure Fieldglass** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3f4ec-169">Копировать hello **URL-адрес выхода и идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="3f4ec-169">Copy hello **Sign-Out URL and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_configure.png) 

7. <span data-ttu-id="3f4ec-171">tooconfigure единого входа на **Fieldglass** стороны, необходимо загрузить hello toosend **Certificate(Base64)** и **URL-адрес выхода, идентификатор сущности SAML** слишком[ Fieldglass поддержки](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="3f4ec-171">tooconfigure single sign-on on **Fieldglass** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID** too[Fieldglass support team](http://www.fieldglass.com/solutions/support).</span></span> <span data-ttu-id="3f4ec-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3f4ec-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3f4ec-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3f4ec-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3f4ec-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f4ec-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f4ec-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f4ec-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f4ec-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3f4ec-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f4ec-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f4ec-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f4ec-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f4ec-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="3f4ec-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f4ec-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3f4ec-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f4ec-188">а.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-188">a.</span></span> <span data-ttu-id="3f4ec-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f4ec-190">b.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-190">b.</span></span> <span data-ttu-id="3f4ec-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f4ec-192">c.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-192">c.</span></span> <span data-ttu-id="3f4ec-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3f4ec-194">d.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-194">d.</span></span> <span data-ttu-id="3f4ec-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-195">Click **Create**.</span></span>
 
### <a name="creating-a-fieldglass-test-user"></a><span data-ttu-id="3f4ec-196">Создание тестового пользователя Fieldglass</span><span class="sxs-lookup"><span data-stu-id="3f4ec-196">Creating a Fieldglass test user</span></span>

<span data-ttu-id="3f4ec-197">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в FieldGlass.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-197">hello objective of this section is toocreate a user called Britta Simon in FieldGlass.</span></span> <span data-ttu-id="3f4ec-198">Обратитесь к [Fieldglass поддержки](http://www.fieldglass.com/solutions/support) tooadd пользователей hello в hello Fieldglass учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-198">Please work with your [Fieldglass support team](http://www.fieldglass.com/solutions/support) tooadd hello users in hello Fieldglass account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3f4ec-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3f4ec-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3f4ec-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooFieldglass доступа.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFieldglass.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3f4ec-202">**tooassign tooFieldglass Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3f4ec-202">**tooassign Britta Simon tooFieldglass, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f4ec-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3f4ec-205">В списке приложений hello выберите **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-205">In hello applications list, select **Fieldglass**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_app.png) 

3. <span data-ttu-id="3f4ec-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3f4ec-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-209">Click **Add** button.</span></span> <span data-ttu-id="3f4ec-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3f4ec-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3f4ec-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f4ec-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f4ec-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3f4ec-215">Testing single sign-on</span></span>

<span data-ttu-id="3f4ec-216">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="3f4ec-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3f4ec-217">При нажатии кнопки Fieldglass плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Fieldglass приложения.</span><span class="sxs-lookup"><span data-stu-id="3f4ec-217">When you click hello Fieldglass tile in hello Access Panel, you should get automatically signed-on tooyour Fieldglass application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f4ec-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3f4ec-218">Additional resources</span></span>

* [<span data-ttu-id="3f4ec-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f4ec-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f4ec-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f4ec-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_203.png

