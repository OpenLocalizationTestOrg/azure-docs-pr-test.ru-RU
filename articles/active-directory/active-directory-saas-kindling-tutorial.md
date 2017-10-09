---
title: "Учебник. Интеграция Azure Active Directory с Kindling | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kindling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="88064-103">Учебник. Интеграция Azure Active Directory с Kindling</span><span class="sxs-lookup"><span data-stu-id="88064-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="88064-104">В этом учебнике вы узнаете, как toointegrate Kindling с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88064-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88064-105">Интеграция с Azure AD Kindling предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="88064-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="88064-106">Можно управлять в Azure AD, имеющего доступ tooKindling</span><span class="sxs-lookup"><span data-stu-id="88064-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="88064-107">Можно включить на пользователей tooautomatically get вошедшего tooKindling (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="88064-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88064-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="88064-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="88064-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88064-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="88064-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="88064-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88064-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="88064-111">Prerequisites</span></span>

<span data-ttu-id="88064-112">Интеграция Azure AD tooconfigure с Kindling, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="88064-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="88064-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="88064-113">An Azure AD subscription</span></span>
- <span data-ttu-id="88064-114">подписка Kindling с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="88064-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88064-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="88064-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88064-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="88064-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88064-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="88064-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88064-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88064-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88064-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="88064-119">Scenario description</span></span>
<span data-ttu-id="88064-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="88064-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88064-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="88064-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88064-122">Добавление Kindling из галереи hello</span><span class="sxs-lookup"><span data-stu-id="88064-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="88064-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="88064-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="88064-124">Добавление Kindling из галереи hello</span><span class="sxs-lookup"><span data-stu-id="88064-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="88064-125">интеграции hello tooconfigure Kindling в Azure AD, необходимо tooadd Kindling из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="88064-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="88064-126">**tooadd Kindling из галереи hello выполнения hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="88064-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88064-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="88064-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88064-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="88064-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="88064-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="88064-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="88064-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="88064-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="88064-134">Введите в поле поиска hello **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="88064-134">In hello search box, type **Kindling**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="88064-136">В панели результатов hello выберите **Kindling**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="88064-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88064-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="88064-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88064-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Kindling для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88064-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88064-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Kindling является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88064-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="88064-141">Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в toobe потребности Kindling установлено.</span><span class="sxs-lookup"><span data-stu-id="88064-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="88064-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Kindling.</span><span class="sxs-lookup"><span data-stu-id="88064-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="88064-143">tooconfigure и теста Azure AD единого входа с Kindling, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="88064-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88064-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="88064-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88064-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="88064-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88064-146">**[Создание тестового пользователя Kindling](#creating-a-kindling-test-user)**  -toohave аналог Саймон Britta в Kindling, то есть связанные представление toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="88064-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="88064-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="88064-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88064-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="88064-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88064-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="88064-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88064-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Kindling.</span><span class="sxs-lookup"><span data-stu-id="88064-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="88064-151">**tooconfigure Azure AD единого входа с Kindling, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="88064-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="88064-152">В hello в hello портала Azure **Kindling** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="88064-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="88064-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="88064-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="88064-156">На hello **Kindling доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="88064-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="88064-158">а.</span><span class="sxs-lookup"><span data-stu-id="88064-158">a.</span></span> <span data-ttu-id="88064-159">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="88064-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="88064-160">b.</span><span class="sxs-lookup"><span data-stu-id="88064-160">b.</span></span>  <span data-ttu-id="88064-161">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="88064-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88064-162">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="88064-162">These values are not hello real.</span></span> <span data-ttu-id="88064-163">Обновите эти значения с hello фактический URL-адрес входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="88064-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="88064-164">Обратитесь к [Kindling поддержки](mailto:support@kindlingapp.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="88064-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="88064-165">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="88064-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="88064-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="88064-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88064-169">На hello **Kindling конфигурации** щелкните **Настройка Kindling** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="88064-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="88064-170">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="88064-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="88064-172">tooconfigure единого входа на **Kindling** стороны, необходимо загрузить hello toosend **сертификата (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы**слишком[Kindling поддержки](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="88064-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="88064-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="88064-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="88064-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="88064-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="88064-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88064-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88064-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="88064-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="88064-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="88064-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="88064-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="88064-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88064-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="88064-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88064-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="88064-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88064-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="88064-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88064-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="88064-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88064-188">а.</span><span class="sxs-lookup"><span data-stu-id="88064-188">a.</span></span> <span data-ttu-id="88064-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88064-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88064-190">b.</span><span class="sxs-lookup"><span data-stu-id="88064-190">b.</span></span> <span data-ttu-id="88064-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88064-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88064-192">c.</span><span class="sxs-lookup"><span data-stu-id="88064-192">c.</span></span> <span data-ttu-id="88064-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="88064-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="88064-194">d.</span><span class="sxs-lookup"><span data-stu-id="88064-194">d.</span></span> <span data-ttu-id="88064-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="88064-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="88064-196">Создание тестового пользователя Kindling</span><span class="sxs-lookup"><span data-stu-id="88064-196">Creating a Kindling test user</span></span>

<span data-ttu-id="88064-197">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Kindling.</span><span class="sxs-lookup"><span data-stu-id="88064-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="88064-198">Приложение Kindling поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="88064-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="88064-199">Эта функция уже включена в ходе [настройки единого входа Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="88064-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="88064-200">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="88064-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="88064-201">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="88064-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="88064-202">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooKindling доступа.</span><span class="sxs-lookup"><span data-stu-id="88064-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="88064-204">**tooassign tooKindling Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="88064-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="88064-205">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="88064-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="88064-207">В списке приложений hello выберите **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="88064-207">In hello applications list, select **Kindling**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="88064-209">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="88064-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="88064-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="88064-211">Click **Add** button.</span></span> <span data-ttu-id="88064-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="88064-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="88064-214">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="88064-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="88064-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="88064-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88064-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="88064-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88064-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="88064-217">Testing single sign-on</span></span>

<span data-ttu-id="88064-218">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="88064-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="88064-219">При нажатии кнопки hello Kindling плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Kindling приложения.</span><span class="sxs-lookup"><span data-stu-id="88064-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="88064-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="88064-220">Additional resources</span></span>

* [<span data-ttu-id="88064-221">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88064-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88064-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88064-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

