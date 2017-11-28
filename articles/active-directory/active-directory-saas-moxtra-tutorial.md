---
title: "Руководство по интеграции Azure Active Directory с Moxtra | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="ebf52-103">Учебник. Интеграция Azure Active Directory с Moxtra</span><span class="sxs-lookup"><span data-stu-id="ebf52-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="ebf52-104">В этом учебнике вы узнаете, как toointegrate Moxtra с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ebf52-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ebf52-105">Интеграция с Azure AD Moxtra предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ebf52-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ebf52-106">Можно управлять в Azure AD, имеющего доступ tooMoxtra</span><span class="sxs-lookup"><span data-stu-id="ebf52-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="ebf52-107">Можно включить на пользователей tooautomatically get вошедшего tooMoxtra (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf52-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ebf52-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ebf52-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ebf52-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ebf52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebf52-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ebf52-110">Prerequisites</span></span>

<span data-ttu-id="ebf52-111">tooconfigure интеграция Azure AD с Moxtra требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ebf52-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="ebf52-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ebf52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ebf52-113">подписка Moxtra с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ebf52-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ebf52-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ebf52-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ebf52-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ebf52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ebf52-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ebf52-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ebf52-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ebf52-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ebf52-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ebf52-118">Scenario description</span></span>
<span data-ttu-id="ebf52-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ebf52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ebf52-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ebf52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ebf52-121">Добавление Moxtra из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ebf52-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="ebf52-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="ebf52-123">Добавление Moxtra из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ebf52-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="ebf52-124">tooconfigure hello интеграции Moxtra в Azure AD, вы должны tooadd Moxtra из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ebf52-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ebf52-125">**tooadd Moxtra из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebf52-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf52-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ebf52-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ebf52-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ebf52-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ebf52-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ebf52-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ebf52-133">Введите в поле поиска hello **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-133">In hello search box, type **Moxtra**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="ebf52-135">В панели результатов hello выберите **Moxtra**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ebf52-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ebf52-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf52-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ebf52-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение Moxtra с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ebf52-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ebf52-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Moxtra является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebf52-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="ebf52-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Moxtra должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ebf52-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="ebf52-141">В Moxtra, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ebf52-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ebf52-142">tooconfigure и теста Azure AD единого входа с Moxtra, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ebf52-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ebf52-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ebf52-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ebf52-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ebf52-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ebf52-145">**[Создание тестового пользователя Moxtra](#creating-a-moxtra-test-user)**  -toohave аналог Саймон Britta в Moxtra, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ebf52-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ebf52-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ebf52-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ebf52-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ebf52-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ebf52-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf52-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ebf52-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ebf52-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="ebf52-150">**Azure AD tooconfigure единого входа с Moxtra, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebf52-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf52-151">В hello в hello портала Azure **Moxtra** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ebf52-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ebf52-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="ebf52-155">На hello **URL-адреса и домена Moxtra** выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="ebf52-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="ebf52-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="ebf52-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="ebf52-158">Moxtra приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="ebf52-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ebf52-159">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ebf52-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="ebf52-160">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="ebf52-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ebf52-161">Следующий снимок экрана приветствия показан пример для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ebf52-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="ebf52-163">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ebf52-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="ebf52-164">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="ebf52-164">Attribute Name</span></span> | <span data-ttu-id="ebf52-165">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="ebf52-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ebf52-166">firstname</span><span class="sxs-lookup"><span data-stu-id="ebf52-166">firstname</span></span> | <span data-ttu-id="ebf52-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ebf52-167">user.givenname</span></span> |
    | <span data-ttu-id="ebf52-168">lastname</span><span class="sxs-lookup"><span data-stu-id="ebf52-168">lastname</span></span> | <span data-ttu-id="ebf52-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="ebf52-169">user.surname</span></span> |
    | <span data-ttu-id="ebf52-170">idpid</span><span class="sxs-lookup"><span data-stu-id="ebf52-170">idpid</span></span>    | <span data-ttu-id="ebf52-171">< идентификатор сущности SAML ></span><span class="sxs-lookup"><span data-stu-id="ebf52-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="ebf52-172">Здравствуйте, значение **idpid** атрибут не является реальным.</span><span class="sxs-lookup"><span data-stu-id="ebf52-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="ebf52-173">Можно получить фактическое значение hello из **краткий справочник** раздела **Moxtra конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="ebf52-174">а.</span><span class="sxs-lookup"><span data-stu-id="ebf52-174">a.</span></span> <span data-ttu-id="ebf52-175">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ebf52-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="ebf52-177">b.</span><span class="sxs-lookup"><span data-stu-id="ebf52-177">b.</span></span> <span data-ttu-id="ebf52-178">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ebf52-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ebf52-180">c.</span><span class="sxs-lookup"><span data-stu-id="ebf52-180">c.</span></span> <span data-ttu-id="ebf52-181">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ebf52-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="ebf52-182">d.</span><span class="sxs-lookup"><span data-stu-id="ebf52-182">d.</span></span> <span data-ttu-id="ebf52-183">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="ebf52-184">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ebf52-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="ebf52-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ebf52-186">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ebf52-188">На hello **конфигурации Moxtra** щелкните **Настройка Moxtra** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ebf52-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ebf52-189">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ebf52-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="ebf52-191">В другом окне браузера Войдите на сайт компании Moxtra tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ebf52-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="ebf52-192">Щелкните hello панели инструментов слева hello **консоли администрирования > SAML Single Sign-on**и нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="ebf52-194">На hello **SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ebf52-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="ebf52-196">а.</span><span class="sxs-lookup"><span data-stu-id="ebf52-196">a.</span></span> <span data-ttu-id="ebf52-197">В hello **имя** текстовом поле введите имя для конфигурации (например: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="ebf52-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="ebf52-198">b.</span><span class="sxs-lookup"><span data-stu-id="ebf52-198">b.</span></span> <span data-ttu-id="ebf52-199">В hello **идентификатор сущности поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf52-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ebf52-200">c.</span><span class="sxs-lookup"><span data-stu-id="ebf52-200">c.</span></span> <span data-ttu-id="ebf52-201">В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf52-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ebf52-202">d.</span><span class="sxs-lookup"><span data-stu-id="ebf52-202">d.</span></span> <span data-ttu-id="ebf52-203">В hello **AuthnContextClassRef** введите **urn: oasis: имена: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="ebf52-204">д.</span><span class="sxs-lookup"><span data-stu-id="ebf52-204">e.</span></span> <span data-ttu-id="ebf52-205">В hello **формата идентификатора имени** введите **urn: oasis: имена: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="ebf52-206">f.</span><span class="sxs-lookup"><span data-stu-id="ebf52-206">f.</span></span> <span data-ttu-id="ebf52-207">Откройте сертификат, который вы скачали из портала Azure в блокноте, скопируйте содержимое hello и вставьте его в hello **сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ebf52-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="ebf52-208">ж.</span><span class="sxs-lookup"><span data-stu-id="ebf52-208">g.</span></span> <span data-ttu-id="ebf52-209">Hello SAML электронной почты домена введите в текстовое поле почтового домена SAML.</span><span class="sxs-lookup"><span data-stu-id="ebf52-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="ebf52-210">toosee hello действия tooverify hello домена щелкните hello»**я**» ниже.</span><span class="sxs-lookup"><span data-stu-id="ebf52-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="ebf52-211">h.</span><span class="sxs-lookup"><span data-stu-id="ebf52-211">h.</span></span> <span data-ttu-id="ebf52-212">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="ebf52-213">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ebf52-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ebf52-214">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ebf52-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ebf52-215">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ebf52-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ebf52-216">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf52-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="ebf52-217">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf52-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ebf52-219">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebf52-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf52-220">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ebf52-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ebf52-222">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ebf52-224">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ebf52-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ebf52-226">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ebf52-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ebf52-228">а.</span><span class="sxs-lookup"><span data-stu-id="ebf52-228">a.</span></span> <span data-ttu-id="ebf52-229">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ebf52-230">b.</span><span class="sxs-lookup"><span data-stu-id="ebf52-230">b.</span></span> <span data-ttu-id="ebf52-231">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ebf52-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ebf52-232">c.</span><span class="sxs-lookup"><span data-stu-id="ebf52-232">c.</span></span> <span data-ttu-id="ebf52-233">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ebf52-234">d.</span><span class="sxs-lookup"><span data-stu-id="ebf52-234">d.</span></span> <span data-ttu-id="ebf52-235">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="ebf52-236">Создание тестового пользователя Moxtra</span><span class="sxs-lookup"><span data-stu-id="ebf52-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="ebf52-237">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ebf52-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="ebf52-238">**toocreate пользователя с именем Саймон Britta в Moxtra, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebf52-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf52-239">Войдите на tooyour Moxtra корпоративный сайт с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ebf52-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="ebf52-240">Щелкните hello панели инструментов слева hello **консоли администрирования > Управление пользователями**, а затем **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="ebf52-242">На hello **добавить пользователя** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ebf52-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="ebf52-243">а.</span><span class="sxs-lookup"><span data-stu-id="ebf52-243">a.</span></span> <span data-ttu-id="ebf52-244">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="ebf52-245">b.</span><span class="sxs-lookup"><span data-stu-id="ebf52-245">b.</span></span> <span data-ttu-id="ebf52-246">В hello **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="ebf52-247">c.</span><span class="sxs-lookup"><span data-stu-id="ebf52-247">c.</span></span> <span data-ttu-id="ebf52-248">В hello **электронной почты** введите совпадает с адресом электронной почты Britta в портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ebf52-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="ebf52-249">d.</span><span class="sxs-lookup"><span data-stu-id="ebf52-249">d.</span></span> <span data-ttu-id="ebf52-250">В hello **деления** введите **разработки**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="ebf52-251">д.</span><span class="sxs-lookup"><span data-stu-id="ebf52-251">e.</span></span> <span data-ttu-id="ebf52-252">В hello **отдел** введите **ИТ**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="ebf52-253">f.</span><span class="sxs-lookup"><span data-stu-id="ebf52-253">f.</span></span> <span data-ttu-id="ebf52-254">Выберите **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="ebf52-255">ж.</span><span class="sxs-lookup"><span data-stu-id="ebf52-255">g.</span></span> <span data-ttu-id="ebf52-256">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ebf52-257">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ebf52-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ebf52-258">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooMoxtra доступа.</span><span class="sxs-lookup"><span data-stu-id="ebf52-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ebf52-260">**tooassign tooMoxtra Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ebf52-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf52-261">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ebf52-263">В списке приложений hello выберите **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-263">In hello applications list, select **Moxtra**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="ebf52-265">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ebf52-267">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-267">Click **Add** button.</span></span> <span data-ttu-id="ebf52-268">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ebf52-270">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ebf52-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ebf52-271">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ebf52-272">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ebf52-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ebf52-273">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ebf52-273">Testing single sign-on</span></span>

<span data-ttu-id="ebf52-274">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ebf52-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ebf52-275">При нажатии кнопки hello Moxtra плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Moxtra приложения.</span><span class="sxs-lookup"><span data-stu-id="ebf52-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="ebf52-276">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ebf52-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ebf52-277">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ebf52-277">Additional resources</span></span>

* [<span data-ttu-id="ebf52-278">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebf52-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebf52-279">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ebf52-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

