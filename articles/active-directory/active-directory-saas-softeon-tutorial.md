---
title: "Учебник по интеграции Azure Active Directory с Softeon WMS | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Softeon WMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 07c5de0d-90aa-43b3-b24e-0cc334b2f9b0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jeedes
ms.openlocfilehash: 135e4a8a4bc63fd24615e12d037120bf37342547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-softeon-wms"></a><span data-ttu-id="26e08-103">Руководство по интеграции Azure Active Directory с Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="26e08-103">Tutorial: Azure Active Directory integration with Softeon WMS</span></span>

<span data-ttu-id="26e08-104">В этом учебнике вы узнаете, как toointegrate Softeon WMS с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26e08-104">In this tutorial, you learn how toointegrate Softeon WMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26e08-105">Интеграция с Azure AD Softeon WMS предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="26e08-105">Integrating Softeon WMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="26e08-106">Можно управлять в Azure AD, имеющего доступ tooSofteon WMS</span><span class="sxs-lookup"><span data-stu-id="26e08-106">You can control in Azure AD who has access tooSofteon WMS</span></span>
- <span data-ttu-id="26e08-107">Можно включить на пользователей tooautomatically get вошедшего tooSofteon WMS (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="26e08-107">You can enable your users tooautomatically get signed-on tooSofteon WMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26e08-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="26e08-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="26e08-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26e08-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26e08-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="26e08-110">Prerequisites</span></span>

<span data-ttu-id="26e08-111">tooconfigure интеграция Azure AD с Softeon WMS необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="26e08-111">tooconfigure Azure AD integration with Softeon WMS, you need hello following items:</span></span>

- <span data-ttu-id="26e08-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="26e08-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26e08-113">подписка на Softeon WMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="26e08-113">A Softeon WMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26e08-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="26e08-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26e08-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="26e08-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26e08-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="26e08-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26e08-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26e08-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26e08-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="26e08-118">Scenario description</span></span>
<span data-ttu-id="26e08-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="26e08-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26e08-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="26e08-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26e08-121">Добавление Softeon WMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="26e08-121">Adding Softeon WMS from hello gallery</span></span>
2. <span data-ttu-id="26e08-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="26e08-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-softeon-wms-from-hello-gallery"></a><span data-ttu-id="26e08-123">Добавление Softeon WMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="26e08-123">Adding Softeon WMS from hello gallery</span></span>
<span data-ttu-id="26e08-124">tooconfigure hello интеграции Softeon WMS в Azure AD, вы должны tooadd Softeon WMS из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="26e08-124">tooconfigure hello integration of Softeon WMS into Azure AD, you need tooadd Softeon WMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="26e08-125">**tooadd WMS Softeon из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="26e08-125">**tooadd Softeon WMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="26e08-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="26e08-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26e08-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="26e08-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="26e08-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="26e08-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="26e08-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="26e08-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="26e08-133">Введите в поле поиска hello **Softeon WMS**.</span><span class="sxs-lookup"><span data-stu-id="26e08-133">In hello search box, type **Softeon WMS**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_search.png)

5. <span data-ttu-id="26e08-135">В панели результатов hello выберите **Softeon WMS**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="26e08-135">In hello results panel, select **Softeon WMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26e08-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="26e08-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26e08-138">В этом разделе описана настройка и проверка единого входа Azure AD в Softeon WMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26e08-138">In this section, you configure and test Azure AD single sign-on with Softeon WMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="26e08-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Softeon WMS является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26e08-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Softeon WMS is tooa user in Azure AD.</span></span> <span data-ttu-id="26e08-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Softeon WMS должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="26e08-140">In other words, a link relationship between an Azure AD user and hello related user in Softeon WMS needs toobe established.</span></span>

<span data-ttu-id="26e08-141">В Softeon WMS, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="26e08-141">In Softeon WMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="26e08-142">tooconfigure и теста Azure AD единого входа с Softeon WMS, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="26e08-142">tooconfigure and test Azure AD single sign-on with Softeon WMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="26e08-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="26e08-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="26e08-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="26e08-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26e08-145">**[Создание тестового пользователя Softeon WMS](#creating-a-softeon-wms-test-user)**  -toohave аналог Саймон Britta в Softeon WMS, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="26e08-145">**[Creating a Softeon WMS test user](#creating-a-softeon-wms-test-user)** - toohave a counterpart of Britta Simon in Softeon WMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="26e08-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="26e08-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26e08-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="26e08-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26e08-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="26e08-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26e08-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Softeon WMS.</span><span class="sxs-lookup"><span data-stu-id="26e08-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Softeon WMS application.</span></span>

<span data-ttu-id="26e08-150">**tooconfigure Azure AD единого входа с Softeon WMS, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="26e08-150">**tooconfigure Azure AD single sign-on with Softeon WMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="26e08-151">В hello в hello портала Azure **Softeon WMS** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="26e08-151">In hello Azure portal, on hello **Softeon WMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="26e08-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="26e08-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_samlbase.png)

