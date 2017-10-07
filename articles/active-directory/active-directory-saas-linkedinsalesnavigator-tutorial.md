---
title: "Учебник. Интеграция Azure Active Directory с LinkedInSalesNavigator | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="b18f3-103">Руководство по интеграции Azure Active Directory с LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="b18f3-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="b18f3-104">В этом учебнике вы узнаете, как toointegrate навигатор продаж LinkedIn с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b18f3-104">In this tutorial, you learn how toointegrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b18f3-105">Интеграция навигатор продаж LinkedIn с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b18f3-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b18f3-106">Можно управлять в Azure AD, имеющего доступ tooLinkedIn навигатор продаж</span><span class="sxs-lookup"><span data-stu-id="b18f3-106">You can control in Azure AD who has access tooLinkedIn Sales Navigator</span></span>
- <span data-ttu-id="b18f3-107">Ваш пользователей tooautomatically get вошедшего tooLinkedIn навигатор продаж (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b18f3-107">You can enable your users tooautomatically get signed-on tooLinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b18f3-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b18f3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b18f3-109">Tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, воспользуйтесь следующей ссылкой [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b18f3-109">If you want tooknow more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b18f3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b18f3-110">Prerequisites</span></span>

<span data-ttu-id="b18f3-111">tooconfigure интеграция Azure AD с навигатор продаж LinkedIn требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b18f3-111">tooconfigure Azure AD integration with LinkedIn Sales Navigator, you need hello following items:</span></span>

- <span data-ttu-id="b18f3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b18f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b18f3-113">подписка LinkedIn Sales Navigator с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b18f3-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b18f3-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b18f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b18f3-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b18f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b18f3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b18f3-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b18f3-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b18f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b18f3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b18f3-118">Scenario description</span></span>
<span data-ttu-id="b18f3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b18f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b18f3-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b18f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b18f3-121">Добавление навигатор LinkedIn продаж из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b18f3-121">Adding LinkedIn Sales Navigator from hello gallery</span></span>
2. <span data-ttu-id="b18f3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b18f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a><span data-ttu-id="b18f3-123">Добавление навигатор LinkedIn продаж из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b18f3-123">Adding LinkedIn Sales Navigator from hello gallery</span></span>
<span data-ttu-id="b18f3-124">tooconfigure hello интеграции навигатор LinkedIn продаж в Azure AD, вы должны tooadd навигатор LinkedIn продаж из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b18f3-124">tooconfigure hello integration of LinkedIn Sales Navigator into Azure AD, you need tooadd LinkedIn Sales Navigator from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b18f3-125">**tooadd LinkedIn навигатор продаж из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b18f3-125">**tooadd LinkedIn Sales Navigator from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b18f3-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b18f3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b18f3-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b18f3-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b18f3-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b18f3-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b18f3-133">Введите в поле поиска hello **навигатор продаж LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-133">In hello search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="b18f3-135">В панели результатов hello, выберите **навигатор продаж LinkedIn**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b18f3-135">In hello results panel, select **LinkedIn Sales Navigator**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b18f3-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b18f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b18f3-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение LinkedIn Sales Navigator с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b18f3-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b18f3-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в навигаторе LinkedIn продажи является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b18f3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Sales Navigator is tooa user in Azure AD.</span></span> <span data-ttu-id="b18f3-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в навигаторе продаж LinkedIn должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b18f3-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Sales Navigator needs toobe established.</span></span>

<span data-ttu-id="b18f3-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в навигаторе LinkedIn продаж.</span><span class="sxs-lookup"><span data-stu-id="b18f3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="b18f3-142">tooconfigure и теста Azure AD единого входа с навигатор LinkedIn продаж, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="b18f3-142">tooconfigure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b18f3-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b18f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b18f3-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b18f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b18f3-145">**[Создание тестового пользователя навигатор продаж LinkedIn](#creating-a-linkedin-sales-navigator-test-user)**  -toohave аналог Саймон Britta в навигаторе LinkedIn продаж, являющийся представлением пользовательского hello связанного toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b18f3-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="b18f3-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b18f3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b18f3-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b18f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b18f3-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b18f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b18f3-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении навигатор LinkedIn продаж.</span><span class="sxs-lookup"><span data-stu-id="b18f3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="b18f3-150">**tooconfigure Azure AD единого входа с навигатор LinkedIn продаж, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b18f3-150">**tooconfigure Azure AD single sign-on with LinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="b18f3-151">В hello в hello портала Azure **навигатор продаж LinkedIn** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-151">In hello Azure portal, on hello **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b18f3-153">На hello **единого входа** диалоговое окно, в **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b18f3-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="b18f3-155">В другом окне браузера, tooyour входа **навигатор продаж LinkedIn** веб-сайта от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="b18f3-155">In a different web browser window, sign-on tooyour **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="b18f3-156">В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры).</span><span class="sxs-lookup"><span data-stu-id="b18f3-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="b18f3-157">Кроме того, установите **навигатор Sales** hello в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="b18f3-157">Also, select **Sales Navigator** from hello dropdown list.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="b18f3-159">Нажмите кнопку **или щелкните здесь tooload и скопируйте отдельные поля из формы hello** и скопируйте **идентификатор сущности** и **утверждение потребителя доступа (ACS) URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="b18f3-161">На портале Azure в разделе **URL-адреса и домена навигатор LinkedIn Sales** выполните hello, выполните действия, при желании tooconfigure приложения hello в **поставщика Удостоверений** инициировал режим.</span><span class="sxs-lookup"><span data-stu-id="b18f3-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="b18f3-163">а.</span><span class="sxs-lookup"><span data-stu-id="b18f3-163">a.</span></span> <span data-ttu-id="b18f3-164">В hello **идентификатор** текстовом поле введите hello **идентификатор сущности** копируются LinkedIn портала</span><span class="sxs-lookup"><span data-stu-id="b18f3-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="b18f3-165">b.</span><span class="sxs-lookup"><span data-stu-id="b18f3-165">b.</span></span> <span data-ttu-id="b18f3-166">В hello **URL-адрес ответа** текстовом поле введите hello **утверждение потребителя доступа (ACS) URL-адрес** копируются LinkedIn портала</span><span class="sxs-lookup"><span data-stu-id="b18f3-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="b18f3-167">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим.</span><span class="sxs-lookup"><span data-stu-id="b18f3-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="b18f3-169">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="b18f3-169">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="b18f3-170">Ваш **навигатор продаж LinkedIn** приложение ожидает утверждения SAML hello в определенном формате, требующий конфигурация атрибутов токена SAML tooyour сопоставления tooadd настраиваемого атрибута.</span><span class="sxs-lookup"><span data-stu-id="b18f3-170">Your **LinkedIn Sales Navigator** application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="b18f3-171">Следующий снимок экрана приветствия показан пример.</span><span class="sxs-lookup"><span data-stu-id="b18f3-171">hello following screenshot shows an example.</span></span> <span data-ttu-id="b18f3-172">значение по умолчанию Hello **идентификатор пользователя** — **user.userprincipalname** , но навигатор продаж LinkedIn ожидает toobe, сопоставленный с адресом электронной почты пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b18f3-172">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it toobe mapped with hello user's email address.</span></span> <span data-ttu-id="b18f3-173">Можно использовать **user.mail** атрибут из списка hello, или используйте hello соответствующее значение атрибута на основе конфигурации в организации.</span><span class="sxs-lookup"><span data-stu-id="b18f3-173">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="b18f3-175">В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello.</span><span class="sxs-lookup"><span data-stu-id="b18f3-175">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="b18f3-176">Hello пользователь должен tooadd четыре утверждения с именем **электронной почты**, **отдел**, **firstname**, и **lastname** и hello значение — toobe сопоставлено с **user.mail**, **user.department**, **user.givenname**, и **user.surname** соответственно</span><span class="sxs-lookup"><span data-stu-id="b18f3-176">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="b18f3-177">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="b18f3-177">Attribute Name</span></span> | <span data-ttu-id="b18f3-178">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="b18f3-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="b18f3-179">email</span><span class="sxs-lookup"><span data-stu-id="b18f3-179">email</span></span>| <span data-ttu-id="b18f3-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="b18f3-180">user.mail</span></span> |
    | <span data-ttu-id="b18f3-181">department</span><span class="sxs-lookup"><span data-stu-id="b18f3-181">department</span></span>| <span data-ttu-id="b18f3-182">user.department</span><span class="sxs-lookup"><span data-stu-id="b18f3-182">user.department</span></span> |
    | <span data-ttu-id="b18f3-183">firstname</span><span class="sxs-lookup"><span data-stu-id="b18f3-183">firstname</span></span>| <span data-ttu-id="b18f3-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b18f3-184">user.givenname</span></span> |
    | <span data-ttu-id="b18f3-185">lastname</span><span class="sxs-lookup"><span data-stu-id="b18f3-185">lastname</span></span>| <span data-ttu-id="b18f3-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="b18f3-186">user.surname</span></span> |
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="b18f3-188">а.</span><span class="sxs-lookup"><span data-stu-id="b18f3-188">a.</span></span> <span data-ttu-id="b18f3-189">Щелкните **Добавление атрибута** tooopen hello атрибута, диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b18f3-189">Click on **Add Attribute** tooopen hello attribute dialog.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="b18f3-192">b.</span><span class="sxs-lookup"><span data-stu-id="b18f3-192">b.</span></span> <span data-ttu-id="b18f3-193">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b18f3-193">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b18f3-194">c.</span><span class="sxs-lookup"><span data-stu-id="b18f3-194">c.</span></span> <span data-ttu-id="b18f3-195">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b18f3-195">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b18f3-196">d.</span><span class="sxs-lookup"><span data-stu-id="b18f3-196">d.</span></span> <span data-ttu-id="b18f3-197">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-197">Click **Ok**</span></span>

10. <span data-ttu-id="b18f3-198">Выполните следующие действия на hello hello **имя** атрибута -</span><span class="sxs-lookup"><span data-stu-id="b18f3-198">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="b18f3-199">а.</span><span class="sxs-lookup"><span data-stu-id="b18f3-199">a.</span></span> <span data-ttu-id="b18f3-200">Щелкните hello атрибут tooopen hello **изменение атрибута** окна.</span><span class="sxs-lookup"><span data-stu-id="b18f3-200">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="b18f3-202">b.</span><span class="sxs-lookup"><span data-stu-id="b18f3-202">b.</span></span> <span data-ttu-id="b18f3-203">Удалить значение URL-адрес hello из hello **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-203">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="b18f3-204">c.</span><span class="sxs-lookup"><span data-stu-id="b18f3-204">c.</span></span> <span data-ttu-id="b18f3-205">Нажмите кнопку **ОК** toosave приветствия.</span><span class="sxs-lookup"><span data-stu-id="b18f3-205">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="b18f3-206">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b18f3-206">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="b18f3-208">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b18f3-208">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="b18f3-210">Go слишком**параметры администрирования LinkedIn** раздела.</span><span class="sxs-lookup"><span data-stu-id="b18f3-210">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="b18f3-211">Нажмите кнопку **отправить XML-файл** tooupload hello метаданных XML-файл, загруженный с портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b18f3-211">Click **Upload XML file** tooupload hello Metadata XML file that you have downloaded from hello Azure portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="b18f3-213">Нажмите кнопку **на** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b18f3-213">Click **On** tooenable SSO.</span></span> <span data-ttu-id="b18f3-214">Изменение состояния единого входа с **не подключены** слишком**подключено**</span><span class="sxs-lookup"><span data-stu-id="b18f3-214">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="b18f3-216">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b18f3-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b18f3-217">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b18f3-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b18f3-218">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b18f3-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b18f3-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b18f3-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="b18f3-220">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b18f3-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b18f3-222">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b18f3-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b18f3-223">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b18f3-223">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b18f3-225">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-225">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b18f3-227">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b18f3-227">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b18f3-229">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b18f3-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b18f3-231">а.</span><span class="sxs-lookup"><span data-stu-id="b18f3-231">a.</span></span> <span data-ttu-id="b18f3-232">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b18f3-233">b.</span><span class="sxs-lookup"><span data-stu-id="b18f3-233">b.</span></span> <span data-ttu-id="b18f3-234">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b18f3-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b18f3-235">c.</span><span class="sxs-lookup"><span data-stu-id="b18f3-235">c.</span></span> <span data-ttu-id="b18f3-236">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b18f3-237">d.</span><span class="sxs-lookup"><span data-stu-id="b18f3-237">d.</span></span> <span data-ttu-id="b18f3-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="b18f3-239">Создание тестового пользователя LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="b18f3-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="b18f3-240">Связанное приложение навигатор продаж поддерживает только в подготовки пользователей Time (JIT) и после проверки подлинности пользователей автоматически создаются в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="b18f3-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="b18f3-241">Активировать **автоматически назначать лицензии** tooassign toohello лицензии пользователя.</span><span class="sxs-lookup"><span data-stu-id="b18f3-241">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b18f3-243">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b18f3-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b18f3-244">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLinkedIn навигатор продаж.</span><span class="sxs-lookup"><span data-stu-id="b18f3-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Sales Navigator.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b18f3-246">**tooassign tooLinkedIn Britta Simon навигатор продаж выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b18f3-246">**tooassign Britta Simon tooLinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="b18f3-247">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b18f3-249">В списке приложений hello выберите **навигатор продаж LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-249">In hello applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="b18f3-251">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b18f3-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-253">Click **Add** button.</span></span> <span data-ttu-id="b18f3-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b18f3-256">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b18f3-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b18f3-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b18f3-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b18f3-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b18f3-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b18f3-259">Testing single sign-on</span></span>

<span data-ttu-id="b18f3-260">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b18f3-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b18f3-261">Если щелкнуть плитку навигатор продаж LinkedIn hello в hello панели доступа, должно быть перенаправленный tooOrganizational страницы, при наличии tooprovide личные сведения учетной записи LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b18f3-261">When you click hello LinkedIn Sales Navigator tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="b18f3-262">В результате ваша личная учетная запись связывается с вашей рабочей учетной записью LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b18f3-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="b18f3-263">Дополнительные сведения о панели доступа hello см. в разделе [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b18f3-263">For more information about hello Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b18f3-264">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b18f3-264">Additional resources</span></span>

* [<span data-ttu-id="b18f3-265">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b18f3-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b18f3-266">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b18f3-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

