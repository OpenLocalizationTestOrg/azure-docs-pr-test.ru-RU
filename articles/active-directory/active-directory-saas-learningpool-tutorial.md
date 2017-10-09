---
title: "Руководство по интеграции Azure Active Directory с Learningpool Act | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Learningpool Act."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: f343623f08bb60e143aaff07d93e4ef773232e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="8e50e-103">Руководство по интеграции Azure Active Directory с Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="8e50e-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="8e50e-104">В этом учебнике вы узнаете, как toointegrate Learningpool работать с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e50e-104">In this tutorial, you learn how toointegrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e50e-105">Интеграция с Azure AD Learningpool Act предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8e50e-105">Integrating Learningpool Act with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8e50e-106">Можно управлять в Azure AD, имеющего доступ tooLearningpool Act</span><span class="sxs-lookup"><span data-stu-id="8e50e-106">You can control in Azure AD who has access tooLearningpool Act</span></span>
- <span data-ttu-id="8e50e-107">Можно включить на пользователей tooautomatically get вошедшего tooLearningpool Act (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e50e-107">You can enable your users tooautomatically get signed-on tooLearningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e50e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8e50e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8e50e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e50e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e50e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8e50e-110">Prerequisites</span></span>

<span data-ttu-id="8e50e-111">tooconfigure интеграция Azure AD с Learningpool Act необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8e50e-111">tooconfigure Azure AD integration with Learningpool Act, you need hello following items:</span></span>

- <span data-ttu-id="8e50e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8e50e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e50e-113">подписка с поддержкой единого входа Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8e50e-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e50e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8e50e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e50e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8e50e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e50e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8e50e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e50e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e50e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e50e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8e50e-118">Scenario description</span></span>
<span data-ttu-id="8e50e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8e50e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e50e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8e50e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e50e-121">Добавление Learningpool Act из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8e50e-121">Adding Learningpool Act from hello gallery</span></span>
2. <span data-ttu-id="8e50e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e50e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-hello-gallery"></a><span data-ttu-id="8e50e-123">Добавление Learningpool Act из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8e50e-123">Adding Learningpool Act from hello gallery</span></span>
<span data-ttu-id="8e50e-124">tooconfigure hello интеграции Learningpool Act в Azure AD, вы должны tooadd Learningpool Act из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8e50e-124">tooconfigure hello integration of Learningpool Act into Azure AD, you need tooadd Learningpool Act from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8e50e-125">**tooadd Learningpool Act из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8e50e-125">**tooadd Learningpool Act from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e50e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8e50e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e50e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8e50e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8e50e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e50e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8e50e-133">Введите в поле поиска hello **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-133">In hello search box, type **Learningpool Act**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="8e50e-135">В панели результатов hello выберите **Learningpool Act**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8e50e-135">In hello results panel, select **Learningpool Act**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e50e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e50e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e50e-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Learningpool Act с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e50e-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e50e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Learningpool Act является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e50e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learningpool Act is tooa user in Azure AD.</span></span> <span data-ttu-id="8e50e-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Learningpool Act должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8e50e-140">In other words, a link relationship between an Azure AD user and hello related user in Learningpool Act needs toobe established.</span></span>

<span data-ttu-id="8e50e-141">В Learningpool Act, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8e50e-141">In Learningpool Act, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8e50e-142">tooconfigure и теста Azure AD единого входа с Learningpool Act, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8e50e-142">tooconfigure and test Azure AD single sign-on with Learningpool Act, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8e50e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8e50e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8e50e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8e50e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e50e-145">**[Создание тестового пользователя Learningpool Act](#creating-a-learningpool-act-test-user)**  -toohave аналог Саймон Britta в Learningpool Act, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8e50e-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - toohave a counterpart of Britta Simon in Learningpool Act that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e50e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8e50e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e50e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8e50e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e50e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e50e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e50e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8e50e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="8e50e-150">**tooconfigure Azure AD единого входа с Learningpool Act, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8e50e-150">**tooconfigure Azure AD single sign-on with Learningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e50e-151">В hello в hello портала Azure **Learningpool Act** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-151">In hello Azure portal, on hello **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8e50e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8e50e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="8e50e-155">На hello **Learningpool Act доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8e50e-155">On hello **Learningpool Act Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="8e50e-157">а.</span><span class="sxs-lookup"><span data-stu-id="8e50e-157">a.</span></span> <span data-ttu-id="8e50e-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="8e50e-158">In hello **Sign-on URL** textbox, type hello URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="8e50e-159">b.</span><span class="sxs-lookup"><span data-stu-id="8e50e-159">b.</span></span> <span data-ttu-id="8e50e-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="8e50e-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="8e50e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8e50e-161">These values are not real.</span></span> <span data-ttu-id="8e50e-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8e50e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8e50e-163">Обратитесь к [группа поддержки Learningpool Act клиента](https://www.Learningpool.com/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="8e50e-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="8e50e-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8e50e-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="8e50e-166">Приложение Learningpool Act ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="8e50e-166">Learningpool Act application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8e50e-167">Выполните настройку следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8e50e-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="8e50e-168">Вы можете управлять hello значения этих атрибутов из hello **«Атрибутов»** вкладку приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8e50e-168">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="8e50e-169">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="8e50e-169">hello following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="8e50e-171">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8e50e-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="8e50e-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="8e50e-172">Attribute Name</span></span> | <span data-ttu-id="8e50e-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="8e50e-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="8e50e-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="8e50e-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="8e50e-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8e50e-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="8e50e-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="8e50e-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="8e50e-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8e50e-177">user.givenname</span></span> |
    | <span data-ttu-id="8e50e-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="8e50e-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="8e50e-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="8e50e-179">user.mail</span></span> |    
    | <span data-ttu-id="8e50e-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="8e50e-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="8e50e-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="8e50e-181">user.surname</span></span> |
    
    <span data-ttu-id="8e50e-182">а.</span><span class="sxs-lookup"><span data-stu-id="8e50e-182">a.</span></span> <span data-ttu-id="8e50e-183">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8e50e-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="8e50e-186">b.</span><span class="sxs-lookup"><span data-stu-id="8e50e-186">b.</span></span> <span data-ttu-id="8e50e-187">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="8e50e-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="8e50e-188">c.</span><span class="sxs-lookup"><span data-stu-id="8e50e-188">c.</span></span> <span data-ttu-id="8e50e-189">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="8e50e-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="8e50e-190">d.</span><span class="sxs-lookup"><span data-stu-id="8e50e-190">d.</span></span> <span data-ttu-id="8e50e-191">Оставьте hello **имен** пустым.</span><span class="sxs-lookup"><span data-stu-id="8e50e-191">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="8e50e-192">д.</span><span class="sxs-lookup"><span data-stu-id="8e50e-192">e.</span></span> <span data-ttu-id="8e50e-193">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-193">Click **Ok**.</span></span>

7. <span data-ttu-id="8e50e-194">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8e50e-194">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8e50e-196">tooconfigure единого входа на **Learningpool Act** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группой поддержки Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="8e50e-196">tooconfigure single sign-on on **Learningpool Act** side, you need toosend hello downloaded **Metadata XML** too[Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="8e50e-197">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="8e50e-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8e50e-198">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8e50e-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8e50e-199">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8e50e-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8e50e-200">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e50e-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e50e-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e50e-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e50e-202">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8e50e-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8e50e-204">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8e50e-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e50e-205">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8e50e-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e50e-207">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e50e-209">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8e50e-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e50e-211">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8e50e-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e50e-213">а.</span><span class="sxs-lookup"><span data-stu-id="8e50e-213">a.</span></span> <span data-ttu-id="8e50e-214">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e50e-215">b.</span><span class="sxs-lookup"><span data-stu-id="8e50e-215">b.</span></span> <span data-ttu-id="8e50e-216">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e50e-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e50e-217">c.</span><span class="sxs-lookup"><span data-stu-id="8e50e-217">c.</span></span> <span data-ttu-id="8e50e-218">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8e50e-219">d.</span><span class="sxs-lookup"><span data-stu-id="8e50e-219">d.</span></span> <span data-ttu-id="8e50e-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="8e50e-221">Создание тестового пользователя Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="8e50e-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="8e50e-222">Пользователи toolog tooenable Azure AD в tooLearningpool Act, их необходимо подготовить в Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8e50e-222">tooenable Azure AD users toolog in tooLearningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="8e50e-223">Нет элемента действия для вас tooconfigure подготовки пользователей tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8e50e-223">There is no action item for you tooconfigure user provisioning tooLearningpool Act.</span></span>  
<span data-ttu-id="8e50e-224">Пользователи должны toobe, созданные вашей [группой поддержки Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="8e50e-224">Users need toobe created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="8e50e-225">Можно использовать любые другие Learningpool Act пользователя средства создания учетных записей или интерфейсы API, предоставляемые Learningpool Act tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="8e50e-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8e50e-226">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8e50e-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8e50e-227">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8e50e-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearningpool Act.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8e50e-229">**tooassign Britta Simon tooLearningpool Act, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8e50e-229">**tooassign Britta Simon tooLearningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e50e-230">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8e50e-232">В списке приложений hello выберите **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-232">In hello applications list, select **Learningpool Act**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="8e50e-234">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8e50e-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-236">Click **Add** button.</span></span> <span data-ttu-id="8e50e-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8e50e-239">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8e50e-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8e50e-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e50e-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8e50e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e50e-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8e50e-242">Testing single sign-on</span></span>

<span data-ttu-id="8e50e-243">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="8e50e-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8e50e-244">При нажатии кнопки hello Learningpool Act плитки в панели доступа hello, вы должны получить tooyour автоматически подписью в приложении Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8e50e-244">When you click hello Learningpool Act tile in hello Access Panel, you should get automatically signed-on tooyour Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e50e-245">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8e50e-245">Additional resources</span></span>

* [<span data-ttu-id="8e50e-246">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e50e-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e50e-247">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e50e-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

