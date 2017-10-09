---
title: "Руководство по интеграции Azure Active Directory с myPolicies | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="8fd6f-103">Руководство по интеграции Azure Active Directory с myPolicies</span><span class="sxs-lookup"><span data-stu-id="8fd6f-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="8fd6f-104">В этом учебнике вы узнаете, как myPolicies toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8fd6f-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8fd6f-105">Интеграция с Azure AD myPolicies предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8fd6f-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8fd6f-106">Можно управлять в Azure AD, имеющего доступ toomyPolicies</span><span class="sxs-lookup"><span data-stu-id="8fd6f-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="8fd6f-107">Можно включить на пользователей tooautomatically get вошедшего toomyPolicies (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fd6f-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8fd6f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8fd6f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8fd6f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fd6f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8fd6f-110">Prerequisites</span></span>

<span data-ttu-id="8fd6f-111">tooconfigure интеграция Azure AD с myPolicies требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8fd6f-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="8fd6f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8fd6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8fd6f-113">подписка myPolicies с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8fd6f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8fd6f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8fd6f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8fd6f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8fd6f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8fd6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8fd6f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8fd6f-118">Scenario description</span></span>
<span data-ttu-id="8fd6f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8fd6f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8fd6f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8fd6f-121">Добавление myPolicies из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8fd6f-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="8fd6f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fd6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="8fd6f-123">Добавление myPolicies из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8fd6f-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="8fd6f-124">tooconfigure hello интеграции myPolicies в Azure AD, вы должны myPolicies tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8fd6f-125">**myPolicies tooadd из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8fd6f-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fd6f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8fd6f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8fd6f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8fd6f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8fd6f-133">Введите в поле поиска hello **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-133">In hello search box, type **myPolicies**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="8fd6f-135">В панели результатов hello выберите **myPolicies**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8fd6f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fd6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8fd6f-138">В этом разделе описана настройка и проверка единого входа Azure AD в myPolicies с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8fd6f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в myPolicies является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="8fd6f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в myPolicies должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="8fd6f-141">В myPolicies, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8fd6f-142">tooconfigure и теста Azure AD единого входа с myPolicies, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8fd6f-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8fd6f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8fd6f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8fd6f-145">**[Создание тестового пользователя myPolicies](#creating-a-mypolicies-test-user)**  -toohave аналог Саймон Britta в myPolicies, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8fd6f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8fd6f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8fd6f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fd6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8fd6f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении myPolicies.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="8fd6f-150">**tooconfigure Azure AD единого входа с myPolicies, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8fd6f-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fd6f-151">В hello в hello портала Azure **myPolicies** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8fd6f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="8fd6f-155">На hello **myPolicies URL-адреса и домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8fd6f-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="8fd6f-157">а.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-157">a.</span></span> <span data-ttu-id="8fd6f-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="8fd6f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="8fd6f-159">b.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-159">b.</span></span> <span data-ttu-id="8fd6f-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="8fd6f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8fd6f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-161">These values are not real.</span></span> <span data-ttu-id="8fd6f-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8fd6f-163">Обратитесь к [myPolicies поддержки](mailto:support@mypolicies.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="8fd6f-164">приложение Hello myPolicies ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="8fd6f-165">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="8fd6f-166">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8fd6f-167">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-167">hello following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="8fd6f-169">Нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** флажок в hello **атрибуты пользователя** статьи tooexpand hello атрибуты.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="8fd6f-170">Выполните следующие действия на каждом из hello отображаются атрибуты - hello</span><span class="sxs-lookup"><span data-stu-id="8fd6f-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="8fd6f-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="8fd6f-171">Attribute Name</span></span> | <span data-ttu-id="8fd6f-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="8fd6f-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="8fd6f-173">givenname</span><span class="sxs-lookup"><span data-stu-id="8fd6f-173">givenname</span></span> | <span data-ttu-id="8fd6f-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8fd6f-174">user.givenname</span></span> |
    | <span data-ttu-id="8fd6f-175">surname</span><span class="sxs-lookup"><span data-stu-id="8fd6f-175">surname</span></span> | <span data-ttu-id="8fd6f-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="8fd6f-176">user.surname</span></span> |
    | <span data-ttu-id="8fd6f-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="8fd6f-177">emailaddress</span></span> | <span data-ttu-id="8fd6f-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="8fd6f-178">user.mail</span></span> |
    | <span data-ttu-id="8fd6f-179">name</span><span class="sxs-lookup"><span data-stu-id="8fd6f-179">name</span></span> | <span data-ttu-id="8fd6f-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8fd6f-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="8fd6f-181">а.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-181">a.</span></span> <span data-ttu-id="8fd6f-182">Щелкните hello атрибут tooopen hello **изменение атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8fd6f-184">b.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-184">b.</span></span> <span data-ttu-id="8fd6f-185">Удалить значение URL-адрес hello из hello **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="8fd6f-186">c.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-186">c.</span></span> <span data-ttu-id="8fd6f-187">Нажмите кнопку **ОК** toosave приветствия.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="8fd6f-188">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="8fd6f-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8fd6f-190">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8fd6f-192">На hello **myPolicies конфигурации** щелкните **Настройка myPolicies** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8fd6f-193">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="8fd6f-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="8fd6f-195">tooconfigure единого входа на **myPolicies** стороны, необходимо загрузить hello toosend **Certificate(Base64)** и **SAML единого входа URL-адрес службы** слишком[myPolicies поддержки](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="8fd6f-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="8fd6f-196">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8fd6f-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8fd6f-197">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8fd6f-198">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8fd6f-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8fd6f-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fd6f-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="8fd6f-200">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8fd6f-202">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8fd6f-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fd6f-203">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8fd6f-205">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8fd6f-207">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8fd6f-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8fd6f-209">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8fd6f-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8fd6f-211">а.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-211">a.</span></span> <span data-ttu-id="8fd6f-212">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8fd6f-213">b.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-213">b.</span></span> <span data-ttu-id="8fd6f-214">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8fd6f-215">c.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-215">c.</span></span> <span data-ttu-id="8fd6f-216">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8fd6f-217">d.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-217">d.</span></span> <span data-ttu-id="8fd6f-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="8fd6f-219">Создание тестового пользователя myPolicies</span><span class="sxs-lookup"><span data-stu-id="8fd6f-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="8fd6f-220">В этом разделе описано, как создать пользователя Britta Simon в myPolicies.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="8fd6f-221">Работать с [myPolicies поддержки](mailto:support@mypolicies.com) для добавления пользователей hello в платформе myPolicies hello.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="8fd6f-222">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8fd6f-223">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8fd6f-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8fd6f-224">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления toomyPolicies доступа.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8fd6f-226">**tooassign toomyPolicies Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8fd6f-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fd6f-227">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8fd6f-229">В списке приложений hello выберите **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-229">In hello applications list, select **myPolicies**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="8fd6f-231">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8fd6f-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-233">Click **Add** button.</span></span> <span data-ttu-id="8fd6f-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8fd6f-236">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8fd6f-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8fd6f-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8fd6f-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8fd6f-239">Testing single sign-on</span></span>

<span data-ttu-id="8fd6f-240">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8fd6f-241">При нажатии кнопки myPolicies плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour myPolicies приложения.</span><span class="sxs-lookup"><span data-stu-id="8fd6f-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="8fd6f-242">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8fd6f-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8fd6f-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8fd6f-243">Additional resources</span></span>

* [<span data-ttu-id="8fd6f-244">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fd6f-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8fd6f-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8fd6f-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

