---
title: "Руководство по интеграции Azure Active Directory с LinkedIn Learning | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LinkedIn обучения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="da8a4-103">Руководство по интеграции Azure Active Directory с LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="da8a4-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="da8a4-104">В этом учебнике вы узнаете, как toointegrate обучения LinkedIn с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="da8a4-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da8a4-105">Интеграция обучения LinkedIn с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="da8a4-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="da8a4-106">Можно управлять в Azure AD, имеющего доступ tooLinkedIn обучения</span><span class="sxs-lookup"><span data-stu-id="da8a4-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="da8a4-107">Можно включить на пользователей tooautomatically get вошедшего tooLinkedIn обучения (Single Sign-On) с использованием их учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="da8a4-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da8a4-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="da8a4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="da8a4-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da8a4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da8a4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="da8a4-110">Prerequisites</span></span>

<span data-ttu-id="da8a4-111">tooconfigure интеграция Azure AD с LinkedIn обучения необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="da8a4-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="da8a4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="da8a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da8a4-113">подписка LinkedIn Learning с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="da8a4-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da8a4-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="da8a4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da8a4-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="da8a4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da8a4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="da8a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da8a4-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da8a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da8a4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="da8a4-118">Scenario description</span></span>
<span data-ttu-id="da8a4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="da8a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da8a4-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="da8a4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da8a4-121">Добавление LinkedIn обучения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="da8a4-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="da8a4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="da8a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="da8a4-123">Добавление LinkedIn обучения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="da8a4-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="da8a4-124">tooconfigure hello интеграции LinkedIn обучения в Azure AD, вы должны tooadd LinkedIn обучения из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="da8a4-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="da8a4-125">**tooadd LinkedIn обучения из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="da8a4-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="da8a4-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="da8a4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da8a4-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="da8a4-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="da8a4-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="da8a4-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="da8a4-133">Введите в поле поиска hello **обучения LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="da8a4-134">На панели результатов щелкните **обучения LinkedIn** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="da8a4-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da8a4-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="da8a4-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da8a4-137">В этом разделе описана настройка и проверка единого входа Azure AD в приложение LinkedIn Learning с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="da8a4-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da8a4-138">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в обучении LinkedIn является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da8a4-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="da8a4-139">Другими словами связи между пользователя Azure AD и связанных пользователей hello в обучении LinkedIn должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="da8a4-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="da8a4-140">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в обучении LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="da8a4-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="da8a4-141">tooconfigure и теста Azure AD единого входа с LinkedIn обучения, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="da8a4-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="da8a4-142">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="da8a4-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="da8a4-143">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="da8a4-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da8a4-144">**[Создание тестового пользователя LinkedIn обучения](#creating-a-linkedin-learning-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="da8a4-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="da8a4-145">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="da8a4-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da8a4-146">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="da8a4-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da8a4-147">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="da8a4-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da8a4-148">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LinkedIn обучения.</span><span class="sxs-lookup"><span data-stu-id="da8a4-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="da8a4-149">**tooconfigure Azure AD единого входа с помощью LinkedIn обучения, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="da8a4-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="da8a4-150">В hello в hello портала Azure **обучения LinkedIn** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="da8a4-152">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="da8a4-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="da8a4-154">В другом окне браузера, клиент LinkedIn обучения tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="da8a4-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="da8a4-155">В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры).</span><span class="sxs-lookup"><span data-stu-id="da8a4-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="da8a4-156">Кроме того, установите **обучения - по умолчанию** hello в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="da8a4-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="da8a4-158">Нажмите кнопку **или щелкните здесь tooload и скопируйте отдельные поля из формы hello** и скопируйте **идентификатор сущности** и **URL-адрес утверждение потребителя доступа (ACS)**</span><span class="sxs-lookup"><span data-stu-id="da8a4-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="da8a4-160">На портале Azure в разделе **URL-адреса и домена обучения LinkedIn**, выполнять hello, выполнив действия, если требуется, чтобы tooconfigure единого входа в **инициированный IdP** режим</span><span class="sxs-lookup"><span data-stu-id="da8a4-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="da8a4-162">а.</span><span class="sxs-lookup"><span data-stu-id="da8a4-162">a.</span></span> <span data-ttu-id="da8a4-163">В hello **идентификатор** текстовом поле введите hello **идентификатор сущности** копируются LinkedIn портала</span><span class="sxs-lookup"><span data-stu-id="da8a4-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="da8a4-164">b.</span><span class="sxs-lookup"><span data-stu-id="da8a4-164">b.</span></span> <span data-ttu-id="da8a4-165">В hello **URL-адрес ответа** текстовом поле введите hello **утверждение потребителя доступа (ACS) URL-адрес** копируются LinkedIn портала</span><span class="sxs-lookup"><span data-stu-id="da8a4-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="da8a4-166">Если требуется, чтобы tooconfigure единого входа в **, инициируемая SP**, затем щелкните URL-адрес Advanced Показать параметр в разделе конфигурации hello и настройте hello URL-адрес входа с hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="da8a4-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="da8a4-168">Приложение обучения LinkedIn ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="da8a4-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="da8a4-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="da8a4-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="da8a4-170">значение по умолчанию Hello **идентификатор пользователя** — **user.userprincipalname** , но это toobe, сопоставленный с адресом электронной почты пользователя hello ожидает LinkedIn обучения.</span><span class="sxs-lookup"><span data-stu-id="da8a4-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="da8a4-171">Для этого можно использовать **user.mail** атрибут из списка hello, или используйте hello соответствующее значение атрибута на основе конфигурации в организации.</span><span class="sxs-lookup"><span data-stu-id="da8a4-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="da8a4-173">В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello.</span><span class="sxs-lookup"><span data-stu-id="da8a4-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="da8a4-174">Hello пользователь должен tooadd четыре утверждения с именем **электронной почты**, **отдел**, **firstname**, и **lastname** и hello значение — toobe сопоставлено с **user.mail**, **user.department**, **user.givenname**, и **user.surname** соответственно</span><span class="sxs-lookup"><span data-stu-id="da8a4-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="da8a4-175">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="da8a4-175">Attribute Name</span></span> | <span data-ttu-id="da8a4-176">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="da8a4-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="da8a4-177">email</span><span class="sxs-lookup"><span data-stu-id="da8a4-177">email</span></span>| <span data-ttu-id="da8a4-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="da8a4-178">user.mail</span></span> |    
    | <span data-ttu-id="da8a4-179">department</span><span class="sxs-lookup"><span data-stu-id="da8a4-179">department</span></span>| <span data-ttu-id="da8a4-180">user.department</span><span class="sxs-lookup"><span data-stu-id="da8a4-180">user.department</span></span> |
    | <span data-ttu-id="da8a4-181">firstname</span><span class="sxs-lookup"><span data-stu-id="da8a4-181">firstname</span></span>| <span data-ttu-id="da8a4-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="da8a4-182">user.givenname</span></span> |
    | <span data-ttu-id="da8a4-183">lastname</span><span class="sxs-lookup"><span data-stu-id="da8a4-183">lastname</span></span>| <span data-ttu-id="da8a4-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="da8a4-184">user.surname</span></span> |
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="da8a4-186">а.</span><span class="sxs-lookup"><span data-stu-id="da8a4-186">a.</span></span> <span data-ttu-id="da8a4-187">Нажмите кнопку **Добавление атрибута** tooopen hello атрибута, диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="da8a4-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="da8a4-190">b.</span><span class="sxs-lookup"><span data-stu-id="da8a4-190">b.</span></span> <span data-ttu-id="da8a4-191">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="da8a4-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="da8a4-192">c.</span><span class="sxs-lookup"><span data-stu-id="da8a4-192">c.</span></span> <span data-ttu-id="da8a4-193">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="da8a4-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="da8a4-194">d.</span><span class="sxs-lookup"><span data-stu-id="da8a4-194">d.</span></span> <span data-ttu-id="da8a4-195">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-195">Click **Ok**</span></span>

10. <span data-ttu-id="da8a4-196">Выполните следующие действия на hello hello **имя** атрибута -</span><span class="sxs-lookup"><span data-stu-id="da8a4-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="da8a4-197">а.</span><span class="sxs-lookup"><span data-stu-id="da8a4-197">a.</span></span> <span data-ttu-id="da8a4-198">Щелкните hello атрибут tooopen hello **изменение атрибута** окна.</span><span class="sxs-lookup"><span data-stu-id="da8a4-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="da8a4-200">b.</span><span class="sxs-lookup"><span data-stu-id="da8a4-200">b.</span></span> <span data-ttu-id="da8a4-201">Удалить значение URL-адрес hello из hello **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="da8a4-202">c.</span><span class="sxs-lookup"><span data-stu-id="da8a4-202">c.</span></span> <span data-ttu-id="da8a4-203">Нажмите кнопку **ОК** toosave приветствия.</span><span class="sxs-lookup"><span data-stu-id="da8a4-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="da8a4-204">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="da8a4-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="da8a4-206">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-206">Click **Save**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="da8a4-208">Go слишком**параметры администрирования LinkedIn** раздела.</span><span class="sxs-lookup"><span data-stu-id="da8a4-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="da8a4-209">Отправьте hello XML-файл, загруженный с портала Azure hello, щелкнув hello отправить файл в формат XML.</span><span class="sxs-lookup"><span data-stu-id="da8a4-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="da8a4-211">Нажмите кнопку **на** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="da8a4-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="da8a4-212">Изменение состояния единого входа с **не подключены** слишком**подключено**</span><span class="sxs-lookup"><span data-stu-id="da8a4-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da8a4-214">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="da8a4-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="da8a4-215">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="da8a4-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="da8a4-217">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="da8a4-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="da8a4-218">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="da8a4-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da8a4-220">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da8a4-222">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="da8a4-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da8a4-224">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="da8a4-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da8a4-226">а.</span><span class="sxs-lookup"><span data-stu-id="da8a4-226">a.</span></span> <span data-ttu-id="da8a4-227">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da8a4-228">b.</span><span class="sxs-lookup"><span data-stu-id="da8a4-228">b.</span></span> <span data-ttu-id="da8a4-229">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="da8a4-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da8a4-230">c.</span><span class="sxs-lookup"><span data-stu-id="da8a4-230">c.</span></span> <span data-ttu-id="da8a4-231">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="da8a4-232">d.</span><span class="sxs-lookup"><span data-stu-id="da8a4-232">d.</span></span> <span data-ttu-id="da8a4-233">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="da8a4-234">Создание тестового пользователя LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="da8a4-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="da8a4-235">Приложение Linked Learning поддерживает</span><span class="sxs-lookup"><span data-stu-id="da8a4-235">Linked Learning Application supports.</span></span> <span data-ttu-id="da8a4-236">Только время подготовки пользователей и после проверки подлинности пользователей автоматически создаются в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="da8a4-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="da8a4-237">На странице параметров администрирования hello на коммутаторе портала зеркало hello обучения LinkedIn hello **автоматически назначать лицензии** tooenable tooactive непосредственно в момент подготовки и это также назначить лицензию пользователя toohello.</span><span class="sxs-lookup"><span data-stu-id="da8a4-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="da8a4-239">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="da8a4-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="da8a4-240">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLinkedIn обучения.</span><span class="sxs-lookup"><span data-stu-id="da8a4-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="da8a4-242">**tooassign tooLinkedIn Britta Simon обучения, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="da8a4-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="da8a4-243">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="da8a4-245">В списке приложений hello выберите **обучения LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="da8a4-247">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="da8a4-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-249">Click **Add** button.</span></span> <span data-ttu-id="da8a4-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="da8a4-252">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="da8a4-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="da8a4-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da8a4-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="da8a4-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="da8a4-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="da8a4-255">Testing single sign-on</span></span>

<span data-ttu-id="da8a4-256">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="da8a4-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="da8a4-257">При выборе плитки обучения LinkedIn hello в hello панели доступа, вы должны получить страницу hello Azure входа и на после успешного входа, должно появиться в приложение LinkedIn обучения.</span><span class="sxs-lookup"><span data-stu-id="da8a4-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="da8a4-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="da8a4-258">Additional resources</span></span>

* [<span data-ttu-id="da8a4-259">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da8a4-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da8a4-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="da8a4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png