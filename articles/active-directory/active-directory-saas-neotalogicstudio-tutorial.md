---
title: "Руководство по интеграции Azure Active Directory с Neota Logic Studio | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Neota Studio логику."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: a479ee49618de8275132dbc2c21a8ef723d92d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="b9ca4-103">Руководство по интеграции Azure Active Directory с Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="b9ca4-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="b9ca4-104">В этом учебнике вы узнаете, как toointegrate Studio логики Neota с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9ca4-104">In this tutorial, you learn how toointegrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9ca4-105">Интеграция с Azure AD Neota логику Studio предоставляет следующие преимущества hello:</span><span class="sxs-lookup"><span data-stu-id="b9ca4-105">Integrating Neota Logic Studio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9ca4-106">Можно управлять в Azure AD, имеющего доступ tooNeota Studio логики</span><span class="sxs-lookup"><span data-stu-id="b9ca4-106">You can control in Azure AD who has access tooNeota Logic Studio</span></span>
- <span data-ttu-id="b9ca4-107">Ваш пользователей tooautomatically get вошедшего tooNeota Studio логики (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca4-107">You can enable your users tooautomatically get signed-on tooNeota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9ca4-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b9ca4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9ca4-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="b9ca4-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca4-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9ca4-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b9ca4-111">Prerequisites</span></span>

<span data-ttu-id="b9ca4-112">tooconfigure интеграция Azure AD с Neota логику Studio необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b9ca4-112">tooconfigure Azure AD integration with Neota Logic Studio, you need hello following items:</span></span>

- <span data-ttu-id="b9ca4-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b9ca4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="b9ca4-114">подписка Neota Logic Studio с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9ca4-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9ca4-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b9ca4-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9ca4-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9ca4-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9ca4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9ca4-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b9ca4-119">Scenario description</span></span>

<span data-ttu-id="b9ca4-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9ca4-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b9ca4-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9ca4-122">Добавление логики Studio Neota из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b9ca4-122">Adding Neota Logic Studio from hello gallery</span></span>
2. <span data-ttu-id="b9ca4-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-hello-gallery"></a><span data-ttu-id="b9ca4-124">Добавление логики Studio Neota из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b9ca4-124">Adding Neota Logic Studio from hello gallery</span></span>

<span data-ttu-id="b9ca4-125">tooconfigure hello интеграцию Neota логики Studio в Azure AD, вы должны tooadd Neota логику Studio из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-125">tooconfigure hello integration of Neota Logic Studio into Azure AD, you need tooadd Neota Logic Studio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9ca4-126">**tooadd Studio логику Neota из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b9ca4-126">**tooadd Neota Logic Studio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ca4-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9ca4-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9ca4-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b9ca4-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b9ca4-134">Введите в поле поиска hello **Neota логику Studio**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-134">In hello search box, type **Neota Logic Studio**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="b9ca4-136">В панели результатов hello, выберите **Studio логику Neota**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-136">In hello results panel, select **Neota Logic Studio**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9ca4-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca4-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="b9ca4-139">В этом разделе описано, как настроить и проверить единый вход Azure AD в Neota Logic Studio с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b9ca4-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Studio логику Neota является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Neota Logic Studio is tooa user in Azure AD.</span></span> <span data-ttu-id="b9ca4-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Studio логику Neota должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-141">In other words, a link relationship between an Azure AD user and hello related user in Neota Logic Studio needs toobe established.</span></span>

<span data-ttu-id="b9ca4-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Studio Neota логику.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="b9ca4-143">tooconfigure и теста Azure AD единого входа с Neota Studio логику, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-143">tooconfigure and test Azure AD single sign-on with Neota Logic Studio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9ca4-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9ca4-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9ca4-146">**[Создание тестового пользователя Studio логику Neota](#creating-a-neota-logic-studio-test-user)**  -toohave аналог Саймон Britta в Studio Neota логики, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - toohave a counterpart of Britta Simon in Neota Logic Studio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9ca4-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9ca4-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9ca4-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9ca4-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Studio Neota логику приложения.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="b9ca4-151">**tooconfigure Azure AD единого входа с помощью Neota Studio логику, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9ca4-151">**tooconfigure Azure AD single sign-on with Neota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ca4-152">В hello в hello портала Azure **Studio логику Neota** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-152">In hello Azure portal, on hello **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b9ca4-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="b9ca4-156">На hello **Neota логику Studio доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9ca4-156">On hello **Neota Logic Studio Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="b9ca4-158">а.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-158">a.</span></span> <span data-ttu-id="b9ca4-159">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="b9ca4-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="b9ca4-160">b.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-160">b.</span></span> <span data-ttu-id="b9ca4-161">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="b9ca4-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9ca4-162">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-162">These values are not hello real.</span></span> <span data-ttu-id="b9ca4-163">Обновить значения hello фактический URL-адрес входа & идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-163">Update these values with hello actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="b9ca4-164">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-164">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="b9ca4-165">Обратитесь к [группа поддержки клиента Studio логику Neota](https://www.neotalogic.com/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="b9ca4-166">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="b9ca4-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b9ca4-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9ca4-170">tooget единого входа, настроенному для вашего приложения, обратитесь к [поддержка Studio логику Neota](https://www.neotalogic.com/contact-us/) группы и предоставить им с загружены **метаданные в формате XML** файла.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-170">tooget SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="b9ca4-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b9ca4-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9ca4-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9ca4-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9ca4-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9ca4-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ca4-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9ca4-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b9ca4-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9ca4-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ca4-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9ca4-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9ca4-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b9ca4-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9ca4-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9ca4-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9ca4-186">а.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-186">a.</span></span> <span data-ttu-id="b9ca4-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9ca4-188">b.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-188">b.</span></span> <span data-ttu-id="b9ca4-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9ca4-190">c.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-190">c.</span></span> <span data-ttu-id="b9ca4-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9ca4-192">d.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-192">d.</span></span> <span data-ttu-id="b9ca4-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="b9ca4-194">Создание тестового пользователя Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="b9ca4-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="b9ca4-195">В этом разделе описано, как создать пользователя Britta Simon в Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="b9ca4-196">работают с [Neota клиента Studio логика поддержки](https://www.neotalogic.com/contact-us/) для добавления пользователей hello в платформы Neota логику Studio hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add hello users in hello Neota Logic Studio platform.</span></span> <span data-ttu-id="b9ca4-197">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9ca4-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b9ca4-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9ca4-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooNeota Studio логику.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNeota Logic Studio.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b9ca4-201">**tooassign tooNeota Britta Simon Studio логику выполнения hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="b9ca4-201">**tooassign Britta Simon tooNeota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ca4-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b9ca4-204">В списке приложений hello выберите **Neota логику Studio**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-204">In hello applications list, select **Neota Logic Studio**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="b9ca4-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b9ca4-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-208">Click **Add** button.</span></span> <span data-ttu-id="b9ca4-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b9ca4-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9ca4-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9ca4-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9ca4-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b9ca4-214">Testing single sign-on</span></span>

<span data-ttu-id="b9ca4-215">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b9ca4-216">Щелкните плитку Neota логику Studio hello в hello панели доступа, будут перенаправленный tooOrganization страницу входа.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-216">Click hello Neota Logic Studio tile in hello Access Panel, you will be redirected tooOrganization sign-on page.</span></span> <span data-ttu-id="b9ca4-217">После успешного входа будет подписан на tooyour Studio Neota логику приложения.</span><span class="sxs-lookup"><span data-stu-id="b9ca4-217">After successful login, you will be signed-on tooyour Neota Logic Studio application.</span></span> <span data-ttu-id="b9ca4-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b9ca4-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="b9ca4-219">Дополнительные сведения о панели доступа hello см. в разделе [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b9ca4-219">For more information about hello Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9ca4-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b9ca4-220">Additional resources</span></span>

* [<span data-ttu-id="b9ca4-221">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9ca4-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9ca4-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9ca4-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

