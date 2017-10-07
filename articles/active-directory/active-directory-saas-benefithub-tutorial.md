---
title: "Руководство по интеграции Azure Active Directory с BenefitHub | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="f514c-103">Руководство по интеграции Azure Active Directory с BenefitHub</span><span class="sxs-lookup"><span data-stu-id="f514c-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="f514c-104">В этом учебнике вы узнаете, как toointegrate BenefitHub с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f514c-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f514c-105">Интеграция с Azure AD BenefitHub предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f514c-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f514c-106">Можно управлять в Azure AD, имеющего доступ tooBenefitHub</span><span class="sxs-lookup"><span data-stu-id="f514c-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="f514c-107">Можно включить на пользователей tooautomatically get вошедшего tooBenefitHub (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f514c-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f514c-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f514c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f514c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f514c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f514c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f514c-110">Prerequisites</span></span>

<span data-ttu-id="f514c-111">tooconfigure интеграция Azure AD с BenefitHub требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f514c-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="f514c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f514c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f514c-113">подписка BenefitHub с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f514c-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f514c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f514c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f514c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f514c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f514c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f514c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f514c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f514c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f514c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f514c-118">Scenario description</span></span>
<span data-ttu-id="f514c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f514c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f514c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f514c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f514c-121">Добавление BenefitHub из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f514c-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="f514c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f514c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="f514c-123">Добавление BenefitHub из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f514c-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="f514c-124">tooconfigure hello интеграции BenefitHub в Azure AD, вы должны tooadd BenefitHub из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f514c-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f514c-125">**tooadd BenefitHub из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f514c-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f514c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f514c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f514c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f514c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f514c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f514c-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f514c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f514c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f514c-133">Введите в поле поиска hello **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="f514c-133">In hello search box, type **BenefitHub**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="f514c-135">В панели результатов hello выберите **BenefitHub**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f514c-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f514c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f514c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f514c-138">В этом разделе описана настройка и проверка единого входа Azure AD в BenefitHub с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f514c-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f514c-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BenefitHub является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f514c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="f514c-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в BenefitHub должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f514c-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="f514c-141">В BenefitHub, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f514c-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f514c-142">tooconfigure и теста Azure AD единого входа с BenefitHub, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f514c-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f514c-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f514c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f514c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f514c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f514c-145">**[Создание тестового пользователя BenefitHub](#creating-a-benefithub-test-user)**  -toohave аналог Саймон Britta в BenefitHub, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f514c-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f514c-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f514c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f514c-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f514c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f514c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f514c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f514c-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="f514c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="f514c-150">**tooconfigure Azure AD единого входа с BenefitHub, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f514c-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="f514c-151">В hello в hello портала Azure **BenefitHub** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f514c-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f514c-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f514c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="f514c-155">На hello **URL-адреса и домена BenefitHub** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f514c-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="f514c-157">а.</span><span class="sxs-lookup"><span data-stu-id="f514c-157">a.</span></span> <span data-ttu-id="f514c-158">В hello **идентификатор** введите:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="f514c-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="f514c-159">b.</span><span class="sxs-lookup"><span data-stu-id="f514c-159">b.</span></span> <span data-ttu-id="f514c-160">В hello **URL-адрес ответа** введите:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="f514c-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="f514c-161">Hello BenefitHub приложения ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="f514c-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="f514c-162">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f514c-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="f514c-163">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="f514c-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="f514c-165">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна настройки атрибутов токена SAML, как показано в hello предшествующий образ и выполнить следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f514c-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="f514c-166">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="f514c-166">Attribute Name</span></span> | <span data-ttu-id="f514c-167">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="f514c-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="f514c-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="f514c-168">organizationid</span></span> | <span data-ttu-id="f514c-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="f514c-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="f514c-170">Это значение атрибута приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="f514c-170">This attribute value is not real.</span></span> <span data-ttu-id="f514c-171">Введите вместо этого значения фактическое значение organizationid.</span><span class="sxs-lookup"><span data-stu-id="f514c-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="f514c-172">Обратитесь к [BenefitHub поддержки](https://www.benefithub.com/Home/ContactUs) tooget hello фактическое organizationid.</span><span class="sxs-lookup"><span data-stu-id="f514c-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="f514c-173">а.</span><span class="sxs-lookup"><span data-stu-id="f514c-173">a.</span></span> <span data-ttu-id="f514c-174">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f514c-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f514c-177">b.</span><span class="sxs-lookup"><span data-stu-id="f514c-177">b.</span></span> <span data-ttu-id="f514c-178">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f514c-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f514c-179">c.</span><span class="sxs-lookup"><span data-stu-id="f514c-179">c.</span></span> <span data-ttu-id="f514c-180">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f514c-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f514c-181">d.</span><span class="sxs-lookup"><span data-stu-id="f514c-181">d.</span></span> <span data-ttu-id="f514c-182">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f514c-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f514c-183">Перед настройкой hello утверждения SAML, необходимо toocontact вашей [BenefitHub поддержки](https://www.benefithub.com/Home/ContactUs) и запросить значение hello hello уникальный идентификатор атрибута для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="f514c-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="f514c-184">Необходимо, чтобы это значение tooconfigure hello пользовательского утверждения для приложения.</span><span class="sxs-lookup"><span data-stu-id="f514c-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="f514c-185">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f514c-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="f514c-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f514c-187">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f514c-189">tooconfigure единого входа на **BenefitHub** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[BenefitHub поддержки](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="f514c-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="f514c-190">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="f514c-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f514c-191">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f514c-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f514c-192">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f514c-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f514c-193">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f514c-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f514c-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f514c-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="f514c-195">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f514c-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f514c-197">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f514c-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f514c-198">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f514c-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f514c-200">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f514c-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f514c-202">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f514c-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f514c-204">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f514c-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f514c-206">а.</span><span class="sxs-lookup"><span data-stu-id="f514c-206">a.</span></span> <span data-ttu-id="f514c-207">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f514c-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f514c-208">b.</span><span class="sxs-lookup"><span data-stu-id="f514c-208">b.</span></span> <span data-ttu-id="f514c-209">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f514c-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f514c-210">c.</span><span class="sxs-lookup"><span data-stu-id="f514c-210">c.</span></span> <span data-ttu-id="f514c-211">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f514c-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f514c-212">d.</span><span class="sxs-lookup"><span data-stu-id="f514c-212">d.</span></span> <span data-ttu-id="f514c-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f514c-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="f514c-214">Создание тестового пользователя BenefitHub</span><span class="sxs-lookup"><span data-stu-id="f514c-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="f514c-215">В этом разделе описано, как создать пользователя Britta Simon в приложении BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="f514c-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="f514c-216">Работать с [BenefitHub поддержки](https://www.benefithub.com/Home/ContactUs) для добавления пользователей hello в платформе BenefitHub hello.</span><span class="sxs-lookup"><span data-stu-id="f514c-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="f514c-217">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="f514c-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f514c-218">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f514c-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f514c-219">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBenefitHub доступа.</span><span class="sxs-lookup"><span data-stu-id="f514c-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f514c-221">**tooassign tooBenefitHub Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f514c-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="f514c-222">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f514c-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f514c-224">В списке приложений hello выберите **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="f514c-224">In hello applications list, select **BenefitHub**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="f514c-226">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f514c-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f514c-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f514c-228">Click **Add** button.</span></span> <span data-ttu-id="f514c-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f514c-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f514c-231">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f514c-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f514c-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f514c-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f514c-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f514c-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f514c-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f514c-234">Testing single sign-on</span></span>

<span data-ttu-id="f514c-235">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f514c-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f514c-236">При нажатии кнопки hello BenefitHub плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour BenefitHub приложения.</span><span class="sxs-lookup"><span data-stu-id="f514c-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="f514c-237">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f514c-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f514c-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f514c-238">Additional resources</span></span>

* [<span data-ttu-id="f514c-239">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f514c-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f514c-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f514c-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

