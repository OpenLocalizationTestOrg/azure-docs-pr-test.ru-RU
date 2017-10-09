---
title: "Руководство. Интеграция Azure Active Directory с eKincare | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 16129e3384132bb34744aadf088bb65f07ed7a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="6400e-103">Руководство. Интеграция Azure Active Directory с eKincare</span><span class="sxs-lookup"><span data-stu-id="6400e-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="6400e-104">В этом учебнике вы узнаете, как eKincare toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6400e-104">In this tutorial, you learn how toointegrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6400e-105">Интеграция с Azure AD eKincare предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="6400e-105">Integrating eKincare with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6400e-106">Можно управлять в Azure AD, имеющего доступ tooeKincare</span><span class="sxs-lookup"><span data-stu-id="6400e-106">You can control in Azure AD who has access tooeKincare</span></span>
- <span data-ttu-id="6400e-107">Можно включить на пользователей tooautomatically get вошедшего tooeKincare (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="6400e-107">You can enable your users tooautomatically get signed-on tooeKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6400e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="6400e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6400e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6400e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6400e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6400e-110">Prerequisites</span></span>

<span data-ttu-id="6400e-111">tooconfigure интеграция Azure AD с eKincare требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="6400e-111">tooconfigure Azure AD integration with eKincare, you need hello following items:</span></span>

- <span data-ttu-id="6400e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6400e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6400e-113">подписка eKincare с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="6400e-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6400e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6400e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6400e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="6400e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6400e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6400e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6400e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6400e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6400e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6400e-118">Scenario description</span></span>
<span data-ttu-id="6400e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6400e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6400e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="6400e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6400e-121">Добавление eKincare из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6400e-121">Adding eKincare from hello gallery</span></span>
2. <span data-ttu-id="6400e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6400e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-hello-gallery"></a><span data-ttu-id="6400e-123">Добавление eKincare из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6400e-123">Adding eKincare from hello gallery</span></span>
<span data-ttu-id="6400e-124">tooconfigure hello интеграции eKincare в Azure AD, вы должны eKincare tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6400e-124">tooconfigure hello integration of eKincare into Azure AD, you need tooadd eKincare from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6400e-125">**eKincare tooadd из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6400e-125">**tooadd eKincare from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6400e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="6400e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6400e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="6400e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6400e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6400e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="6400e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6400e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="6400e-133">Введите в поле поиска hello **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="6400e-133">In hello search box, type **eKincare**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="6400e-135">В панели результатов hello выберите **eKincare**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6400e-135">In hello results panel, select **eKincare**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6400e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6400e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6400e-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение eKincare с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6400e-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6400e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в eKincare является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6400e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eKincare is tooa user in Azure AD.</span></span> <span data-ttu-id="6400e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в eKincare должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="6400e-140">In other words, a link relationship between an Azure AD user and hello related user in eKincare needs toobe established.</span></span>

<span data-ttu-id="6400e-141">В eKincare, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="6400e-141">In eKincare, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6400e-142">tooconfigure и теста Azure AD единого входа с eKincare, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6400e-142">tooconfigure and test Azure AD single sign-on with eKincare, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6400e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="6400e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6400e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="6400e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6400e-145">**[Создание тестового пользователя eKincare](#creating-a-ekincare-test-user)**  -toohave аналог Саймон Britta в eKincare, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="6400e-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - toohave a counterpart of Britta Simon in eKincare that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6400e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="6400e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6400e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6400e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6400e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6400e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6400e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении eKincare.</span><span class="sxs-lookup"><span data-stu-id="6400e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="6400e-150">**tooconfigure Azure AD единого входа с eKincare, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6400e-150">**tooconfigure Azure AD single sign-on with eKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="6400e-151">В hello в hello портала Azure **eKincare** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="6400e-151">In hello Azure portal, on hello **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="6400e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="6400e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="6400e-155">На hello **eKincare URL-адреса и домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6400e-155">On hello **eKincare Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="6400e-157">а.</span><span class="sxs-lookup"><span data-stu-id="6400e-157">a.</span></span> <span data-ttu-id="6400e-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="6400e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="6400e-159">b.</span><span class="sxs-lookup"><span data-stu-id="6400e-159">b.</span></span> <span data-ttu-id="6400e-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="6400e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6400e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="6400e-161">These values are not real.</span></span> <span data-ttu-id="6400e-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6400e-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6400e-163">Обратитесь к [eKincare поддержки](mailto:tech@ekincare.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="6400e-163">Contact [eKincare support team](mailto:tech@ekincare.com) tooget these values.</span></span>
 
4. <span data-ttu-id="6400e-164">eKincare приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="6400e-164">eKincare application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="6400e-165">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6400e-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="6400e-166">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="6400e-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="6400e-167">Следующий снимок экрана приветствия показан пример для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6400e-167">hello following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="6400e-168">Hello имя утверждения всегда будет **«employeeid»** и значение hello, из которых сопоставленной toouser.extensionattribute1, содержащий employeeid hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="6400e-168">hello claim name will always be **"employeeid"** and hello value of which we have mapped toouser.extensionattribute1, that contains hello employeeid of hello user.</span></span> <span data-ttu-id="6400e-169">Здравствуйте, т. е. остальные два утверждения имя</span><span class="sxs-lookup"><span data-stu-id="6400e-169">hello other two claims' name i.e</span></span> <span data-ttu-id="6400e-170">**«organizationid»** и **«название_организации»** всегда будет одинаковым и их значений содержатся подробные hello hello организации пользователя hello соответственно.</span><span class="sxs-lookup"><span data-stu-id="6400e-170">**"organizationid"** and **"organizationname"** will always be same and their values contain hello details of hello organization of hello user respectively.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="6400e-172">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6400e-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="6400e-173">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="6400e-173">Attribute Name</span></span> | <span data-ttu-id="6400e-174">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="6400e-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="6400e-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="6400e-175">employeeid</span></span> | <span data-ttu-id="6400e-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="6400e-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="6400e-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="6400e-177">organizationid</span></span> | <span data-ttu-id="6400e-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="6400e-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="6400e-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="6400e-179">organizationname</span></span> | <span data-ttu-id="6400e-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="6400e-180">*user.companyname*</span></span> |

    <span data-ttu-id="6400e-181">а.</span><span class="sxs-lookup"><span data-stu-id="6400e-181">a.</span></span> <span data-ttu-id="6400e-182">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6400e-182">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="6400e-185">b.</span><span class="sxs-lookup"><span data-stu-id="6400e-185">b.</span></span> <span data-ttu-id="6400e-186">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="6400e-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="6400e-187">c.</span><span class="sxs-lookup"><span data-stu-id="6400e-187">c.</span></span> <span data-ttu-id="6400e-188">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="6400e-188">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6400e-189">d.</span><span class="sxs-lookup"><span data-stu-id="6400e-189">d.</span></span> <span data-ttu-id="6400e-190">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6400e-190">Click **Ok**</span></span>

6. <span data-ttu-id="6400e-191">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="6400e-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="6400e-193">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6400e-193">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6400e-195">tooconfigure единого входа на **eKincare** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[eKincare поддержки](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="6400e-195">tooconfigure single sign-on on **eKincare** side, you need toosend hello downloaded **Metadata XML** too[eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="6400e-196">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="6400e-196">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6400e-197">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="6400e-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6400e-198">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="6400e-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6400e-199">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6400e-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6400e-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6400e-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="6400e-201">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6400e-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="6400e-203">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6400e-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6400e-204">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="6400e-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6400e-206">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6400e-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6400e-208">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="6400e-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6400e-210">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6400e-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6400e-212">а.</span><span class="sxs-lookup"><span data-stu-id="6400e-212">a.</span></span> <span data-ttu-id="6400e-213">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6400e-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6400e-214">b.</span><span class="sxs-lookup"><span data-stu-id="6400e-214">b.</span></span> <span data-ttu-id="6400e-215">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6400e-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6400e-216">c.</span><span class="sxs-lookup"><span data-stu-id="6400e-216">c.</span></span> <span data-ttu-id="6400e-217">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="6400e-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6400e-218">d.</span><span class="sxs-lookup"><span data-stu-id="6400e-218">d.</span></span> <span data-ttu-id="6400e-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6400e-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="6400e-220">Создание тестового пользователя eKincare</span><span class="sxs-lookup"><span data-stu-id="6400e-220">Creating a eKincare test user</span></span>

<span data-ttu-id="6400e-221">Приложение поддерживает только в подготовки пользователей время и после проверки подлинности пользователей автоматически создаются в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="6400e-221">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6400e-222">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="6400e-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6400e-223">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooeKincare доступа.</span><span class="sxs-lookup"><span data-stu-id="6400e-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeKincare.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="6400e-225">**tooassign tooeKincare Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6400e-225">**tooassign Britta Simon tooeKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="6400e-226">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6400e-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="6400e-228">В списке приложений hello выберите **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="6400e-228">In hello applications list, select **eKincare**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="6400e-230">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="6400e-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="6400e-232">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6400e-232">Click **Add** button.</span></span> <span data-ttu-id="6400e-233">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6400e-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="6400e-235">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="6400e-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6400e-236">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6400e-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6400e-237">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="6400e-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6400e-238">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6400e-238">Testing single sign-on</span></span>

<span data-ttu-id="6400e-239">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="6400e-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6400e-240">При нажатии кнопки hello eKincare плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour eKincare приложения.</span><span class="sxs-lookup"><span data-stu-id="6400e-240">When you click hello eKincare tile in hello Access Panel, you should get automatically signed-on tooyour eKincare application.</span></span>
<span data-ttu-id="6400e-241">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6400e-241">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6400e-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6400e-242">Additional resources</span></span>

* [<span data-ttu-id="6400e-243">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6400e-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6400e-244">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6400e-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

