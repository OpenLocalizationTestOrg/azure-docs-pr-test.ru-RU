---
title: "Руководство по интеграции Azure Active Directory с ServiceChannel | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="d08ba-103">Руководство: интеграция Azure Active Directory с ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="d08ba-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="d08ba-104">В этом учебнике вы узнаете, как toointegrate ServiceChannel с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d08ba-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d08ba-105">Интеграция с Azure AD ServiceChannel предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d08ba-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d08ba-106">Можно управлять в Azure AD, имеющего доступ tooServiceChannel</span><span class="sxs-lookup"><span data-stu-id="d08ba-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="d08ba-107">Можно включить на пользователей tooautomatically get вошедшего tooServiceChannel (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="d08ba-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d08ba-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="d08ba-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d08ba-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d08ba-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d08ba-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d08ba-110">Prerequisites</span></span>

<span data-ttu-id="d08ba-111">tooconfigure интеграция Azure AD с ServiceChannel требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d08ba-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="d08ba-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d08ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d08ba-113">подписка ServiceChannel с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d08ba-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d08ba-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d08ba-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d08ba-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d08ba-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d08ba-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="d08ba-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d08ba-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d08ba-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d08ba-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d08ba-118">Scenario description</span></span>
<span data-ttu-id="d08ba-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d08ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d08ba-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d08ba-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d08ba-121">Добавление ServiceChannel из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d08ba-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="d08ba-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d08ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="d08ba-123">Добавление ServiceChannel из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d08ba-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="d08ba-124">tooconfigure hello интеграции ServiceChannel в Azure AD, вы должны tooadd ServiceChannel из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d08ba-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d08ba-125">**tooadd ServiceChannel из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d08ba-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d08ba-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d08ba-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d08ba-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d08ba-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d08ba-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="d08ba-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d08ba-133">Введите в поле поиска hello **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="d08ba-135">В панели результатов hello выберите **ServiceChannel**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d08ba-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d08ba-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d08ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d08ba-138">В этом разделе описана настройка и проверка единого входа Azure AD в ServiceChannel с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d08ba-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d08ba-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ServiceChannel является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d08ba-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="d08ba-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ServiceChannel должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d08ba-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="d08ba-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="d08ba-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="d08ba-142">tooconfigure и теста Azure AD единого входа с ServiceChannel, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d08ba-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d08ba-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d08ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d08ba-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d08ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d08ba-145">**[Создание тестового пользователя ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d08ba-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="d08ba-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d08ba-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d08ba-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d08ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d08ba-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d08ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d08ba-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="d08ba-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="d08ba-150">**tooconfigure Azure AD единого входа с ServiceChannel, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d08ba-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="d08ba-151">На портале управления Azure hello на hello **ServiceChannel** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d08ba-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d08ba-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="d08ba-155">На hello **URL-адреса и домена ServiceChannel** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d08ba-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="d08ba-157">а.</span><span class="sxs-lookup"><span data-stu-id="d08ba-157">a.</span></span> <span data-ttu-id="d08ba-158">В hello **идентификатор** текстовое поле, значение типа hello как:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="d08ba-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="d08ba-159">b.</span><span class="sxs-lookup"><span data-stu-id="d08ba-159">b.</span></span> <span data-ttu-id="d08ba-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="d08ba-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d08ba-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="d08ba-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="d08ba-162">У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d08ba-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d08ba-163">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d08ba-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="d08ba-164">Обратитесь к [ServiceChannel поддержки](https://servicechannel.zendesk.com/hc/en-us) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="d08ba-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="d08ba-165">Приложение ServiceChannel ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="d08ba-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="d08ba-166">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="d08ba-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="d08ba-167">**NameIdentifier (идентификатор пользователя)** hello только обязательные утверждение и значение по умолчанию hello — **user.userprincipalname** , но ServiceChannel ожидает этот toobe, сопоставленный с **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="d08ba-168">При планировании подготовки пользователей tooenable только в момент времени, то необходимо добавить hello после утверждения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d08ba-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="d08ba-169">**Роль** утверждения должен сопоставить слишком toobe**user.assignedroles** , содержащее роли hello hello.</span><span class="sxs-lookup"><span data-stu-id="d08ba-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="d08ba-170">Дополнительные инструкции по работе с утверждениями можно найти в руководстве по ServiceChannel [здесь](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example).</span><span class="sxs-lookup"><span data-stu-id="d08ba-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="d08ba-172">Нажмите кнопку [здесь](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow как tooconfigure **роли** в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d08ba-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="d08ba-173">В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello.</span><span class="sxs-lookup"><span data-stu-id="d08ba-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="d08ba-174">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="d08ba-174">Attribute Name</span></span> | <span data-ttu-id="d08ba-175">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="d08ba-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="d08ba-176">Роль</span><span class="sxs-lookup"><span data-stu-id="d08ba-176">Role</span></span>| <span data-ttu-id="d08ba-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="d08ba-177">user.assignedroles</span></span> |

    <span data-ttu-id="d08ba-178">а.</span><span class="sxs-lookup"><span data-stu-id="d08ba-178">a.</span></span> <span data-ttu-id="d08ba-179">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d08ba-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="d08ba-182">b.</span><span class="sxs-lookup"><span data-stu-id="d08ba-182">b.</span></span> <span data-ttu-id="d08ba-183">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="d08ba-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d08ba-184">c.</span><span class="sxs-lookup"><span data-stu-id="d08ba-184">c.</span></span> <span data-ttu-id="d08ba-185">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="d08ba-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d08ba-186">d.</span><span class="sxs-lookup"><span data-stu-id="d08ba-186">d.</span></span> <span data-ttu-id="d08ba-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="d08ba-188">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="d08ba-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="d08ba-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-190">Click **Save**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d08ba-192">На hello **конфигурации ServiceChannel** щелкните **Настройка ServiceChannel** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="d08ba-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d08ba-193">Обратите внимание, hello **идентификатор SAML Enitity** из hello **краткий справочник** раздела.</span><span class="sxs-lookup"><span data-stu-id="d08ba-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="d08ba-194">tooconfigure единого входа на **ServiceChannel** стороны, необходимо загрузить hello toosend **сертификата (Base64)** и **идентификатор сущности SAML** слишком[ Группа поддержки ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="d08ba-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="d08ba-195">Они будут устанавливается в порядке toohave hello правильно настроенной на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="d08ba-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d08ba-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d08ba-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="d08ba-197">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d08ba-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d08ba-199">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d08ba-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d08ba-200">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d08ba-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d08ba-202">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="d08ba-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d08ba-204">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d08ba-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d08ba-206">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d08ba-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d08ba-208">а.</span><span class="sxs-lookup"><span data-stu-id="d08ba-208">a.</span></span> <span data-ttu-id="d08ba-209">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d08ba-210">b.</span><span class="sxs-lookup"><span data-stu-id="d08ba-210">b.</span></span> <span data-ttu-id="d08ba-211">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d08ba-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d08ba-212">c.</span><span class="sxs-lookup"><span data-stu-id="d08ba-212">c.</span></span> <span data-ttu-id="d08ba-213">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d08ba-214">d.</span><span class="sxs-lookup"><span data-stu-id="d08ba-214">d.</span></span> <span data-ttu-id="d08ba-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="d08ba-216">Создание тестового пользователя ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="d08ba-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="d08ba-217">В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение.</span><span class="sxs-lookup"><span data-stu-id="d08ba-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="d08ba-218">Для настройки полной подготовки пользователей обратитесь в [службу поддержки ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="d08ba-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d08ba-219">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d08ba-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d08ba-220">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooServiceChannel доступа.</span><span class="sxs-lookup"><span data-stu-id="d08ba-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d08ba-222">**tooassign tooServiceChannel Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d08ba-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="d08ba-223">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d08ba-225">В списке приложений hello выберите **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="d08ba-227">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d08ba-229">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-229">Click **Add** button.</span></span> <span data-ttu-id="d08ba-230">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d08ba-232">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d08ba-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d08ba-233">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d08ba-234">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d08ba-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d08ba-235">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d08ba-235">Testing single sign-on</span></span>

<span data-ttu-id="d08ba-236">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="d08ba-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d08ba-237">При нажатии кнопки hello ServiceChannel плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="d08ba-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d08ba-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d08ba-238">Additional resources</span></span>

* [<span data-ttu-id="d08ba-239">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d08ba-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d08ba-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d08ba-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png