---
title: "Учебник. Интеграция Azure Active Directory с DigiCert | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 861039d00533b3aeb361d04e45c4460c6fc8cef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="c0acd-103">Учебник. Интеграция Azure Active Directory с DigiCert</span><span class="sxs-lookup"><span data-stu-id="c0acd-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="c0acd-104">В этом учебнике вы узнаете, как toointegrate DigiCert с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0acd-104">In this tutorial, you learn how toointegrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0acd-105">Интеграция с Azure AD DigiCert предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c0acd-105">Integrating DigiCert with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0acd-106">Можно управлять в Azure AD, имеющего доступ tooDigiCert</span><span class="sxs-lookup"><span data-stu-id="c0acd-106">You can control in Azure AD who has access tooDigiCert</span></span>
- <span data-ttu-id="c0acd-107">Можно включить на пользователей tooautomatically get вошедшего tooDigiCert (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0acd-107">You can enable your users tooautomatically get signed-on tooDigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0acd-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c0acd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0acd-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0acd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0acd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c0acd-110">Prerequisites</span></span>

<span data-ttu-id="c0acd-111">tooconfigure интеграция Azure AD с DigiCert требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c0acd-111">tooconfigure Azure AD integration with DigiCert, you need hello following items:</span></span>

- <span data-ttu-id="c0acd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c0acd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0acd-113">подписка с поддержкой единого входа DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c0acd-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0acd-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c0acd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0acd-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c0acd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0acd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c0acd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0acd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0acd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0acd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c0acd-118">Scenario description</span></span>
<span data-ttu-id="c0acd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c0acd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0acd-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c0acd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0acd-121">Добавление DigiCert из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c0acd-121">Adding DigiCert from hello gallery</span></span>
2. <span data-ttu-id="c0acd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0acd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-hello-gallery"></a><span data-ttu-id="c0acd-123">Добавление DigiCert из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c0acd-123">Adding DigiCert from hello gallery</span></span>
<span data-ttu-id="c0acd-124">tooconfigure hello интеграции DigiCert в Azure AD, вы должны tooadd DigiCert из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0acd-124">tooconfigure hello integration of DigiCert into Azure AD, you need tooadd DigiCert from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0acd-125">**tooadd DigiCert из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0acd-125">**tooadd DigiCert from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0acd-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c0acd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0acd-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0acd-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c0acd-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c0acd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c0acd-133">Введите в поле поиска hello **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-133">In hello search box, type **DigiCert**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="c0acd-135">В панели результатов hello выберите **DigiCert**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c0acd-135">In hello results panel, select **DigiCert**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0acd-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0acd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0acd-138">В этом разделе описана настройка и проверка единого входа Azure AD в DigiCert с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0acd-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c0acd-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в DigiCert является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0acd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DigiCert is tooa user in Azure AD.</span></span> <span data-ttu-id="c0acd-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в DigiCert должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c0acd-140">In other words, a link relationship between an Azure AD user and hello related user in DigiCert needs toobe established.</span></span>

<span data-ttu-id="c0acd-141">В DigiCert, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c0acd-141">In DigiCert, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c0acd-142">tooconfigure и теста Azure AD единого входа с DigiCert, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c0acd-142">tooconfigure and test Azure AD single sign-on with DigiCert, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0acd-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c0acd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0acd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c0acd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0acd-145">**[Создание тестового пользователя DigiCert](#creating-a-digicert-test-user)**  -toohave аналог Саймон Britta в DigiCert, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0acd-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - toohave a counterpart of Britta Simon in DigiCert that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0acd-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c0acd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0acd-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c0acd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0acd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0acd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0acd-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложения DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c0acd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="c0acd-150">**tooconfigure Azure AD единого входа с DigiCert, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0acd-150">**tooconfigure Azure AD single sign-on with DigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0acd-151">В hello в hello портала Azure **DigiCert** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-151">In hello Azure portal, on hello **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c0acd-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c0acd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="c0acd-155">На hello **URL-адреса и домена DigiCert** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="c0acd-155">On hello **DigiCert Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="c0acd-157">Приложения DigiCert ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="c0acd-157">DigiCert application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c0acd-158">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c0acd-158">Configure hello following claims for this application.</span></span> <span data-ttu-id="c0acd-159">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="c0acd-159">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c0acd-160">Следующий снимок экрана приветствия показан пример для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c0acd-160">hello following screenshot shows an example for this configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="c0acd-162">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c0acd-162">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c0acd-163">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="c0acd-163">Attribute Name</span></span> | <span data-ttu-id="c0acd-164">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="c0acd-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="c0acd-165">company</span><span class="sxs-lookup"><span data-stu-id="c0acd-165">company</span></span> | <span data-ttu-id="c0acd-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="c0acd-166">< companycode ></span></span> |
    | <span data-ttu-id="c0acd-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="c0acd-167">digicertrole</span></span> | <span data-ttu-id="c0acd-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="c0acd-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="c0acd-169">Здравствуйте, значение **компании** атрибут не является реальным.</span><span class="sxs-lookup"><span data-stu-id="c0acd-169">hello value of **company** attribute is not real.</span></span> <span data-ttu-id="c0acd-170">Введите вместо этого значения фактический код компании.</span><span class="sxs-lookup"><span data-stu-id="c0acd-170">Update this value with actual company code.</span></span> <span data-ttu-id="c0acd-171">значение hello tooget **компании** атрибут контакт [группа поддержки DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="c0acd-171">tooget hello value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="c0acd-172">а.</span><span class="sxs-lookup"><span data-stu-id="c0acd-172">a.</span></span> <span data-ttu-id="c0acd-173">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c0acd-173">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c0acd-176">b.</span><span class="sxs-lookup"><span data-stu-id="c0acd-176">b.</span></span> <span data-ttu-id="c0acd-177">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="c0acd-177">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="c0acd-178">c.</span><span class="sxs-lookup"><span data-stu-id="c0acd-178">c.</span></span> <span data-ttu-id="c0acd-179">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="c0acd-179">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c0acd-180">d.</span><span class="sxs-lookup"><span data-stu-id="c0acd-180">d.</span></span> <span data-ttu-id="c0acd-181">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="c0acd-182">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c0acd-182">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="c0acd-184">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c0acd-184">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c0acd-186">tooconfigure единого входа на **DigiCert** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="c0acd-186">tooconfigure single sign-on on **DigiCert** side, you need toosend hello downloaded **Metadata XML** too[DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="c0acd-187">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="c0acd-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c0acd-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c0acd-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0acd-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c0acd-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0acd-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0acd-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0acd-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0acd-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0acd-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c0acd-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c0acd-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0acd-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0acd-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c0acd-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0acd-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0acd-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c0acd-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0acd-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c0acd-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0acd-203">а.</span><span class="sxs-lookup"><span data-stu-id="c0acd-203">a.</span></span> <span data-ttu-id="c0acd-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0acd-205">b.</span><span class="sxs-lookup"><span data-stu-id="c0acd-205">b.</span></span> <span data-ttu-id="c0acd-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0acd-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0acd-207">c.</span><span class="sxs-lookup"><span data-stu-id="c0acd-207">c.</span></span> <span data-ttu-id="c0acd-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0acd-209">d.</span><span class="sxs-lookup"><span data-stu-id="c0acd-209">d.</span></span> <span data-ttu-id="c0acd-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="c0acd-211">Создание тестового пользователя DigiCert</span><span class="sxs-lookup"><span data-stu-id="c0acd-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="c0acd-212">В этом разделе описано, как создать пользователя Britta Simon в приложении DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c0acd-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="c0acd-213">Можно работать с [группа поддержки DigiCert](mailto:support@digicert.com) tooadd пользователей hello в DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c0acd-213">Please work with [DigiCert support team](mailto:support@digicert.com) tooadd hello users in DigiCert.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0acd-214">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c0acd-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0acd-215">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooDigiCert доступа.</span><span class="sxs-lookup"><span data-stu-id="c0acd-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDigiCert.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c0acd-217">**tooassign tooDigiCert Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0acd-217">**tooassign Britta Simon tooDigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0acd-218">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c0acd-220">В списке приложений hello выберите **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-220">In hello applications list, select **DigiCert**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="c0acd-222">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c0acd-224">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-224">Click **Add** button.</span></span> <span data-ttu-id="c0acd-225">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c0acd-227">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c0acd-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0acd-228">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0acd-229">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c0acd-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0acd-230">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c0acd-230">Testing single sign-on</span></span>

<span data-ttu-id="c0acd-231">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c0acd-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c0acd-232">При выборе плитки DigiCert hello в hello панели доступа, следует получать автоматически вошедшего tooyour DeigiCert приложения.</span><span class="sxs-lookup"><span data-stu-id="c0acd-232">When you click hello DigiCert tile in hello Access Panel, you should get automatically signed-on tooyour DeigiCert application.</span></span>
<span data-ttu-id="c0acd-233">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c0acd-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c0acd-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c0acd-234">Additional resources</span></span>

* [<span data-ttu-id="c0acd-235">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0acd-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0acd-236">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0acd-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

