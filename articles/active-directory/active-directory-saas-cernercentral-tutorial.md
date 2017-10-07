---
title: "Руководство по интеграции Azure Active Directory с Cerner Central | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и центр Cerner."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="ff256-103">Руководство. Интеграция Azure Active Directory с Cerner Central</span><span class="sxs-lookup"><span data-stu-id="ff256-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="ff256-104">В этом учебнике вы узнаете, как toointegrate центральный Cerner с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff256-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff256-105">Интеграция с Azure AD центральный Cerner предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ff256-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ff256-106">Можно управлять в Azure AD, имеющего доступ tooCerner центральный</span><span class="sxs-lookup"><span data-stu-id="ff256-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="ff256-107">Можно включить на пользователей tooautomatically get вошедшего tooCerner центральный (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff256-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff256-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ff256-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ff256-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff256-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff256-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ff256-110">Prerequisites</span></span>

<span data-ttu-id="ff256-111">tooconfigure интеграция Azure AD с центрального Cerner требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ff256-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="ff256-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ff256-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff256-113">утвержденная системная учетная запись Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="ff256-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="ff256-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ff256-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff256-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ff256-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff256-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff256-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff256-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff256-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff256-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ff256-118">Scenario description</span></span>
<span data-ttu-id="ff256-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ff256-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff256-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ff256-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff256-121">Добавление центральный Cerner из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ff256-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="ff256-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff256-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="ff256-123">Добавление центральный Cerner из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ff256-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="ff256-124">tooconfigure hello интеграции центральный Cerner в Azure AD, вы должны tooadd центральный Cerner из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ff256-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ff256-125">**tooadd центральный Cerner из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="ff256-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff256-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ff256-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ff256-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ff256-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ff256-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff256-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ff256-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопки на диалоговое окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="ff256-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ff256-133">Введите в поле поиска hello **Cerner центральный**.</span><span class="sxs-lookup"><span data-stu-id="ff256-133">In hello search box, type **Cerner Central**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="ff256-135">В панели результатов hello выберите **центральный Cerner**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ff256-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff256-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff256-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff256-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Cerner Central с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff256-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ff256-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в центральный Cerner является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff256-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="ff256-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в центральный Cerner должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ff256-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="ff256-141">tooconfigure и теста Azure AD единого входа с центрального Cerner, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ff256-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ff256-142">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ff256-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ff256-143">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ff256-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff256-144">**[Создание тестового пользователя центральный Cerner](#creating-a-cerner-central-test-user)**  -toohave аналог Саймон Britta в центральный Cerner, являющийся представлением пользовательского hello связанного toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff256-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="ff256-145">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ff256-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff256-146">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ff256-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff256-147">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff256-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff256-148">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении центральный Cerner.</span><span class="sxs-lookup"><span data-stu-id="ff256-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="ff256-149">**tooconfigure Azure AD единого входа с центрального Cerner выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ff256-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff256-150">В hello в hello портала Azure **центральный Cerner** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ff256-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ff256-152">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ff256-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="ff256-154">На hello **URL-адреса и домена центра Cerner** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ff256-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="ff256-156">а.</span><span class="sxs-lookup"><span data-stu-id="ff256-156">a.</span></span> <span data-ttu-id="ff256-157">В hello **идентификатор** текстовое значение hello типа с помощью hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="ff256-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="ff256-158">b.</span><span class="sxs-lookup"><span data-stu-id="ff256-158">b.</span></span> <span data-ttu-id="ff256-159">В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="ff256-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="ff256-160">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="ff256-160">These values are not hello real.</span></span> <span data-ttu-id="ff256-161">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ff256-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ff256-162">Обратитесь к [Cerner центральная группа поддержки](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ff256-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="ff256-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ff256-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="ff256-165">toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ff256-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="ff256-166">а.</span><span class="sxs-lookup"><span data-stu-id="ff256-166">a.</span></span> <span data-ttu-id="ff256-167">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="ff256-167">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="ff256-169">b.</span><span class="sxs-lookup"><span data-stu-id="ff256-169">b.</span></span> <span data-ttu-id="ff256-170">Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="ff256-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="ff256-172">c.</span><span class="sxs-lookup"><span data-stu-id="ff256-172">c.</span></span> <span data-ttu-id="ff256-173">Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="ff256-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="ff256-175">d.</span><span class="sxs-lookup"><span data-stu-id="ff256-175">d.</span></span> <span data-ttu-id="ff256-176">Теперь перейдите на странице свойств toohello **центральный Cerner** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="ff256-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="ff256-178">д.</span><span class="sxs-lookup"><span data-stu-id="ff256-178">e.</span></span> <span data-ttu-id="ff256-179">Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="ff256-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="ff256-180">tooconfigure единого входа на **центральный Cerner** параллельно, необходимо toosend hello **URL-адрес метаданных** слишком[Cerner центр поддержки](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="ff256-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="ff256-181">Они настроить hello единого входа для интеграции hello toocomplete стороне приложений.</span><span class="sxs-lookup"><span data-stu-id="ff256-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="ff256-182">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ff256-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ff256-183">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ff256-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ff256-184">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff256-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff256-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff256-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff256-186">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ff256-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Создание пользователя Azure AD][100]

<span data-ttu-id="ff256-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ff256-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff256-189">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ff256-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff256-191">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ff256-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff256-193">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff256-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff256-195">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ff256-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff256-197">а.</span><span class="sxs-lookup"><span data-stu-id="ff256-197">a.</span></span> <span data-ttu-id="ff256-198">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff256-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff256-199">b.</span><span class="sxs-lookup"><span data-stu-id="ff256-199">b.</span></span> <span data-ttu-id="ff256-200">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ff256-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="ff256-201">c.</span><span class="sxs-lookup"><span data-stu-id="ff256-201">c.</span></span> <span data-ttu-id="ff256-202">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ff256-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ff256-203">d.</span><span class="sxs-lookup"><span data-stu-id="ff256-203">d.</span></span> <span data-ttu-id="ff256-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ff256-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="ff256-205">Создание тестового пользователя Cerner Central</span><span class="sxs-lookup"><span data-stu-id="ff256-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="ff256-206">Приложение **Cerner Central** разрешает аутентификацию посредством любого поставщика федеративных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="ff256-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="ff256-207">Если пользователь может toolog в домашней страницы приложения toohello, они включаются в федерацию и не требуется вручную подготовки.</span><span class="sxs-lookup"><span data-stu-id="ff256-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ff256-208">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ff256-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ff256-209">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCerner центральный.</span><span class="sxs-lookup"><span data-stu-id="ff256-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ff256-211">**tooassign tooCerner Britta Simon центральный, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="ff256-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff256-212">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff256-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ff256-214">В списке приложений hello выберите **Cerner центральный**.</span><span class="sxs-lookup"><span data-stu-id="ff256-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="ff256-216">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ff256-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ff256-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff256-218">Click **Add** button.</span></span> <span data-ttu-id="ff256-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ff256-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ff256-221">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ff256-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ff256-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ff256-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff256-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ff256-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ff256-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ff256-224">Testing single sign-on</span></span>

<span data-ttu-id="ff256-225">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ff256-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ff256-226">При нажатии кнопки hello центральный Cerner плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на центральный Cerner приложения.</span><span class="sxs-lookup"><span data-stu-id="ff256-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="ff256-227">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ff256-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff256-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ff256-228">Additional resources</span></span>

* [<span data-ttu-id="ff256-229">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff256-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff256-230">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff256-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

