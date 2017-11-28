---
title: "Руководство по интеграции Azure Active Directory и StatusPage | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и StatusPage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="129b9-103">Руководство. Интеграция Azure Active Directory и StatusPage</span><span class="sxs-lookup"><span data-stu-id="129b9-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="129b9-104">В этом учебнике вы узнаете, как toointegrate StatusPage с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="129b9-104">In this tutorial, you learn how toointegrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="129b9-105">Интеграция с Azure AD StatusPage предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="129b9-105">Integrating StatusPage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="129b9-106">Можно управлять в Azure AD, имеющего доступ tooStatusPage</span><span class="sxs-lookup"><span data-stu-id="129b9-106">You can control in Azure AD who has access tooStatusPage</span></span>
- <span data-ttu-id="129b9-107">Можно включить на пользователей tooautomatically get вошедшего tooStatusPage (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="129b9-107">You can enable your users tooautomatically get signed-on tooStatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="129b9-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="129b9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="129b9-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="129b9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="129b9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="129b9-110">Prerequisites</span></span>

<span data-ttu-id="129b9-111">tooconfigure интеграция Azure AD с StatusPage требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="129b9-111">tooconfigure Azure AD integration with StatusPage, you need hello following items:</span></span>

- <span data-ttu-id="129b9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="129b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="129b9-113">подписка StatusPage с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="129b9-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="129b9-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="129b9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="129b9-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="129b9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="129b9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="129b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="129b9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="129b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="129b9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="129b9-118">Scenario description</span></span>
<span data-ttu-id="129b9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="129b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="129b9-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="129b9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="129b9-121">Добавление StatusPage из галереи hello</span><span class="sxs-lookup"><span data-stu-id="129b9-121">Adding StatusPage from hello gallery</span></span>
2. <span data-ttu-id="129b9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="129b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-hello-gallery"></a><span data-ttu-id="129b9-123">Добавление StatusPage из галереи hello</span><span class="sxs-lookup"><span data-stu-id="129b9-123">Adding StatusPage from hello gallery</span></span>
<span data-ttu-id="129b9-124">tooconfigure hello интеграции StatusPage в Azure AD, вы должны tooadd StatusPage из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="129b9-124">tooconfigure hello integration of StatusPage into Azure AD, you need tooadd StatusPage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="129b9-125">**tooadd StatusPage из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129b9-125">**tooadd StatusPage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="129b9-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="129b9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="129b9-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="129b9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="129b9-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="129b9-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="129b9-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="129b9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="129b9-133">Введите в поле поиска hello **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="129b9-133">In hello search box, type **StatusPage**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="129b9-135">В панели результатов hello выберите **StatusPage**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="129b9-135">In hello results panel, select **StatusPage**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="129b9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="129b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="129b9-138">В этом разделе описана настройка и проверка единого входа Azure AD в StatusPage с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="129b9-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="129b9-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в StatusPage является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="129b9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in StatusPage is tooa user in Azure AD.</span></span> <span data-ttu-id="129b9-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в StatusPage должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="129b9-140">In other words, a link relationship between an Azure AD user and hello related user in StatusPage needs toobe established.</span></span>

<span data-ttu-id="129b9-141">В StatusPage, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="129b9-141">In StatusPage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="129b9-142">tooconfigure и теста Azure AD единого входа с StatusPage, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="129b9-142">tooconfigure and test Azure AD single sign-on with StatusPage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="129b9-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="129b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="129b9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="129b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="129b9-145">**[Создание тестового пользователя StatusPage](#creating-a-statuspage-test-user)**  -toohave аналог Саймон Britta в StatusPage, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="129b9-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - toohave a counterpart of Britta Simon in StatusPage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="129b9-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="129b9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="129b9-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="129b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="129b9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="129b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="129b9-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении StatusPage.</span><span class="sxs-lookup"><span data-stu-id="129b9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="129b9-150">**tooconfigure Azure AD единого входа с StatusPage, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129b9-150">**tooconfigure Azure AD single sign-on with StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="129b9-151">В hello в hello портала Azure **StatusPage** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="129b9-151">In hello Azure portal, on hello **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="129b9-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="129b9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="129b9-155">На hello **URL-адреса и домена StatusPage** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="129b9-155">On hello **StatusPage Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="129b9-157">а.</span><span class="sxs-lookup"><span data-stu-id="129b9-157">a.</span></span> <span data-ttu-id="129b9-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="129b9-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="129b9-159">b.</span><span class="sxs-lookup"><span data-stu-id="129b9-159">b.</span></span> <span data-ttu-id="129b9-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="129b9-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="129b9-161">Обратитесь в службу поддержки StatusPage hello в [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest метаданных необходимые tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="129b9-161">Contact hello StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)toorequest metadata necessary tooconfigure single sign-on.</span></span> 
    >
    ><span data-ttu-id="129b9-162">а.</span><span class="sxs-lookup"><span data-stu-id="129b9-162">a.</span></span> <span data-ttu-id="129b9-163">Из метаданных hello, скопируйте значение издателя hello и вставьте его в hello **идентификатор** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="129b9-163">From hello metadata, copy hello Issuer value, and then paste it into hello **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="129b9-164">b.</span><span class="sxs-lookup"><span data-stu-id="129b9-164">b.</span></span> <span data-ttu-id="129b9-165">Из метаданных hello hello URL-адрес ответа скопируйте и вставьте его в hello **URL-адрес ответа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="129b9-165">From hello metadata, copy hello Reply URL, and then paste it into hello **Reply URL** textbox.</span></span>

4. <span data-ttu-id="129b9-166">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="129b9-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="129b9-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="129b9-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="129b9-170">На hello **конфигурации StatusPage** щелкните **Настройка StatusPage** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="129b9-170">On hello **StatusPage Configuration** section, click **Configure StatusPage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="129b9-171">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="129b9-171">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="129b9-173">В другом окне браузера Войдите на сайт компании StatusPage tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="129b9-173">In another browser window, sign on tooyour StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="129b9-174">На главной панели инструментов hello, щелкните **Управление учетной записью**.</span><span class="sxs-lookup"><span data-stu-id="129b9-174">In hello main toolbar, click **Manage Account**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="129b9-176">Нажмите кнопку hello **Single Sign-on** вкладки.</span><span class="sxs-lookup"><span data-stu-id="129b9-176">Click hello **Single Sign-on** tab.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="129b9-178">На странице настройки единого входа hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="129b9-178">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="129b9-181">а.</span><span class="sxs-lookup"><span data-stu-id="129b9-181">a.</span></span> <span data-ttu-id="129b9-182">В hello **URL-адрес единого входа для целевого** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="129b9-182">In hello **SSO Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="129b9-183">b.</span><span class="sxs-lookup"><span data-stu-id="129b9-183">b.</span></span> <span data-ttu-id="129b9-184">Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="129b9-184">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span> 

    <span data-ttu-id="129b9-185">c.</span><span class="sxs-lookup"><span data-stu-id="129b9-185">c.</span></span> <span data-ttu-id="129b9-186">Щелкните **SAVE CONFIGURATION** (Сохранить конфигурацию).</span><span class="sxs-lookup"><span data-stu-id="129b9-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="129b9-187">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="129b9-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="129b9-188">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="129b9-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="129b9-189">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="129b9-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="129b9-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="129b9-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="129b9-191">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="129b9-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="129b9-193">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129b9-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="129b9-194">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="129b9-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="129b9-196">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="129b9-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="129b9-198">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="129b9-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="129b9-200">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="129b9-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="129b9-202">а.</span><span class="sxs-lookup"><span data-stu-id="129b9-202">a.</span></span> <span data-ttu-id="129b9-203">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="129b9-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="129b9-204">b.</span><span class="sxs-lookup"><span data-stu-id="129b9-204">b.</span></span> <span data-ttu-id="129b9-205">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="129b9-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="129b9-206">c.</span><span class="sxs-lookup"><span data-stu-id="129b9-206">c.</span></span> <span data-ttu-id="129b9-207">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="129b9-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="129b9-208">d.</span><span class="sxs-lookup"><span data-stu-id="129b9-208">d.</span></span> <span data-ttu-id="129b9-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="129b9-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="129b9-210">Создание тестового пользователя в приложении StatusPage</span><span class="sxs-lookup"><span data-stu-id="129b9-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="129b9-211">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в StatusPage.</span><span class="sxs-lookup"><span data-stu-id="129b9-211">hello objective of this section is toocreate a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="129b9-212">Приложение StatusPage поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="129b9-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="129b9-213">Эта функция уже включена в ходе [настройки единого входа в Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="129b9-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="129b9-214">**toocreate пользователя с именем Саймон Britta в StatusPage, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129b9-214">**toocreate a user called Britta Simon in StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="129b9-215">Корпоративный сайт StatusPage tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="129b9-215">Sign-on tooyour StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="129b9-216">В меню в верхней части hello hello выберите **Управление учетной записью**.</span><span class="sxs-lookup"><span data-stu-id="129b9-216">In hello menu on hello top, click **Manage Account**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="129b9-218">Нажмите кнопку hello **члены команды** вкладки.</span><span class="sxs-lookup"><span data-stu-id="129b9-218">Click hello **Team Members** tab.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="129b9-220">Щелкните **ADD TEAM MEMBER** (Добавить участника команды).</span><span class="sxs-lookup"><span data-stu-id="129b9-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="129b9-222">Тип hello **адрес электронной почты**, **имя**, и **Sur имя** действительного пользователя требуется tooprovision в hello связанные текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="129b9-222">Type hello **Email Address**, **First Name**, and **Sur Name** of a valid user you want tooprovision into hello related textboxes.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="129b9-224">Для параметра **Role** (Роль) выберите значение **Client Administrator** (Администратор клиента).</span><span class="sxs-lookup"><span data-stu-id="129b9-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="129b9-225">Щелкните **CREATE ACCOUNT** (Создать учетную запись).</span><span class="sxs-lookup"><span data-stu-id="129b9-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="129b9-226">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="129b9-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="129b9-227">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooStatusPage доступа.</span><span class="sxs-lookup"><span data-stu-id="129b9-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooStatusPage.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="129b9-229">**tooassign tooStatusPage Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="129b9-229">**tooassign Britta Simon tooStatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="129b9-230">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="129b9-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="129b9-232">В списке приложений hello выберите **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="129b9-232">In hello applications list, select **StatusPage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="129b9-234">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="129b9-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="129b9-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="129b9-236">Click **Add** button.</span></span> <span data-ttu-id="129b9-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="129b9-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="129b9-239">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="129b9-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="129b9-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="129b9-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="129b9-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="129b9-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="129b9-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="129b9-242">Testing single sign-on</span></span>

<span data-ttu-id="129b9-243">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="129b9-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="129b9-244">При нажатии кнопки hello StatusPage плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour StatusPage приложения.</span><span class="sxs-lookup"><span data-stu-id="129b9-244">When you click hello StatusPage tile in hello Access Panel, you should get automatically signed-on tooyour StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="129b9-245">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="129b9-245">Additional resources</span></span>

* [<span data-ttu-id="129b9-246">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="129b9-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="129b9-247">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="129b9-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

