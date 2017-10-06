---
title: "Руководство по интеграции Azure Active Directory с ADP Globalview | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ADP Globalview."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="c0e32-103">Руководство по интеграции Azure Active Directory с ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="c0e32-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="c0e32-104">В этом учебнике вы узнаете, как toointegrate ADP Globalview в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0e32-104">In this tutorial, you learn how toointegrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0e32-105">Интеграция с Azure AD ADP Globalview предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c0e32-105">Integrating ADP Globalview with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0e32-106">Можно управлять в Azure AD, имеющего доступ tooADP Globalview</span><span class="sxs-lookup"><span data-stu-id="c0e32-106">You can control in Azure AD who has access tooADP Globalview</span></span>
- <span data-ttu-id="c0e32-107">Можно включить на пользователей tooautomatically get вошедшего tooADP Globalview (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0e32-107">You can enable your users tooautomatically get signed-on tooADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0e32-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c0e32-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0e32-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0e32-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0e32-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c0e32-110">Prerequisites</span></span>

<span data-ttu-id="c0e32-111">tooconfigure интеграция Azure AD с ADP Globalview требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c0e32-111">tooconfigure Azure AD integration with ADP Globalview, you need hello following items:</span></span>

- <span data-ttu-id="c0e32-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c0e32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0e32-113">подписка ADP Globalview с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c0e32-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0e32-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c0e32-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0e32-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c0e32-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0e32-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c0e32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0e32-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0e32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0e32-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c0e32-118">Scenario description</span></span>
<span data-ttu-id="c0e32-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c0e32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0e32-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c0e32-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0e32-121">Добавление ADP Globalview из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c0e32-121">Adding ADP Globalview from hello gallery</span></span>
2. <span data-ttu-id="c0e32-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0e32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-hello-gallery"></a><span data-ttu-id="c0e32-123">Добавление ADP Globalview из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c0e32-123">Adding ADP Globalview from hello gallery</span></span>
<span data-ttu-id="c0e32-124">tooconfigure hello интеграции ADP Globalview в Azure AD, вы должны tooadd ADP Globalview из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0e32-124">tooconfigure hello integration of ADP Globalview into Azure AD, you need tooadd ADP Globalview from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0e32-125">**tooadd ADP Globalview из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0e32-125">**tooadd ADP Globalview from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0e32-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c0e32-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0e32-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0e32-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c0e32-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c0e32-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c0e32-133">Введите в поле поиска hello **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-133">In hello search box, type **ADP Globalview**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="c0e32-135">В панели результатов hello выберите **ADP Globalview**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c0e32-135">In hello results panel, select **ADP Globalview**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0e32-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0e32-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0e32-138">В этом разделе описана настройка и проверка единого входа Azure AD в ADP Globalview с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0e32-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c0e32-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ADP Globalview является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0e32-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP Globalview is tooa user in Azure AD.</span></span> <span data-ttu-id="c0e32-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ADP Globalview должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c0e32-140">In other words, a link relationship between an Azure AD user and hello related user in ADP Globalview needs toobe established.</span></span>

<span data-ttu-id="c0e32-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="c0e32-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP Globalview.</span></span>

<span data-ttu-id="c0e32-142">tooconfigure и теста Azure AD единого входа с ADP Globalview, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c0e32-142">tooconfigure and test Azure AD single sign-on with ADP Globalview, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0e32-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c0e32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0e32-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c0e32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0e32-145">**[Создание тестового пользователя, прошедшего ADP Globalview](#creating-an-adp-globalview-test-user) ** -toohave аналог Саймон Britta в ADP Globalview, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0e32-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - toohave a counterpart of Britta Simon in ADP Globalview that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0e32-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c0e32-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0e32-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c0e32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0e32-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0e32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0e32-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="c0e32-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="c0e32-150">**tooconfigure Azure AD единого входа с ADP Globalview выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0e32-150">**tooconfigure Azure AD single sign-on with ADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0e32-151">В hello в hello портала Azure **ADP Globalview** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-151">In hello Azure portal, on hello **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c0e32-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c0e32-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="c0e32-155">На hello **URL-адреса и домена Globalview ADP** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c0e32-155">On hello **ADP Globalview Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="c0e32-157">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://<subdomain>.globalview.adp.com/federate` или`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="c0e32-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0e32-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="c0e32-158">hello value is not real.</span></span> <span data-ttu-id="c0e32-159">Обновите значение hello с hello фактический идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c0e32-159">Update hello value with hello actual Identifier.</span></span> <span data-ttu-id="c0e32-160">Обратитесь к [ADP Globalview поддержки](https://www.adp.com/contact-us/overview.aspx) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="c0e32-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooget hello value.</span></span>
 
4. <span data-ttu-id="c0e32-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c0e32-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="c0e32-163">Hello ADP GlobalView приложения ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="c0e32-163">hello ADP GlobalView application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="c0e32-164">пример Hello следующий снимок экрана для него.</span><span class="sxs-lookup"><span data-stu-id="c0e32-164">hello following screenshot shows an example for it.</span></span> <span data-ttu-id="c0e32-165">Hello утверждения имена всегда быть **«PersonImmutableID»** и из которых сопоставленной tooExtensionAttribute2, который содержит значение hello hello EmployeeID hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0e32-165">hello claim names always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2, which contains hello EmployeeID of hello user.</span></span> <span data-ttu-id="c0e32-166">Здесь hello сопоставление пользователей из Azure AD tooADP GlobalView выполняется на hello EmployeeID, но можно сопоставить их другим значением tooa также основана на параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="c0e32-166">Here hello user mapping from Azure AD tooADP GlobalView is done on hello EmployeeID but you can map it tooa different value also based on your application settings.</span></span> <span data-ttu-id="c0e32-167">Можно работать с hello ADP GlobalView команды первого toouse hello правильный идентификатор пользователя и сопоставить это значение с hello **«PersonImmutableID»** утверждения.</span><span class="sxs-lookup"><span data-stu-id="c0e32-167">You can work with hello ADP GlobalView team first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="c0e32-168">Также можно сопоставить hello утверждения электронной почты и UserID как показано на рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="c0e32-168">You can also map hello Email and UserID claim as shown in hello picture.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="c0e32-170">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c0e32-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c0e32-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="c0e32-171">Attribute Name</span></span> | <span data-ttu-id="c0e32-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="c0e32-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="c0e32-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="c0e32-173">personalimmutableid</span></span> | <span data-ttu-id="c0e32-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="c0e32-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="c0e32-175">email</span><span class="sxs-lookup"><span data-stu-id="c0e32-175">email</span></span>               | <span data-ttu-id="c0e32-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="c0e32-176">user.mail</span></span> |
    | <span data-ttu-id="c0e32-177">userid</span><span class="sxs-lookup"><span data-stu-id="c0e32-177">userid</span></span>              | <span data-ttu-id="c0e32-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="c0e32-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="c0e32-179">а.</span><span class="sxs-lookup"><span data-stu-id="c0e32-179">a.</span></span> <span data-ttu-id="c0e32-180">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c0e32-180">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c0e32-183">b.</span><span class="sxs-lookup"><span data-stu-id="c0e32-183">b.</span></span> <span data-ttu-id="c0e32-184">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="c0e32-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="c0e32-185">c.</span><span class="sxs-lookup"><span data-stu-id="c0e32-185">c.</span></span> <span data-ttu-id="c0e32-186">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="c0e32-186">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c0e32-187">d.</span><span class="sxs-lookup"><span data-stu-id="c0e32-187">d.</span></span> <span data-ttu-id="c0e32-188">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0e32-189">Перед настройкой hello утверждения SAML, необходимо toocontact вашей [ADP Globalview поддержки](https://www.adp.com/contact-us/overview.aspx) и запросить значение hello hello уникальный идентификатор атрибута для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="c0e32-189">Before you can configure hello SAML assertion, you need toocontact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="c0e32-190">Необходимо, чтобы это значение tooconfigure hello пользовательского утверждения для приложения.</span><span class="sxs-lookup"><span data-stu-id="c0e32-190">You need this value tooconfigure hello custom claim for your application.</span></span> 

8. <span data-ttu-id="c0e32-191">На hello **конфигурации ADP Globalview** щелкните **Настройка ADP Globalview** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c0e32-191">On hello **ADP Globalview Configuration** section, click **Configure ADP Globalview** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c0e32-192">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c0e32-192">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="c0e32-194">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c0e32-194">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="c0e32-196">tooconfigure единого входа на **ADP Globalview** стороны, необходимо загрузить hello toosend **сертификата (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[ADP Globalview поддержки](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0e32-196">tooconfigure single sign-on on **ADP Globalview** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="c0e32-197">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c0e32-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0e32-198">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c0e32-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0e32-199">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0e32-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0e32-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0e32-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0e32-201">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e32-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c0e32-203">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0e32-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0e32-204">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c0e32-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="c0e32-206">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0e32-208">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c0e32-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0e32-210">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c0e32-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0e32-212">а.</span><span class="sxs-lookup"><span data-stu-id="c0e32-212">a.</span></span> <span data-ttu-id="c0e32-213">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0e32-214">b.</span><span class="sxs-lookup"><span data-stu-id="c0e32-214">b.</span></span> <span data-ttu-id="c0e32-215">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0e32-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0e32-216">c.</span><span class="sxs-lookup"><span data-stu-id="c0e32-216">c.</span></span> <span data-ttu-id="c0e32-217">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0e32-218">d.</span><span class="sxs-lookup"><span data-stu-id="c0e32-218">d.</span></span> <span data-ttu-id="c0e32-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="c0e32-220">Создание тестового пользователя ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="c0e32-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="c0e32-221">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="c0e32-221">hello objective of this section is toocreate a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="c0e32-222">Работать с [ADP Globalview поддержки](https://www.adp.com/contact-us/overview.aspx) tooadd пользователей hello в hello ADP GlobalView учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c0e32-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP GlobalView account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0e32-223">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c0e32-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0e32-224">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="c0e32-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP Globalview.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c0e32-226">**tooassign Britta Simon tooADP Globalview, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0e32-226">**tooassign Britta Simon tooADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0e32-227">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c0e32-229">В списке приложений hello выберите **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-229">In hello applications list, select **ADP Globalview**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="c0e32-231">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c0e32-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-233">Click **Add** button.</span></span> <span data-ttu-id="c0e32-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c0e32-236">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c0e32-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0e32-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0e32-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c0e32-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0e32-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c0e32-239">Testing single sign-on</span></span>

<span data-ttu-id="c0e32-240">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="c0e32-240">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="c0e32-241">При нажатии кнопки hello ADP GlobalView плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour ADP GlobalView приложения.</span><span class="sxs-lookup"><span data-stu-id="c0e32-241">When you click hello ADP GlobalView tile in hello Access Panel, you should get automatically signed-on tooyour ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0e32-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c0e32-242">Additional resources</span></span>

* [<span data-ttu-id="c0e32-243">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0e32-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0e32-244">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0e32-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

