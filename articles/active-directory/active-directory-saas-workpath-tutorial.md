---
title: "Руководство. Интеграция Azure Active Directory с Workpath | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Workpath."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 69f443f314edb7c8c489a6c193e09b6f8fe6795a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="a2a48-103">Руководство. Интеграция Azure Active Directory с Workpath</span><span class="sxs-lookup"><span data-stu-id="a2a48-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="a2a48-104">В этом учебнике вы узнаете, как toointegrate Workpath с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2a48-104">In this tutorial, you learn how toointegrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2a48-105">Интеграция с Azure AD Workpath предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a2a48-105">Integrating Workpath with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2a48-106">Можно управлять в Azure AD, имеющего доступ tooWorkpath</span><span class="sxs-lookup"><span data-stu-id="a2a48-106">You can control in Azure AD who has access tooWorkpath</span></span>
- <span data-ttu-id="a2a48-107">Можно включить на пользователей tooautomatically get вошедшего tooWorkpath (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a48-107">You can enable your users tooautomatically get signed-on tooWorkpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2a48-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a2a48-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2a48-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2a48-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2a48-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a2a48-110">Prerequisites</span></span>

<span data-ttu-id="a2a48-111">tooconfigure интеграция Azure AD с Workpath требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a2a48-111">tooconfigure Azure AD integration with Workpath, you need hello following items:</span></span>

- <span data-ttu-id="a2a48-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a2a48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2a48-113">подписка Workpath с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a2a48-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2a48-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a2a48-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2a48-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a2a48-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2a48-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a2a48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2a48-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2a48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2a48-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a2a48-118">Scenario description</span></span>
<span data-ttu-id="a2a48-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a2a48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2a48-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a2a48-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2a48-121">Добавление Workpath из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a2a48-121">Adding Workpath from hello gallery</span></span>
2. <span data-ttu-id="a2a48-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-hello-gallery"></a><span data-ttu-id="a2a48-123">Добавление Workpath из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a2a48-123">Adding Workpath from hello gallery</span></span>
<span data-ttu-id="a2a48-124">tooconfigure hello интеграции Workpath в Azure AD, вы должны tooadd Workpath из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a2a48-124">tooconfigure hello integration of Workpath into Azure AD, you need tooadd Workpath from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2a48-125">**tooadd Workpath из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2a48-125">**tooadd Workpath from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2a48-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a2a48-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2a48-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2a48-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a2a48-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a2a48-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a2a48-133">Введите в поле поиска hello **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-133">In hello search box, type **Workpath**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="a2a48-135">В панели результатов hello выберите **Workpath**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a2a48-135">In hello results panel, select **Workpath**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2a48-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a48-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2a48-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Workpath с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2a48-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2a48-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Workpath является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2a48-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workpath is tooa user in Azure AD.</span></span> <span data-ttu-id="a2a48-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Workpath должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a2a48-140">In other words, a link relationship between an Azure AD user and hello related user in Workpath needs toobe established.</span></span>

<span data-ttu-id="a2a48-141">В Workpath, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a2a48-141">In Workpath, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a2a48-142">tooconfigure и теста Azure AD единого входа с Workpath, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a2a48-142">tooconfigure and test Azure AD single sign-on with Workpath, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2a48-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a2a48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2a48-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a2a48-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2a48-145">**[Создание тестового пользователя Workpath](#creating-a-workpath-test-user)**  -toohave аналог Саймон Britta в Workpath, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a2a48-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - toohave a counterpart of Britta Simon in Workpath that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2a48-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a2a48-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2a48-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a2a48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2a48-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a48-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2a48-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Workpath.</span><span class="sxs-lookup"><span data-stu-id="a2a48-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="a2a48-150">**tooconfigure Azure AD единого входа с Workpath, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2a48-150">**tooconfigure Azure AD single sign-on with Workpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2a48-151">В hello в hello портала Azure **Workpath** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-151">In hello Azure portal, on hello **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a2a48-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a2a48-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="a2a48-155">На hello **URL-адреса и домена Workpath** статьи, при желании tooconfigure приложения hello в **поставщика Удостоверений** инициируемых режиме выполняется hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="a2a48-155">On hello **Workpath Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="a2a48-157">а.</span><span class="sxs-lookup"><span data-stu-id="a2a48-157">a.</span></span> <span data-ttu-id="a2a48-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="a2a48-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="a2a48-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2a48-159">b.</span></span> <span data-ttu-id="a2a48-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="a2a48-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="a2a48-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="a2a48-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a2a48-162">При необходимости приложение hello tooconfigure в **SP** инициировал режим, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a2a48-162">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="a2a48-164">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="a2a48-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2a48-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a2a48-165">These values are not real.</span></span> <span data-ttu-id="a2a48-166">Обновите эти значения с hello фактический URL-адрес входа, идентификатор и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="a2a48-166">Update these values with hello actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="a2a48-167">Обратитесь к [Workpath поддержки](https://help.workpath.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="a2a48-167">Contact [Workpath support team](https://help.workpath.com) tooget these values.</span></span>

5. <span data-ttu-id="a2a48-168">Workpath приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="a2a48-168">Workpath application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a2a48-169">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a2a48-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="a2a48-170">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="a2a48-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a2a48-171">Следующий снимок экрана приветствия показан пример для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a2a48-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="a2a48-173">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a2a48-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="a2a48-174">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="a2a48-174">Attribute Name</span></span> | <span data-ttu-id="a2a48-175">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="a2a48-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="a2a48-176">first_name</span><span class="sxs-lookup"><span data-stu-id="a2a48-176">first_name</span></span> | <span data-ttu-id="a2a48-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a2a48-177">user.givenname</span></span> |
    | <span data-ttu-id="a2a48-178">last_name</span><span class="sxs-lookup"><span data-stu-id="a2a48-178">last_name</span></span> | <span data-ttu-id="a2a48-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="a2a48-179">user.surname</span></span> |
    
    <span data-ttu-id="a2a48-180">а.</span><span class="sxs-lookup"><span data-stu-id="a2a48-180">a.</span></span> <span data-ttu-id="a2a48-181">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a2a48-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="a2a48-183">b.</span><span class="sxs-lookup"><span data-stu-id="a2a48-183">b.</span></span> <span data-ttu-id="a2a48-184">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="a2a48-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a2a48-186">c.</span><span class="sxs-lookup"><span data-stu-id="a2a48-186">c.</span></span> <span data-ttu-id="a2a48-187">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="a2a48-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="a2a48-188">d.</span><span class="sxs-lookup"><span data-stu-id="a2a48-188">d.</span></span> <span data-ttu-id="a2a48-189">Оставьте hello **имен** пустое текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="a2a48-189">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="a2a48-190">д.</span><span class="sxs-lookup"><span data-stu-id="a2a48-190">e.</span></span> <span data-ttu-id="a2a48-191">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="a2a48-192">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a2a48-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="a2a48-194">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a2a48-194">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="a2a48-196">На hello **конфигурации Workpath** щелкните **Настройка Workpath** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a2a48-196">On hello **Workpath Configuration** section, click **Configure Workpath** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a2a48-197">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a2a48-197">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="a2a48-199">tooconfigure единого входа на **Workpath** стороны, необходимо загрузить hello toosend **метаданные в формате XML**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Workpath поддержки](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="a2a48-199">tooconfigure single sign-on on **Workpath** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="a2a48-200">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a2a48-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2a48-201">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a2a48-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2a48-202">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2a48-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2a48-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2a48-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2a48-204">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a2a48-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a2a48-206">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2a48-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2a48-207">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a2a48-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2a48-209">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2a48-211">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a2a48-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2a48-213">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a2a48-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2a48-215">а.</span><span class="sxs-lookup"><span data-stu-id="a2a48-215">a.</span></span> <span data-ttu-id="a2a48-216">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2a48-217">b.</span><span class="sxs-lookup"><span data-stu-id="a2a48-217">b.</span></span> <span data-ttu-id="a2a48-218">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2a48-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2a48-219">c.</span><span class="sxs-lookup"><span data-stu-id="a2a48-219">c.</span></span> <span data-ttu-id="a2a48-220">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2a48-221">d.</span><span class="sxs-lookup"><span data-stu-id="a2a48-221">d.</span></span> <span data-ttu-id="a2a48-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="a2a48-223">Создание тестового пользователя Workpath</span><span class="sxs-lookup"><span data-stu-id="a2a48-223">Creating a Workpath test user</span></span>

<span data-ttu-id="a2a48-224">Workpath поддерживает JIT-подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="a2a48-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="a2a48-225">После проверки подлинности пользователей создаются в приложении hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="a2a48-225">After authentication users are created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2a48-226">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a2a48-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2a48-227">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWorkpath доступа.</span><span class="sxs-lookup"><span data-stu-id="a2a48-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkpath.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a2a48-229">**tooassign tooWorkpath Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2a48-229">**tooassign Britta Simon tooWorkpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2a48-230">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a2a48-232">В списке приложений hello выберите **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-232">In hello applications list, select **Workpath**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="a2a48-234">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a2a48-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-236">Click **Add** button.</span></span> <span data-ttu-id="a2a48-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a2a48-239">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a2a48-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2a48-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2a48-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a2a48-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2a48-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a2a48-242">Testing single sign-on</span></span>

<span data-ttu-id="a2a48-243">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a2a48-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2a48-244">При нажатии кнопки hello Workpath плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Workpath приложения.</span><span class="sxs-lookup"><span data-stu-id="a2a48-244">When you click hello Workpath tile in hello Access Panel, you should get automatically signed-on tooyour Workpath application.</span></span>
<span data-ttu-id="a2a48-245">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2a48-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2a48-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a2a48-246">Additional resources</span></span>

* [<span data-ttu-id="a2a48-247">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2a48-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2a48-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2a48-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

