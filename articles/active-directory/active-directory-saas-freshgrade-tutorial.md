---
title: "Учебник. Интеграция Azure Active Directory с FreshGrade | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FreshGrade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2fe7cedd45290945ec5624453a9675abdd7726d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="bec91-103">Учебник. Интеграция Azure Active Directory с FreshGrade</span><span class="sxs-lookup"><span data-stu-id="bec91-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="bec91-104">В этом учебнике вы узнаете, как toointegrate FreshGrade с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bec91-104">In this tutorial, you learn how toointegrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bec91-105">Интеграция с Azure AD FreshGrade предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bec91-105">Integrating FreshGrade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bec91-106">Можно управлять в Azure AD, имеющего доступ tooFreshGrade</span><span class="sxs-lookup"><span data-stu-id="bec91-106">You can control in Azure AD who has access tooFreshGrade</span></span>
- <span data-ttu-id="bec91-107">Можно включить на пользователей tooautomatically get вошедшего tooFreshGrade (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="bec91-107">You can enable your users tooautomatically get signed-on tooFreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bec91-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bec91-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bec91-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bec91-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bec91-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bec91-110">Prerequisites</span></span>

<span data-ttu-id="bec91-111">tooconfigure интеграция Azure AD с FreshGrade требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="bec91-111">tooconfigure Azure AD integration with FreshGrade, you need hello following items:</span></span>

- <span data-ttu-id="bec91-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bec91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bec91-113">подписка FreshGrade с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bec91-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bec91-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bec91-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bec91-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="bec91-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bec91-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bec91-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bec91-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bec91-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bec91-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bec91-118">Scenario description</span></span>
<span data-ttu-id="bec91-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bec91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bec91-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="bec91-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bec91-121">Добавление FreshGrade из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bec91-121">Adding FreshGrade from hello gallery</span></span>
2. <span data-ttu-id="bec91-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bec91-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-hello-gallery"></a><span data-ttu-id="bec91-123">Добавление FreshGrade из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bec91-123">Adding FreshGrade from hello gallery</span></span>
<span data-ttu-id="bec91-124">tooconfigure hello интеграции FreshGrade в Azure AD, вы должны tooadd FreshGrade из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bec91-124">tooconfigure hello integration of FreshGrade into Azure AD, you need tooadd FreshGrade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bec91-125">**tooadd FreshGrade из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bec91-125">**tooadd FreshGrade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bec91-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bec91-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bec91-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="bec91-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bec91-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bec91-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bec91-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bec91-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bec91-133">Введите в поле поиска hello **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="bec91-133">In hello search box, type **FreshGrade**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="bec91-135">В панели результатов hello выберите **FreshGrade**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bec91-135">In hello results panel, select **FreshGrade**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bec91-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bec91-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bec91-138">В этом разделе описана настройка и проверка единого входа Azure AD во FreshGrade с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bec91-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bec91-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FreshGrade является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bec91-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshGrade is tooa user in Azure AD.</span></span> <span data-ttu-id="bec91-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в FreshGrade должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="bec91-140">In other words, a link relationship between an Azure AD user and hello related user in FreshGrade needs toobe established.</span></span>

<span data-ttu-id="bec91-141">В FreshGrade, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="bec91-141">In FreshGrade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bec91-142">tooconfigure и теста Azure AD единого входа с FreshGrade, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bec91-142">tooconfigure and test Azure AD single sign-on with FreshGrade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bec91-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="bec91-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bec91-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bec91-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bec91-145">**[Создание тестового пользователя FreshGrade](#creating-a-freshgrade-test-user)**  -toohave аналог Саймон Britta в FreshGrade, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="bec91-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - toohave a counterpart of Britta Simon in FreshGrade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bec91-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="bec91-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bec91-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bec91-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bec91-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bec91-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bec91-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="bec91-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="bec91-150">**tooconfigure Azure AD единого входа с FreshGrade, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bec91-150">**tooconfigure Azure AD single sign-on with FreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="bec91-151">В hello в hello портала Azure **FreshGrade** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bec91-151">In hello Azure portal, on hello **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bec91-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="bec91-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="bec91-155">На hello **URL-адреса и домена FreshGrade** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bec91-155">On hello **FreshGrade Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="bec91-157">а.</span><span class="sxs-lookup"><span data-stu-id="bec91-157">a.</span></span> <span data-ttu-id="bec91-158">В hello **URL-адрес входа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="bec91-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="bec91-159">b.</span><span class="sxs-lookup"><span data-stu-id="bec91-159">b.</span></span> <span data-ttu-id="bec91-160">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="bec91-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="bec91-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="bec91-161">These values are not real.</span></span> <span data-ttu-id="bec91-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="bec91-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bec91-163">Обратитесь к [группа поддержки клиента FreshGrade](mailTo:support@freshgrade.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="bec91-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="bec91-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="bec91-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="bec91-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bec91-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bec91-168">На hello **конфигурации FreshGrade** щелкните **Настройка FreshGrade** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="bec91-168">On hello **FreshGrade Configuration** section, click **Configure FreshGrade** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bec91-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="bec91-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="bec91-171">toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bec91-171">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="bec91-172">а.</span><span class="sxs-lookup"><span data-stu-id="bec91-172">a.</span></span> <span data-ttu-id="bec91-173">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="bec91-173">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="bec91-175">b.</span><span class="sxs-lookup"><span data-stu-id="bec91-175">b.</span></span> <span data-ttu-id="bec91-176">Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="bec91-176">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="bec91-178">c.</span><span class="sxs-lookup"><span data-stu-id="bec91-178">c.</span></span> <span data-ttu-id="bec91-179">Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="bec91-179">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="bec91-181">d.</span><span class="sxs-lookup"><span data-stu-id="bec91-181">d.</span></span> <span data-ttu-id="bec91-182">Теперь перейдите на странице свойств toohello **FreshGrade** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="bec91-182">Now go toohello property page of **FreshGrade** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="bec91-184">д.</span><span class="sxs-lookup"><span data-stu-id="bec91-184">e.</span></span> <span data-ttu-id="bec91-185">Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="bec91-185">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="bec91-186">tooconfigure единого входа на **FreshGrade** параллельно, необходимо toosend hello **URL-адрес метаданных** и **SAML единого входа URL-адрес службы** слишком[FreshGrade поддержки](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="bec91-186">tooconfigure single sign-on on **FreshGrade** side, you need toosend hello **Metadata URL** and **SAML Single Sign-On Service URL** too[FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="bec91-187">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="bec91-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bec91-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="bec91-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bec91-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="bec91-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bec91-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bec91-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bec91-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bec91-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="bec91-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bec91-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bec91-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bec91-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bec91-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bec91-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bec91-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bec91-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bec91-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="bec91-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bec91-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bec91-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bec91-203">а.</span><span class="sxs-lookup"><span data-stu-id="bec91-203">a.</span></span> <span data-ttu-id="bec91-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bec91-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bec91-205">b.</span><span class="sxs-lookup"><span data-stu-id="bec91-205">b.</span></span> <span data-ttu-id="bec91-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bec91-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bec91-207">c.</span><span class="sxs-lookup"><span data-stu-id="bec91-207">c.</span></span> <span data-ttu-id="bec91-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="bec91-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bec91-209">d.</span><span class="sxs-lookup"><span data-stu-id="bec91-209">d.</span></span> <span data-ttu-id="bec91-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bec91-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="bec91-211">Создание тестового пользователя FreshGrade</span><span class="sxs-lookup"><span data-stu-id="bec91-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="bec91-212">В этом разделе описано, как создать пользователя Britta Simon в приложении FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="bec91-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="bec91-213">Можно работать с [FreshGrade поддержки](mailTo:support@freshgrade.com) tooadd hello пользователей на платформе FreshGrade hello.</span><span class="sxs-lookup"><span data-stu-id="bec91-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) tooadd hello users in hello FreshGrade platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bec91-214">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bec91-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bec91-215">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooFreshGrade доступа.</span><span class="sxs-lookup"><span data-stu-id="bec91-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFreshGrade.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bec91-217">**tooassign tooFreshGrade Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bec91-217">**tooassign Britta Simon tooFreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="bec91-218">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bec91-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bec91-220">В списке приложений hello выберите **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="bec91-220">In hello applications list, select **FreshGrade**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="bec91-222">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="bec91-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bec91-224">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bec91-224">Click **Add** button.</span></span> <span data-ttu-id="bec91-225">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bec91-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bec91-227">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="bec91-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bec91-228">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bec91-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bec91-229">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bec91-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bec91-230">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bec91-230">Testing single sign-on</span></span>

<span data-ttu-id="bec91-231">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="bec91-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bec91-232">При нажатии кнопки hello FreshGrade плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour FreshGrade приложения.</span><span class="sxs-lookup"><span data-stu-id="bec91-232">When you click hello FreshGrade tile in hello Access Panel, you should get automatically signed-on tooyour FreshGrade application.</span></span>
<span data-ttu-id="bec91-233">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bec91-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bec91-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bec91-234">Additional resources</span></span>

* [<span data-ttu-id="bec91-235">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bec91-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bec91-236">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bec91-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

