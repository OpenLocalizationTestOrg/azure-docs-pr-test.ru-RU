---
title: "Руководство по интеграции Azure Active Directory с Klue | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Klue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: bb9134a558d6c050f428690d57a3cea850b7dbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="f4646-103">Руководство по интеграции Azure Active Directory с Klue</span><span class="sxs-lookup"><span data-stu-id="f4646-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="f4646-104">В этом учебнике вы узнаете, как toointegrate Klue с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4646-104">In this tutorial, you learn how toointegrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4646-105">Интеграция с Azure AD Klue предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f4646-105">Integrating Klue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f4646-106">Можно управлять в Azure AD, имеющего доступ tooKlue</span><span class="sxs-lookup"><span data-stu-id="f4646-106">You can control in Azure AD who has access tooKlue</span></span>
- <span data-ttu-id="f4646-107">Можно включить на пользователей tooautomatically get вошедшего tooKlue (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4646-107">You can enable your users tooautomatically get signed-on tooKlue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4646-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f4646-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f4646-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4646-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4646-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f4646-110">Prerequisites</span></span>

<span data-ttu-id="f4646-111">tooconfigure интеграция Azure AD с Klue требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f4646-111">tooconfigure Azure AD integration with Klue, you need hello following items:</span></span>

- <span data-ttu-id="f4646-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f4646-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4646-113">подписка Klue с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f4646-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4646-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f4646-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4646-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f4646-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4646-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f4646-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4646-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4646-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4646-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f4646-118">Scenario description</span></span>
<span data-ttu-id="f4646-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f4646-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4646-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f4646-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4646-121">Добавление Klue из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f4646-121">Adding Klue from hello gallery</span></span>
2. <span data-ttu-id="f4646-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4646-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-hello-gallery"></a><span data-ttu-id="f4646-123">Добавление Klue из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f4646-123">Adding Klue from hello gallery</span></span>
<span data-ttu-id="f4646-124">tooconfigure hello интеграции Klue в Azure AD, вы должны tooadd Klue из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f4646-124">tooconfigure hello integration of Klue into Azure AD, you need tooadd Klue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f4646-125">**tooadd Klue из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4646-125">**tooadd Klue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4646-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f4646-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f4646-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f4646-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f4646-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f4646-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f4646-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f4646-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f4646-133">Введите в поле поиска hello **Klue**.</span><span class="sxs-lookup"><span data-stu-id="f4646-133">In hello search box, type **Klue**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="f4646-135">В панели результатов hello выберите **Klue**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f4646-135">In hello results panel, select **Klue**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4646-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4646-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4646-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Klue с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4646-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f4646-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Klue является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4646-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Klue is tooa user in Azure AD.</span></span> <span data-ttu-id="f4646-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Klue должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f4646-140">In other words, a link relationship between an Azure AD user and hello related user in Klue needs toobe established.</span></span>

<span data-ttu-id="f4646-141">В Klue, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f4646-141">In Klue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f4646-142">tooconfigure и теста Azure AD единого входа с Klue, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f4646-142">tooconfigure and test Azure AD single sign-on with Klue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f4646-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f4646-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f4646-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f4646-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4646-145">**[Создание тестового пользователя Klue](#creating-a-klue-test-user)**  -toohave аналог Саймон Britta в Klue, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4646-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - toohave a counterpart of Britta Simon in Klue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4646-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f4646-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4646-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f4646-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4646-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4646-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4646-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Klue.</span><span class="sxs-lookup"><span data-stu-id="f4646-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="f4646-150">**tooconfigure Azure AD единого входа с Klue, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4646-150">**tooconfigure Azure AD single sign-on with Klue, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4646-151">В hello в hello портала Azure **Klue** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f4646-151">In hello Azure portal, on hello **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f4646-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f4646-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="f4646-155">На hello **Klue доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="f4646-155">On hello **Klue Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="f4646-157">а.</span><span class="sxs-lookup"><span data-stu-id="f4646-157">a.</span></span> <span data-ttu-id="f4646-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="f4646-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="f4646-159">b.</span><span class="sxs-lookup"><span data-stu-id="f4646-159">b.</span></span> <span data-ttu-id="f4646-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="f4646-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="f4646-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="f4646-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="f4646-162">При необходимости приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="f4646-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="f4646-164">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="f4646-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="f4646-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f4646-165">These values are not real.</span></span> <span data-ttu-id="f4646-166">Обновите эти значения с hello фактический URL-адрес ответа, идентификатора и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="f4646-166">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="f4646-167">Обратитесь к [группа поддержки клиента Klue](mailto:support@klue.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f4646-167">Contact [Klue Client support team](mailto:support@klue.com) tooget these values.</span></span>

5. <span data-ttu-id="f4646-168">Hello Klue приложения ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="f4646-168">hello Klue application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="f4646-169">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="f4646-169">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="f4646-171">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна настройки атрибутов токена SAML, как показано в hello предшествующий образ и выполнить следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f4646-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="f4646-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="f4646-172">Attribute Name</span></span>      | <span data-ttu-id="f4646-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="f4646-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="f4646-174">first_name</span><span class="sxs-lookup"><span data-stu-id="f4646-174">first_name</span></span>          | <span data-ttu-id="f4646-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f4646-175">user.givenname</span></span> |
    | <span data-ttu-id="f4646-176">last_name</span><span class="sxs-lookup"><span data-stu-id="f4646-176">last_name</span></span>           | <span data-ttu-id="f4646-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="f4646-177">user.surname</span></span> |
    | <span data-ttu-id="f4646-178">email</span><span class="sxs-lookup"><span data-stu-id="f4646-178">email</span></span>               | <span data-ttu-id="f4646-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="f4646-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="f4646-180">а.</span><span class="sxs-lookup"><span data-stu-id="f4646-180">a.</span></span> <span data-ttu-id="f4646-181">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f4646-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f4646-184">b.</span><span class="sxs-lookup"><span data-stu-id="f4646-184">b.</span></span> <span data-ttu-id="f4646-185">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f4646-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="f4646-186">c.</span><span class="sxs-lookup"><span data-stu-id="f4646-186">c.</span></span> <span data-ttu-id="f4646-187">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f4646-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f4646-188">d.</span><span class="sxs-lookup"><span data-stu-id="f4646-188">d.</span></span> <span data-ttu-id="f4646-189">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f4646-189">Click **Ok**.</span></span>

7. <span data-ttu-id="f4646-190">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f4646-190">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="f4646-192">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f4646-192">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="f4646-194">На hello **конфигурации Klue** щелкните **Настройка Klue** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="f4646-194">On hello **Klue Configuration** section, click **Configure Klue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f4646-195">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="f4646-195">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="f4646-197">tooconfigure единого входа на **Klue** стороны, необходимо загрузить hello toosend **Certificate(Base64) SAML единого входа URL-адрес службы и идентификатор сущности SAML** слишком[Klue поддержки](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="f4646-197">tooconfigure single sign-on on **Klue** side, you need toosend hello downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** too[Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="f4646-198">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f4646-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f4646-199">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f4646-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f4646-200">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4646-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4646-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4646-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4646-202">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f4646-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f4646-204">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4646-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4646-205">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f4646-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4646-207">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f4646-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4646-209">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f4646-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4646-211">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f4646-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4646-213">а.</span><span class="sxs-lookup"><span data-stu-id="f4646-213">a.</span></span> <span data-ttu-id="f4646-214">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4646-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4646-215">b.</span><span class="sxs-lookup"><span data-stu-id="f4646-215">b.</span></span> <span data-ttu-id="f4646-216">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f4646-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4646-217">c.</span><span class="sxs-lookup"><span data-stu-id="f4646-217">c.</span></span> <span data-ttu-id="f4646-218">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f4646-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f4646-219">d.</span><span class="sxs-lookup"><span data-stu-id="f4646-219">d.</span></span> <span data-ttu-id="f4646-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f4646-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="f4646-221">Создание тестового пользователя Klue</span><span class="sxs-lookup"><span data-stu-id="f4646-221">Creating a Klue test user</span></span>

<span data-ttu-id="f4646-222">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Klue.</span><span class="sxs-lookup"><span data-stu-id="f4646-222">hello objective of this section is toocreate a user called Britta Simon in Klue.</span></span> <span data-ttu-id="f4646-223">Приложение Klue поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f4646-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f4646-224">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="f4646-224">There is no action item for you in this section.</span></span> <span data-ttu-id="f4646-225">Новый пользователь создается во время попытки tooaccess Klue, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="f4646-225">A new user is created during an attempt tooaccess Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="f4646-226">При необходимости пользователь вручную, обратитесь к toocreate [Klue поддержки](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="f4646-226">If you need toocreate a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f4646-227">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f4646-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f4646-228">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooKlue доступа.</span><span class="sxs-lookup"><span data-stu-id="f4646-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKlue.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f4646-230">**tooassign tooKlue Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f4646-230">**tooassign Britta Simon tooKlue, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4646-231">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f4646-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f4646-233">В списке приложений hello выберите **Klue**.</span><span class="sxs-lookup"><span data-stu-id="f4646-233">In hello applications list, select **Klue**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="f4646-235">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f4646-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f4646-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f4646-237">Click **Add** button.</span></span> <span data-ttu-id="f4646-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f4646-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f4646-240">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f4646-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f4646-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f4646-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4646-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f4646-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f4646-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f4646-243">Testing single sign-on</span></span>

<span data-ttu-id="f4646-244">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f4646-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f4646-245">При нажатии кнопки hello Klue плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Klue приложения.</span><span class="sxs-lookup"><span data-stu-id="f4646-245">When you click hello Klue tile in hello Access Panel, you should get automatically signed-on tooyour Klue application.</span></span>
<span data-ttu-id="f4646-246">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4646-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f4646-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f4646-247">Additional resources</span></span>

* [<span data-ttu-id="f4646-248">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4646-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4646-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4646-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

