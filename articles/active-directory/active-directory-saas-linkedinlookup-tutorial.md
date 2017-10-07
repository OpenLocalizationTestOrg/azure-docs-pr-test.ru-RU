---
title: "Руководство по интеграции Azure Active Directory с LinkedIn Lookup | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LinkedIn уточняющего запроса."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="1c357-103">Руководство по интеграции Azure Active Directory с LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="1c357-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="1c357-104">В этом учебнике вы узнаете, как toointegrate уточняющего запроса LinkedIn с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c357-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c357-105">Интеграция LinkedIn подстановки с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1c357-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1c357-106">Можно управлять в Azure AD, имеющего доступ tooLinkedIn уточняющего запроса</span><span class="sxs-lookup"><span data-stu-id="1c357-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="1c357-107">Можно включить вашей пользователей tooautomatically get вошедшего tooLinkedIn уточняющего запроса (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c357-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c357-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1c357-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1c357-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c357-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c357-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1c357-110">Prerequisites</span></span>

<span data-ttu-id="1c357-111">tooconfigure интеграция Azure AD с LinkedIn подстановки необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1c357-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="1c357-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1c357-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c357-113">подписка LinkedIn Lookup с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1c357-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c357-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1c357-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c357-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1c357-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c357-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1c357-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c357-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c357-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c357-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1c357-118">Scenario description</span></span>
<span data-ttu-id="1c357-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1c357-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c357-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1c357-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c357-121">Добавление LinkedIn поиска из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1c357-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="1c357-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c357-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="1c357-123">Добавление LinkedIn поиска из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1c357-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="1c357-124">tooconfigure hello интеграции LinkedIn уточняющего запроса в Azure AD, вы должны tooadd LinkedIn поиска из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1c357-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c357-125">**tooadd LinkedIn поиска из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1c357-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c357-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1c357-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c357-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1c357-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1c357-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1c357-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1c357-131">Нажмите кнопку **новое приложение** кнопку сверху "hello" hello диалоговое окно tooadd новое приложение.</span><span class="sxs-lookup"><span data-stu-id="1c357-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1c357-133">Введите в поле поиска hello **уточняющего запроса LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="1c357-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="1c357-135">В панели результатов hello, выберите **уточняющего запроса LinkedIn**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1c357-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c357-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c357-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c357-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложении LinkedIn Lookup с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c357-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c357-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в уточняющем запросе LinkedIn является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c357-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="1c357-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в уточняющем запросе LinkedIn должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="1c357-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="1c357-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в уточняющем запросе LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1c357-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="1c357-142">tooconfigure и теста Azure AD единого входа с LinkedIn уточняющего запроса, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="1c357-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1c357-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1c357-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1c357-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1c357-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c357-145">**[Создание тестового пользователя, прошедшего подстановки LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave аналог Саймон Britta в уточняющем запросе LinkedIn, представление связанных toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c357-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="1c357-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1c357-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c357-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1c357-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c357-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c357-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c357-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LinkedIn уточняющего запроса.</span><span class="sxs-lookup"><span data-stu-id="1c357-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="1c357-150">**tooconfigure Azure AD единого входа при поиске LinkedIn выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1c357-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c357-151">В hello в hello портала Azure **уточняющего запроса LinkedIn** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1c357-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1c357-153">На hello **единого входа** диалоговое окно, в **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1c357-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="1c357-155">В другом окне браузера, tooyour входа **уточняющего запроса LinkedIn** веб-сайта от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="1c357-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="1c357-156">В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры).</span><span class="sxs-lookup"><span data-stu-id="1c357-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="1c357-157">Кроме того, установите **уточняющего запроса** hello в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="1c357-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="1c357-159">Нажмите кнопку **или щелкните здесь tooload и скопируйте отдельные поля из формы hello** и скопируйте **идентификатор сущности** и **URL-адрес утверждение потребителя доступа (ACS)**</span><span class="sxs-lookup"><span data-stu-id="1c357-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="1c357-161">На портале Azure в разделе **LinkedIn просмотр доменов и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="1c357-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="1c357-163">а.</span><span class="sxs-lookup"><span data-stu-id="1c357-163">a.</span></span> <span data-ttu-id="1c357-164">В hello **идентификатор** текстовом поле введите hello **идентификатор сущности** копируются LinkedIn портала</span><span class="sxs-lookup"><span data-stu-id="1c357-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="1c357-165">b.</span><span class="sxs-lookup"><span data-stu-id="1c357-165">b.</span></span> <span data-ttu-id="1c357-166">В hello **URL-адрес ответа** текстовом поле введите hello **утверждение потребителя доступа (ACS) URL-адрес** копируются LinkedIn портала</span><span class="sxs-lookup"><span data-stu-id="1c357-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="1c357-167">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="1c357-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="1c357-169">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="1c357-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1c357-170">Не является действительным значением.</span><span class="sxs-lookup"><span data-stu-id="1c357-170">This is not real value.</span></span> <span data-ttu-id="1c357-171">Hello пользователем tooupdate эти значения с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="1c357-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="1c357-172">Обратитесь к [уточняющего запроса клиент LinkedIn поддержки](https://business.LinkedIn.com/lookup) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="1c357-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="1c357-173">Ваш **уточняющего запроса LinkedIn** приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="1c357-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1c357-174">Hello пользователем конфигурация атрибутов токена SAML toohello сопоставления tooadd настраиваемого атрибута.</span><span class="sxs-lookup"><span data-stu-id="1c357-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="1c357-175">Следующий снимок экрана приветствия показан пример.</span><span class="sxs-lookup"><span data-stu-id="1c357-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="1c357-176">значение по умолчанию Hello **идентификатор пользователя** — **user.userprincipalname** , но это toobe, сопоставленный с адресом электронной почты пользователя hello ожидает LinkedIn уточняющего запроса.</span><span class="sxs-lookup"><span data-stu-id="1c357-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="1c357-177">Можно использовать **user.mail** атрибут из списка hello, или используйте hello соответствующее значение атрибута на основе конфигурации в организации.</span><span class="sxs-lookup"><span data-stu-id="1c357-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="1c357-179">В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello.</span><span class="sxs-lookup"><span data-stu-id="1c357-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="1c357-180">Hello пользователь должен tooadd четыре утверждения с именем **электронной почты**, **отдел**, **firstname**, и **lastname** и hello значение — toobe сопоставлено с **user.mail**, **user.department**, **user.givenname**, и **user.surname** соответственно</span><span class="sxs-lookup"><span data-stu-id="1c357-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="1c357-181">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="1c357-181">Attribute Name</span></span> | <span data-ttu-id="1c357-182">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="1c357-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1c357-183">email</span><span class="sxs-lookup"><span data-stu-id="1c357-183">email</span></span>| <span data-ttu-id="1c357-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="1c357-184">user.mail</span></span> |    
    | <span data-ttu-id="1c357-185">department</span><span class="sxs-lookup"><span data-stu-id="1c357-185">department</span></span>| <span data-ttu-id="1c357-186">user.department</span><span class="sxs-lookup"><span data-stu-id="1c357-186">user.department</span></span> |
    | <span data-ttu-id="1c357-187">firstname</span><span class="sxs-lookup"><span data-stu-id="1c357-187">firstname</span></span>| <span data-ttu-id="1c357-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1c357-188">user.givenname</span></span> |
    | <span data-ttu-id="1c357-189">lastname</span><span class="sxs-lookup"><span data-stu-id="1c357-189">lastname</span></span>| <span data-ttu-id="1c357-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="1c357-190">user.surname</span></span> |

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="1c357-192">а.</span><span class="sxs-lookup"><span data-stu-id="1c357-192">a.</span></span> <span data-ttu-id="1c357-193">Нажмите кнопку **Добавление атрибута** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1c357-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="1c357-196">b.</span><span class="sxs-lookup"><span data-stu-id="1c357-196">b.</span></span> <span data-ttu-id="1c357-197">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="1c357-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1c357-198">c.</span><span class="sxs-lookup"><span data-stu-id="1c357-198">c.</span></span> <span data-ttu-id="1c357-199">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="1c357-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1c357-200">d.</span><span class="sxs-lookup"><span data-stu-id="1c357-200">d.</span></span> <span data-ttu-id="1c357-201">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1c357-201">Click **Ok**</span></span>

10. <span data-ttu-id="1c357-202">Выполните следующие действия на hello hello **имя** атрибута -</span><span class="sxs-lookup"><span data-stu-id="1c357-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="1c357-203">а.</span><span class="sxs-lookup"><span data-stu-id="1c357-203">a.</span></span> <span data-ttu-id="1c357-204">Щелкните hello атрибут tooopen hello **изменение атрибута** окна.</span><span class="sxs-lookup"><span data-stu-id="1c357-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="1c357-206">b.</span><span class="sxs-lookup"><span data-stu-id="1c357-206">b.</span></span> <span data-ttu-id="1c357-207">Удалить значение URL-адрес hello из hello **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="1c357-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="1c357-208">c.</span><span class="sxs-lookup"><span data-stu-id="1c357-208">c.</span></span> <span data-ttu-id="1c357-209">Нажмите кнопку **ОК** toosave приветствия.</span><span class="sxs-lookup"><span data-stu-id="1c357-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="1c357-210">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1c357-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="1c357-212">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1c357-212">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="1c357-214">Go слишком**параметры администрирования LinkedIn** раздела.</span><span class="sxs-lookup"><span data-stu-id="1c357-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="1c357-215">Отправка hello XML-файл, загруженный с портала Azure hello, щелкнув hello **отправить XML-файл** параметр.</span><span class="sxs-lookup"><span data-stu-id="1c357-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="1c357-217">Нажмите кнопку **на** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1c357-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="1c357-218">Изменение состояния единого входа с **не подключены** слишком**подключено**</span><span class="sxs-lookup"><span data-stu-id="1c357-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="1c357-220">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1c357-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1c357-221">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1c357-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1c357-222">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c357-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c357-223">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c357-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c357-224">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1c357-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1c357-226">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1c357-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c357-227">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1c357-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c357-229">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1c357-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c357-231">Нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1c357-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c357-233">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1c357-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c357-235">а.</span><span class="sxs-lookup"><span data-stu-id="1c357-235">a.</span></span> <span data-ttu-id="1c357-236">В hello **имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1c357-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="1c357-237">b.</span><span class="sxs-lookup"><span data-stu-id="1c357-237">b.</span></span> <span data-ttu-id="1c357-238">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1c357-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="1c357-239">c.</span><span class="sxs-lookup"><span data-stu-id="1c357-239">c.</span></span> <span data-ttu-id="1c357-240">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="1c357-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1c357-241">d.</span><span class="sxs-lookup"><span data-stu-id="1c357-241">d.</span></span> <span data-ttu-id="1c357-242">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1c357-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="1c357-243">Создание тестового пользователя LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="1c357-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="1c357-244">Связанное приложение поиска поддерживает только в подготовки пользователей Time (JIT) и после проверки подлинности пользователей автоматически создаются в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="1c357-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="1c357-245">Активировать **автоматически назначать лицензии** tooassign toohello лицензии пользователя.</span><span class="sxs-lookup"><span data-stu-id="1c357-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1c357-247">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1c357-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1c357-248">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLinkedIn уточняющего запроса.</span><span class="sxs-lookup"><span data-stu-id="1c357-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1c357-250">**tooassign tooLinkedIn Britta Simon уточняющего запроса, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1c357-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c357-251">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1c357-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1c357-253">В списке приложений hello выберите **уточняющего запроса LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="1c357-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="1c357-255">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1c357-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1c357-257">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c357-257">Click **Add** button.</span></span> <span data-ttu-id="1c357-258">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1c357-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1c357-260">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1c357-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1c357-261">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1c357-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c357-262">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1c357-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c357-263">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1c357-263">Testing single sign-on</span></span>

<span data-ttu-id="1c357-264">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="1c357-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1c357-265">При нажатии кнопки hello, LinkedIn подстановки плитки в панели доступа hello, должна быть страницей перенаправленный tooOrganizational, при наличии tooprovide личные сведения учетной записи LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1c357-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="1c357-266">В результате ваша личная учетная запись связывается с вашей рабочей учетной записью LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1c357-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="1c357-267">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c357-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1c357-268">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1c357-268">Additional resources</span></span>

* [<span data-ttu-id="1c357-269">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c357-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c357-270">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c357-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

