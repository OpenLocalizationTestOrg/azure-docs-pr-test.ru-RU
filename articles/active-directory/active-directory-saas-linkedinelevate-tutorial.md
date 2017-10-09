---
title: "Руководство по интеграции Azure Active Directory с LinkedIn Elevate | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и может повышать уровень LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="83745-103">Руководство по интеграции Azure Active Directory с LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="83745-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="83745-104">В этом учебнике вы узнаете, как повысить уровень LinkedIn toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83745-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83745-105">Интеграция LinkedIn повышения прав с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="83745-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="83745-106">Можно управлять в Azure AD, имеющего доступ tooLinkedIn повышение</span><span class="sxs-lookup"><span data-stu-id="83745-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="83745-107">Можно включить на пользователей tooautomatically get вошедшего tooLinkedIn повышение (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="83745-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83745-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="83745-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="83745-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83745-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83745-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83745-110">Prerequisites</span></span>

<span data-ttu-id="83745-111">tooconfigure интеграция Azure AD с повышение LinkedIn требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="83745-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="83745-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="83745-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83745-113">подписка LinkedIn Elevate с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="83745-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83745-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="83745-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83745-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="83745-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83745-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="83745-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="83745-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83745-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83745-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="83745-118">Scenario description</span></span>
<span data-ttu-id="83745-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="83745-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83745-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="83745-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83745-121">Добавление LinkedIn повысить уровень из галереи hello</span><span class="sxs-lookup"><span data-stu-id="83745-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="83745-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83745-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="83745-123">Добавление LinkedIn повысить уровень из галереи hello</span><span class="sxs-lookup"><span data-stu-id="83745-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="83745-124">tooconfigure hello интеграции LinkedIn повышение в Azure AD, вы должны tooadd LinkedIn повысить уровень из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="83745-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83745-125">**tooadd LinkedIn повысить уровень из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="83745-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="83745-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="83745-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83745-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="83745-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="83745-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="83745-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="83745-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="83745-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="83745-133">Введите в поле поиска hello **повысить LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="83745-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="83745-134">На панели результатов щелкните **повысить LinkedIn** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="83745-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83745-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83745-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83745-137">В этом разделе описана настройка и проверка единого входа Azure AD в приложение LinkedIn Elevate с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83745-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83745-138">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в повышение LinkedIn является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83745-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="83745-139">Другими словами связи между пользователя Azure AD и связанных пользователей hello в повышение LinkedIn должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="83745-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="83745-140">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в повышение LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="83745-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="83745-141">tooconfigure и теста Azure AD единого входа с LinkedIn повышать права, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="83745-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="83745-142">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="83745-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="83745-143">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="83745-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83745-144">**[Создание тестового пользователя повышение LinkedIn](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="83745-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="83745-145">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="83745-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83745-146">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="83745-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83745-147">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83745-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83745-148">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении LinkedIn повышения прав.</span><span class="sxs-lookup"><span data-stu-id="83745-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="83745-149">**tooconfigure Azure AD единого входа с LinkedIn повышения прав, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="83745-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="83745-150">На портале управления Azure hello на hello **LinkedIn повышение** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="83745-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="83745-152">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="83745-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="83745-154">В другом окне браузера, клиент LinkedIn повышение tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="83745-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="83745-155">В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры).</span><span class="sxs-lookup"><span data-stu-id="83745-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="83745-156">Кроме того, установите **повышение - повышение теста AAD** hello в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="83745-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="83745-158">Щелкните **или щелкните здесь tooload и скопируйте отдельные поля из формы hello** и скопируйте **идентификатор сущности** и **URL-адрес утверждение потребителя доступа (ACS)**</span><span class="sxs-lookup"><span data-stu-id="83745-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="83745-160">На портале Azure в разделе **URL-адреса и домена повышение LinkedIn**, выполнять hello, выполнив действия, если требуется, чтобы tooconfigure единого входа в **инициированный IdP** режим</span><span class="sxs-lookup"><span data-stu-id="83745-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="83745-162">а.</span><span class="sxs-lookup"><span data-stu-id="83745-162">a.</span></span> <span data-ttu-id="83745-163">В hello **идентификатор** текстовом поле введите hello **идентификатор сущности** копируются LinkedIn портала</span><span class="sxs-lookup"><span data-stu-id="83745-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="83745-164">b.</span><span class="sxs-lookup"><span data-stu-id="83745-164">b.</span></span> <span data-ttu-id="83745-165">В hello **URL-адрес ответа** текстовом поле введите hello **утверждение потребителя доступа (ACS) URL-адрес** копируются LinkedIn портала</span><span class="sxs-lookup"><span data-stu-id="83745-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="83745-166">Если требуется, чтобы tooconfigure единого входа в **, инициируемая SP**, затем щелкните URL-адрес Advanced Показать параметр в разделе конфигурации hello и настройка входа hello URL-адрес с hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="83745-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="83745-168">Приложение LinkedIn повышение ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="83745-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="83745-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="83745-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="83745-170">значение по умолчанию Hello **идентификатор пользователя** — **user.userprincipalname** , но повышение LinkedIn ожидает этот toobe, сопоставленный с адресом электронной почты пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="83745-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="83745-171">Для этого можно использовать **user.mail** атрибут из списка hello, или используйте hello соответствующее значение атрибута на основе конфигурации в организации.</span><span class="sxs-lookup"><span data-stu-id="83745-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="83745-173">В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello.</span><span class="sxs-lookup"><span data-stu-id="83745-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="83745-174">Требуется tooadd с именем другого утверждения **отдел** и значение hello должен сопоставить слишком toobe**user.department**.</span><span class="sxs-lookup"><span data-stu-id="83745-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="83745-175">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="83745-175">Attribute Name</span></span> | <span data-ttu-id="83745-176">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="83745-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="83745-177">department</span><span class="sxs-lookup"><span data-stu-id="83745-177">department</span></span>| <span data-ttu-id="83745-178">user.department</span><span class="sxs-lookup"><span data-stu-id="83745-178">user.department</span></span> |

      ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="83745-180">а.</span><span class="sxs-lookup"><span data-stu-id="83745-180">a.</span></span> <span data-ttu-id="83745-181">Щелкните на странице добавить атрибут tooopen hello атрибут сведения о добавить атрибута отдела hello, как показано ниже-</span><span class="sxs-lookup"><span data-stu-id="83745-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="83745-183">b.</span><span class="sxs-lookup"><span data-stu-id="83745-183">b.</span></span> <span data-ttu-id="83745-184">Щелкните **ОК** toosave hello атрибута.</span><span class="sxs-lookup"><span data-stu-id="83745-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="83745-185">c.</span><span class="sxs-lookup"><span data-stu-id="83745-185">c.</span></span> <span data-ttu-id="83745-186">Изменение имени hello hello атрибута **emailaddress** слишком**электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="83745-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="83745-187">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="83745-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="83745-189">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="83745-189">Click **Save**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="83745-191">Go слишком**параметры администрирования LinkedIn** раздела.</span><span class="sxs-lookup"><span data-stu-id="83745-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="83745-192">Отправьте hello XML-файл, только что загруженном из портала Azure hello, щелкнув hello параметр Отправить XML-файл.</span><span class="sxs-lookup"><span data-stu-id="83745-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="83745-194">Нажмите кнопку **на** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="83745-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="83745-195">SSO состояние изменится с **не подключены** слишком**подключено**</span><span class="sxs-lookup"><span data-stu-id="83745-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83745-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="83745-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="83745-198">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="83745-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="83745-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="83745-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="83745-201">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="83745-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83745-203">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="83745-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83745-205">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="83745-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83745-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="83745-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83745-209">а.</span><span class="sxs-lookup"><span data-stu-id="83745-209">a.</span></span> <span data-ttu-id="83745-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83745-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83745-211">b.</span><span class="sxs-lookup"><span data-stu-id="83745-211">b.</span></span> <span data-ttu-id="83745-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="83745-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83745-213">c.</span><span class="sxs-lookup"><span data-stu-id="83745-213">c.</span></span> <span data-ttu-id="83745-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="83745-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="83745-215">d.</span><span class="sxs-lookup"><span data-stu-id="83745-215">d.</span></span> <span data-ttu-id="83745-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="83745-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="83745-217">Создание тестового пользователя LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="83745-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="83745-218">Связанное приложение повышение поддерживает только в подготовки пользователей время и после проверки подлинности пользователей в приложении hello автоматически создаются.</span><span class="sxs-lookup"><span data-stu-id="83745-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="83745-219">На странице параметров администрирования hello на коммутаторе портала зеркало hello повышение LinkedIn hello **автоматически назначать лицензии** tooenable tooactive непосредственно в момент подготовки и это также назначить лицензию пользователя toohello.</span><span class="sxs-lookup"><span data-stu-id="83745-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="83745-221">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="83745-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="83745-222">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooLinkedIn повышение.</span><span class="sxs-lookup"><span data-stu-id="83745-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="83745-224">**tooassign tooLinkedIn Britta Simon повышение, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="83745-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="83745-225">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="83745-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="83745-227">В списке приложений hello выберите **повысить LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="83745-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="83745-229">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="83745-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="83745-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83745-231">Click **Add** button.</span></span> <span data-ttu-id="83745-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="83745-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="83745-234">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="83745-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="83745-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="83745-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83745-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="83745-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83745-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="83745-237">Testing single sign-on</span></span>

<span data-ttu-id="83745-238">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="83745-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="83745-239">При нажатии кнопки hello повышение LinkedIn плитки в панели доступа hello, вы должны получить страницу hello Azure входа и на после успешного входа, должно появиться в приложение LinkedIn повышения прав.</span><span class="sxs-lookup"><span data-stu-id="83745-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83745-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="83745-240">Additional resources</span></span>

* [<span data-ttu-id="83745-241">Руководство по настройке LinkedIn Elevate для автоматической подготовки пользователей с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83745-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="83745-242">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83745-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83745-243">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83745-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
