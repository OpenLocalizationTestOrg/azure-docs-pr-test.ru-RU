---
title: "Руководство по интеграции Azure Active Directory с YouEarnedIt | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и YouEarnedIt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: cc9a8ae2f92751cf3fadbeec23c8319c83728a33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="e465c-103">Руководство. Интеграция Azure Active Directory с YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="e465c-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="e465c-104">В этом учебнике вы узнаете, как toointegrate YouEarnedIt с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e465c-104">In this tutorial, you learn how toointegrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e465c-105">Интеграция с Azure AD YouEarnedIt предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e465c-105">Integrating YouEarnedIt with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e465c-106">Можно управлять в Azure AD, имеющего доступ tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="e465c-106">You can control in Azure AD who has access tooYouEarnedIt.</span></span>
- <span data-ttu-id="e465c-107">Можно включить на пользователей tooautomatically get вошедшего tooYouEarnedIt (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e465c-107">You can enable your users tooautomatically get signed-on tooYouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e465c-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e465c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e465c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e465c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e465c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e465c-110">Prerequisites</span></span>

<span data-ttu-id="e465c-111">tooconfigure интеграция Azure AD с YouEarnedIt требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="e465c-111">tooconfigure Azure AD integration with YouEarnedIt, you need hello following items:</span></span>

- <span data-ttu-id="e465c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e465c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e465c-113">подписка YouEarnedIt с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e465c-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e465c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e465c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e465c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="e465c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e465c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e465c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e465c-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e465c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e465c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e465c-118">Scenario description</span></span>
<span data-ttu-id="e465c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e465c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e465c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="e465c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e465c-121">Добавление YouEarnedIt из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e465c-121">Adding YouEarnedIt from hello gallery</span></span>
2. <span data-ttu-id="e465c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e465c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-hello-gallery"></a><span data-ttu-id="e465c-123">Добавление YouEarnedIt из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e465c-123">Adding YouEarnedIt from hello gallery</span></span>
<span data-ttu-id="e465c-124">tooconfigure hello интеграции YouEarnedIt в Azure AD, вы должны tooadd YouEarnedIt из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e465c-124">tooconfigure hello integration of YouEarnedIt into Azure AD, you need tooadd YouEarnedIt from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e465c-125">**tooadd YouEarnedIt из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e465c-125">**tooadd YouEarnedIt from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e465c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e465c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="e465c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="e465c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e465c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e465c-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="e465c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e465c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="e465c-133">Введите в поле поиска hello **YouEarnedt**выберите **YouEarnedt** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e465c-133">In hello search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![YouEarnedIt в списке результатов hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e465c-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e465c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e465c-136">В этом разделе описана настройка и проверка единого входа Azure AD в YouEarnedIt с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e465c-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e465c-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в YouEarnedIt является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e465c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in YouEarnedIt is tooa user in Azure AD.</span></span> <span data-ttu-id="e465c-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в YouEarnedIt должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="e465c-138">In other words, a link relationship between an Azure AD user and hello related user in YouEarnedIt needs toobe established.</span></span>

<span data-ttu-id="e465c-139">В YouEarnedIt, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="e465c-139">In YouEarnedIt, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e465c-140">tooconfigure и теста Azure AD единого входа с YouEarnedIt, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e465c-140">tooconfigure and test Azure AD single sign-on with YouEarnedIt, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e465c-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="e465c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e465c-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e465c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e465c-143">**[Создание тестового пользователя YouEarnedIt](#create-a-youearnedit-test-user)**  -toohave аналог Саймон Britta в YouEarnedIt, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e465c-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - toohave a counterpart of Britta Simon in YouEarnedIt that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e465c-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="e465c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e465c-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e465c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e465c-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="e465c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e465c-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="e465c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="e465c-148">**tooconfigure Azure AD единого входа с YouEarnedIt, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e465c-148">**tooconfigure Azure AD single sign-on with YouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="e465c-149">В hello в hello портала Azure **YouEarnedIt** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e465c-149">In hello Azure portal, on hello **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="e465c-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="e465c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="e465c-153">На hello **URL-адреса и домена YouEarnedIt** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e465c-153">On hello **YouEarnedIt Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="e465c-155">а.</span><span class="sxs-lookup"><span data-stu-id="e465c-155">a.</span></span> <span data-ttu-id="e465c-156">В hello **URL-адрес входа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="e465c-156">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | <span data-ttu-id="e465c-157">Среда</span><span class="sxs-lookup"><span data-stu-id="e465c-157">Environment</span></span>  | <span data-ttu-id="e465c-158">Модель</span><span class="sxs-lookup"><span data-stu-id="e465c-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="e465c-159">Производство</span><span class="sxs-lookup"><span data-stu-id="e465c-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="e465c-160">Песочница</span><span class="sxs-lookup"><span data-stu-id="e465c-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="e465c-161">b.</span><span class="sxs-lookup"><span data-stu-id="e465c-161">b.</span></span> <span data-ttu-id="e465c-162">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="e465c-162">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="e465c-163">Среда</span><span class="sxs-lookup"><span data-stu-id="e465c-163">Environment</span></span>  | <span data-ttu-id="e465c-164">Модель</span><span class="sxs-lookup"><span data-stu-id="e465c-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="e465c-165">Производство</span><span class="sxs-lookup"><span data-stu-id="e465c-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="e465c-166">Песочница</span><span class="sxs-lookup"><span data-stu-id="e465c-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="e465c-167">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e465c-167">These values are not real.</span></span> <span data-ttu-id="e465c-168">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="e465c-168">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e465c-169">Обратитесь к [группа поддержки клиента YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="e465c-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) tooget these values.</span></span> 
 
4. <span data-ttu-id="e465c-170">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e465c-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="e465c-172">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e465c-172">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e465c-174">На hello **конфигурации YouEarnedIt** щелкните **Настройка YouEarnedIt** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="e465c-174">On hello **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e465c-175">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="e465c-175">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="e465c-177">tooconfigure единого входа на **YouEarnedIt** стороны, необходимо загрузить hello toosend **Certificate(Base64)** и **SAML единого входа URL-адрес службы** слишком[Группа поддержки YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="e465c-177">tooconfigure single sign-on on **YouEarnedIt** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="e465c-178">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="e465c-178">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e465c-179">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="e465c-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e465c-180">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="e465c-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e465c-181">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e465c-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e465c-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e465c-182">Create an Azure AD test user</span></span>

<span data-ttu-id="e465c-183">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e465c-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="e465c-185">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e465c-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e465c-186">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e465c-186">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e465c-188">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e465c-188">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e465c-190">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e465c-190">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e465c-192">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e465c-192">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e465c-194">а.</span><span class="sxs-lookup"><span data-stu-id="e465c-194">a.</span></span> <span data-ttu-id="e465c-195">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e465c-195">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e465c-196">b.</span><span class="sxs-lookup"><span data-stu-id="e465c-196">b.</span></span> <span data-ttu-id="e465c-197">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e465c-197">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e465c-198">c.</span><span class="sxs-lookup"><span data-stu-id="e465c-198">c.</span></span> <span data-ttu-id="e465c-199">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="e465c-199">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e465c-200">d.</span><span class="sxs-lookup"><span data-stu-id="e465c-200">d.</span></span> <span data-ttu-id="e465c-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e465c-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="e465c-202">Создание тестового пользователя YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="e465c-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="e465c-203">В этом разделе описано, как создать пользователя Britta Simon в приложении YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="e465c-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="e465c-204">Обратитесь пользователи YouEarnedIt поддержки team tooadd hello в платформе YouEarnedIt hello.</span><span class="sxs-lookup"><span data-stu-id="e465c-204">Please work with YouEarnedIt support team tooadd hello users in hello YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="e465c-205">YouEarnedIt ожидать hello поставщика удостоверений toosupply EmailAddress или имя пользователя в атрибуте идентификатора имени hello.</span><span class="sxs-lookup"><span data-stu-id="e465c-205">YouEarnedIt expect hello Identity Provider toosupply an EmailAddress  or UserName in hello NameID attribute.</span></span> <span data-ttu-id="e465c-206">Если соответствующие имя пользователя или EmailAddress не найден в базе данных hello, или не полностью совпадают, пройдет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="e465c-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within hello database or does not match exactly.</span></span> <span data-ttu-id="e465c-207">Для этого потребуется, импортировать учетные записи в систему YouEarnedIt hello перед hello интеграция единого входа (обычно либо посредством импорта API или CSV).</span><span class="sxs-lookup"><span data-stu-id="e465c-207">This will require that accounts be imported into hello YouEarnedIt system before hello SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e465c-208">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="e465c-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e465c-209">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooYouEarnedIt доступа.</span><span class="sxs-lookup"><span data-stu-id="e465c-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYouEarnedIt.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="e465c-211">**tooassign tooYouEarnedIt Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e465c-211">**tooassign Britta Simon tooYouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="e465c-212">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e465c-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e465c-214">В списке приложений hello выберите **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="e465c-214">In hello applications list, select **YouEarnedIt**.</span></span>

    ![ссылка YouEarnedIt Hello в списке приложений hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="e465c-216">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e465c-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="e465c-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e465c-218">Click **Add** button.</span></span> <span data-ttu-id="e465c-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e465c-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="e465c-221">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e465c-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e465c-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e465c-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e465c-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e465c-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e465c-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e465c-224">Test single sign-on</span></span>

<span data-ttu-id="e465c-225">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="e465c-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e465c-226">При нажатии кнопки hello YouEarnedIt плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour YouEarnedIt приложения.</span><span class="sxs-lookup"><span data-stu-id="e465c-226">When you click hello YouEarnedIt tile in hello Access Panel, you should get automatically signed-on tooyour YouEarnedIt application.</span></span>
<span data-ttu-id="e465c-227">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e465c-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e465c-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e465c-228">Additional resources</span></span>

* [<span data-ttu-id="e465c-229">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e465c-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e465c-230">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e465c-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