3. <span data-ttu-id="26e08-155">На hello **URL-адреса и домена WMS Softeon** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="26e08-155">On hello **Softeon WMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_url.png)

    <span data-ttu-id="26e08-157">а.</span><span class="sxs-lookup"><span data-stu-id="26e08-157">a.</span></span> <span data-ttu-id="26e08-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.softeon.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="26e08-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.softeon.com/<instancename>`</span></span>

    <span data-ttu-id="26e08-159">b.</span><span class="sxs-lookup"><span data-stu-id="26e08-159">b.</span></span> <span data-ttu-id="26e08-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.softeon.com/sp`</span><span class="sxs-lookup"><span data-stu-id="26e08-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.softeon.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26e08-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="26e08-161">These values are not real.</span></span> <span data-ttu-id="26e08-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="26e08-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="26e08-163">Обратитесь к [группа поддержки клиента WMS Softeon](mailto:contact@softeon.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="26e08-163">Contact [Softeon WMS Client support team](mailto:contact@softeon.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="26e08-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="26e08-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_certificate.png) 

5. <span data-ttu-id="26e08-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="26e08-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-softeon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26e08-168">На hello **конфигурации WMS Softeon** щелкните **настройки WMS Softeon** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="26e08-168">On hello **Softeon WMS Configuration** section, click **Configure Softeon WMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="26e08-169">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="26e08-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_configure.png) 

7. <span data-ttu-id="26e08-171">tooconfigure единого входа на **Softeon WMS** стороны, необходимо загрузить hello toosend **сертификат (Base64), идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[поддержки Softeon WMS команда](mailto:contact@softeon.com).</span><span class="sxs-lookup"><span data-stu-id="26e08-171">tooconfigure single sign-on on **Softeon WMS** side, you need toosend hello downloaded **Certificate (Base64), SAML Entity ID, and SAML Single Sign-On Service URL** too[Softeon WMS support team](mailto:contact@softeon.com).</span></span> <span data-ttu-id="26e08-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="26e08-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="26e08-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="26e08-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="26e08-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="26e08-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="26e08-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26e08-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26e08-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="26e08-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="26e08-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="26e08-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="26e08-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="26e08-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="26e08-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="26e08-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-softeon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26e08-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="26e08-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-softeon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26e08-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="26e08-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-softeon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26e08-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="26e08-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-softeon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26e08-188">а.</span><span class="sxs-lookup"><span data-stu-id="26e08-188">a.</span></span> <span data-ttu-id="26e08-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26e08-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26e08-190">b.</span><span class="sxs-lookup"><span data-stu-id="26e08-190">b.</span></span> <span data-ttu-id="26e08-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="26e08-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26e08-192">c.</span><span class="sxs-lookup"><span data-stu-id="26e08-192">c.</span></span> <span data-ttu-id="26e08-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="26e08-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="26e08-194">d.</span><span class="sxs-lookup"><span data-stu-id="26e08-194">d.</span></span> <span data-ttu-id="26e08-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="26e08-195">Click **Create**.</span></span>
 
### <a name="creating-a-softeon-wms-test-user"></a><span data-ttu-id="26e08-196">Создание тестового пользователя Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="26e08-196">Creating a Softeon WMS test user</span></span>

<span data-ttu-id="26e08-197">Приложение поддерживает только в подготовки пользователей время и после проверки подлинности пользователей автоматически создаются в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="26e08-197">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="26e08-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="26e08-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="26e08-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSofteon WMS.</span><span class="sxs-lookup"><span data-stu-id="26e08-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSofteon WMS.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="26e08-201">**tooassign tooSofteon Britta Simon WMS, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="26e08-201">**tooassign Britta Simon tooSofteon WMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="26e08-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="26e08-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="26e08-204">В списке приложений hello выберите **Softeon WMS**.</span><span class="sxs-lookup"><span data-stu-id="26e08-204">In hello applications list, select **Softeon WMS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_app.png) 

3. <span data-ttu-id="26e08-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="26e08-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="26e08-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="26e08-208">Click **Add** button.</span></span> <span data-ttu-id="26e08-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="26e08-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="26e08-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="26e08-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="26e08-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="26e08-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26e08-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="26e08-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26e08-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="26e08-214">Testing single sign-on</span></span>

<span data-ttu-id="26e08-215">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="26e08-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="26e08-216">При нажатии кнопки hello Softeon WMS плитки в панели доступа hello, должно появиться страница входа Softeon WMS приложения.</span><span class="sxs-lookup"><span data-stu-id="26e08-216">When you click hello Softeon WMS tile in hello Access Panel, you should get login page of Softeon WMS application.</span></span>
<span data-ttu-id="26e08-217">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26e08-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="26e08-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="26e08-218">Additional resources</span></span>

* [<span data-ttu-id="26e08-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26e08-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26e08-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26e08-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_203.png

