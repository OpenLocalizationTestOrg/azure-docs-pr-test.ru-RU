---
title: "Руководство по интеграции Azure Active Directory с Blackboard Learn | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Blackboard сведения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="c4955-103">Учебник. Интеграция Azure Active Directory с Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="c4955-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="c4955-104">В этом учебнике вы узнаете, как toointegrate Blackboard сведения с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4955-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4955-105">Интеграция с Azure AD узнать Blackboard предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c4955-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4955-106">Можно управлять в Azure AD, имеющего доступ tooBlackboard Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="c4955-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="c4955-107">Можно включить на пользователей tooautomatically get вошедшего tooBlackboard Дополнительные сведения (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4955-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4955-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c4955-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c4955-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4955-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4955-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c4955-110">Prerequisites</span></span>

<span data-ttu-id="c4955-111">tooconfigure интеграция Azure AD с Blackboard сведения, необходимые hello следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="c4955-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="c4955-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c4955-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4955-113">подписка Blackboard Learn — Shibboleth с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c4955-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4955-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c4955-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4955-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c4955-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4955-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c4955-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4955-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4955-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4955-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c4955-118">Scenario description</span></span>
<span data-ttu-id="c4955-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c4955-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4955-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c4955-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4955-121">Добавление Blackboard узнать из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c4955-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="c4955-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4955-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="c4955-123">Добавление Blackboard узнать из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c4955-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="c4955-124">tooconfigure hello интеграции узнать Blackboard в Azure AD, вы должны tooadd Blackboard узнать из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c4955-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4955-125">**tooadd Blackboard узнать из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4955-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4955-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c4955-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4955-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c4955-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4955-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c4955-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c4955-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c4955-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c4955-133">Введите в поле поиска hello **Blackboard узнать**.</span><span class="sxs-lookup"><span data-stu-id="c4955-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="c4955-135">В панели результатов hello выберите **узнать Blackboard**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c4955-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4955-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4955-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4955-138">В этом разделе описана настройка и проверка единого входа Azure AD в Blackboard Learn с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4955-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c4955-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Blackboard узнать является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4955-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="c4955-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Blackboard узнать должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c4955-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="c4955-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Blackboard Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="c4955-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="c4955-142">tooconfigure и теста Azure AD единого входа с Blackboard сведения, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="c4955-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4955-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c4955-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4955-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c4955-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4955-145">**[Создание тестового пользователя узнать Blackboard](#creating-a-blackboard-learn-test-user)**  -toohave аналог Саймон Britta в Blackboard узнать, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c4955-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4955-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c4955-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4955-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c4955-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4955-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4955-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4955-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Blackboard сведения.</span><span class="sxs-lookup"><span data-stu-id="c4955-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="c4955-150">**tooconfigure Azure AD единого входа с Blackboard узнать, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4955-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4955-151">В hello в hello портала Azure **узнать Blackboard** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c4955-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c4955-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c4955-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="c4955-155">На hello **URL-адреса и домена узнать Blackboard** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c4955-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="c4955-157">а.</span><span class="sxs-lookup"><span data-stu-id="c4955-157">a.</span></span> <span data-ttu-id="c4955-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="c4955-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="c4955-159">b.</span><span class="sxs-lookup"><span data-stu-id="c4955-159">b.</span></span> <span data-ttu-id="c4955-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="c4955-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="c4955-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c4955-161">These values are not real.</span></span> <span data-ttu-id="c4955-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c4955-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c4955-163">Обратитесь к [группа поддержки клиента узнать Blackboard](https://www.blackboard.com/support/index.aspx) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="c4955-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="c4955-164">Blackboard подробнее приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="c4955-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c4955-165">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c4955-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="c4955-166">Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** раздел на странице интеграции приложений.</span><span class="sxs-lookup"><span data-stu-id="c4955-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="c4955-167">Следующий снимок экрана приветствия показан пример о нем.</span><span class="sxs-lookup"><span data-stu-id="c4955-167">hello following screenshot shows an example about it.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="c4955-169">В hello **атрибуты пользователя** статьи на **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c4955-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="c4955-170">Мы сопоставленной hello Userprincipalname как атрибут уникального пользователя hello здесь, но можно было сопоставить его toohello соответствующее значение, что используемый для обозначения hello пользователь в организации hello, а также сопоставляет поле имени пользователя tooBlackboard Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="c4955-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="c4955-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="c4955-171">Attribute Name</span></span> | <span data-ttu-id="c4955-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="c4955-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="c4955-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="c4955-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="c4955-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="c4955-174">user.userprincipalname</span></span> |

    <span data-ttu-id="c4955-175">а.</span><span class="sxs-lookup"><span data-stu-id="c4955-175">a.</span></span> <span data-ttu-id="c4955-176">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c4955-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c4955-179">b.</span><span class="sxs-lookup"><span data-stu-id="c4955-179">b.</span></span> <span data-ttu-id="c4955-180">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="c4955-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="c4955-181">c.</span><span class="sxs-lookup"><span data-stu-id="c4955-181">c.</span></span> <span data-ttu-id="c4955-182">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="c4955-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c4955-183">d.</span><span class="sxs-lookup"><span data-stu-id="c4955-183">d.</span></span> <span data-ttu-id="c4955-184">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c4955-184">Click **Ok**.</span></span>

4. <span data-ttu-id="c4955-185">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c4955-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="c4955-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c4955-187">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c4955-189">На hello **Blackboard сведения конфигурации** щелкните **Настройка узнать Blackboard** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c4955-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c4955-190">Копировать hello **идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c4955-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="c4955-192">tooconfigure единого входа на **узнать Blackboard** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **идентификатор сущности SAML** слишком[Blackboard сведения поддерживает](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4955-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="c4955-193">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c4955-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4955-194">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c4955-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4955-195">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4955-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4955-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4955-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4955-197">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c4955-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c4955-199">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4955-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4955-200">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c4955-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4955-202">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c4955-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4955-204">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c4955-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4955-206">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c4955-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4955-208">а.</span><span class="sxs-lookup"><span data-stu-id="c4955-208">a.</span></span> <span data-ttu-id="c4955-209">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4955-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4955-210">b.</span><span class="sxs-lookup"><span data-stu-id="c4955-210">b.</span></span> <span data-ttu-id="c4955-211">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c4955-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="c4955-212">c.</span><span class="sxs-lookup"><span data-stu-id="c4955-212">c.</span></span> <span data-ttu-id="c4955-213">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c4955-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c4955-214">d.</span><span class="sxs-lookup"><span data-stu-id="c4955-214">d.</span></span> <span data-ttu-id="c4955-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c4955-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="c4955-216">Создание тестового пользователя Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="c4955-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="c4955-217">В этом разделе описано, как создать пользователя Britta Simon в приложении Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="c4955-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="c4955-218">Приложение Blackboard Learn поддерживает JIT-подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="c4955-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="c4955-219">Убедитесь, что настроены hello утверждения, как описано в разделе "hello"  **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="c4955-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c4955-220">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c4955-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c4955-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooBlackboard Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="c4955-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c4955-223">**tooassign tooBlackboard Britta Simon Дополнительные сведения, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="c4955-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4955-224">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c4955-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c4955-226">В списке приложений hello выберите **Blackboard узнать**.</span><span class="sxs-lookup"><span data-stu-id="c4955-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="c4955-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c4955-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c4955-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c4955-230">Click **Add** button.</span></span> <span data-ttu-id="c4955-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c4955-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c4955-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c4955-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4955-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c4955-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4955-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c4955-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4955-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c4955-236">Testing single sign-on</span></span>

<span data-ttu-id="c4955-237">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c4955-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c4955-238">При нажатии кнопки hello узнать Blackboard плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Blackboard сведения приложения.</span><span class="sxs-lookup"><span data-stu-id="c4955-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="c4955-239">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4955-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c4955-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c4955-240">Additional resources</span></span>

* [<span data-ttu-id="c4955-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4955-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4955-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4955-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

