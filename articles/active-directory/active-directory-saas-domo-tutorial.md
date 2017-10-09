---
title: "Учебник. Интеграция Azure Active Directory с Domo | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Domo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: cc70f8e5013f864d275762bbc1f84bd9677e8c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="dbcc6-103">Учебник. Интеграция Azure Active Directory с Domo</span><span class="sxs-lookup"><span data-stu-id="dbcc6-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="dbcc6-104">В этом учебнике вы узнаете, как toointegrate Domo с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dbcc6-104">In this tutorial, you learn how toointegrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dbcc6-105">Интеграция с Azure AD Domo предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-105">Integrating Domo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dbcc6-106">Можно управлять в Azure AD, имеющего доступ tooDomo</span><span class="sxs-lookup"><span data-stu-id="dbcc6-106">You can control in Azure AD who has access tooDomo</span></span>
- <span data-ttu-id="dbcc6-107">Можно включить на пользователей tooautomatically get вошедшего tooDomo (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbcc6-107">You can enable your users tooautomatically get signed-on tooDomo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dbcc6-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="dbcc6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dbcc6-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dbcc6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbcc6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dbcc6-110">Prerequisites</span></span>

<span data-ttu-id="dbcc6-111">tooconfigure интеграция Azure AD с Domo требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-111">tooconfigure Azure AD integration with Domo, you need hello following items:</span></span>

- <span data-ttu-id="dbcc6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dbcc6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dbcc6-113">подписка Domo с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dbcc6-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dbcc6-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dbcc6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dbcc6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbcc6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dbcc6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dbcc6-118">Scenario description</span></span>
<span data-ttu-id="dbcc6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dbcc6-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dbcc6-121">Добавление Domo из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dbcc6-121">Adding Domo from hello gallery</span></span>
2. <span data-ttu-id="dbcc6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbcc6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-hello-gallery"></a><span data-ttu-id="dbcc6-123">Добавление Domo из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dbcc6-123">Adding Domo from hello gallery</span></span>
<span data-ttu-id="dbcc6-124">tooconfigure hello интеграции Domo в Azure AD, вы должны tooadd Domo из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-124">tooconfigure hello integration of Domo into Azure AD, you need tooadd Domo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dbcc6-125">**tooadd Domo из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dbcc6-125">**tooadd Domo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbcc6-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dbcc6-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dbcc6-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dbcc6-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dbcc6-133">Введите в поле поиска hello **Domo**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-133">In hello search box, type **Domo**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="dbcc6-135">В панели результатов hello выберите **Domo**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-135">In hello results panel, select **Domo**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dbcc6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbcc6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dbcc6-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Domo с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dbcc6-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Domo является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Domo is tooa user in Azure AD.</span></span> <span data-ttu-id="dbcc6-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Domo должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-140">In other words, a link relationship between an Azure AD user and hello related user in Domo needs toobe established.</span></span>

<span data-ttu-id="dbcc6-141">В Domo, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-141">In Domo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dbcc6-142">tooconfigure и теста Azure AD единого входа с Domo, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-142">tooconfigure and test Azure AD single sign-on with Domo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dbcc6-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dbcc6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dbcc6-145">**[Создание тестового пользователя Domo](#creating-a-domo-test-user)**  -toohave аналог Саймон Britta в Domo, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - toohave a counterpart of Britta Simon in Domo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dbcc6-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dbcc6-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dbcc6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbcc6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dbcc6-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Domo.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="dbcc6-150">**tooconfigure Azure AD единого входа с Domo, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dbcc6-150">**tooconfigure Azure AD single sign-on with Domo, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbcc6-151">В hello в hello портала Azure **Domo** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-151">In hello Azure portal, on hello **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dbcc6-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="dbcc6-155">На hello **URL-адреса и домена Domo** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-155">On hello **Domo Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="dbcc6-157">а.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-157">a.</span></span> <span data-ttu-id="dbcc6-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="dbcc6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="dbcc6-159">b.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-159">b.</span></span> <span data-ttu-id="dbcc6-160">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="dbcc6-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-161">These values are not real.</span></span> <span data-ttu-id="dbcc6-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dbcc6-163">Обратитесь к [группа поддержки клиента Domo](mailto:support@domo.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-163">Contact [Domo Client support team](mailto:support@domo.com) tooget these values.</span></span>

4. <span data-ttu-id="dbcc6-164">Domo приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-164">Domo application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="dbcc6-165">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="dbcc6-166">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="dbcc6-167">Следующий снимок экрана приветствия показан пример для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-167">hello following screenshot shows an example for this configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="dbcc6-169">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="dbcc6-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="dbcc6-170">Attribute Name</span></span> | <span data-ttu-id="dbcc6-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="dbcc6-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="dbcc6-172">name</span><span class="sxs-lookup"><span data-stu-id="dbcc6-172">name</span></span> | <span data-ttu-id="dbcc6-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="dbcc6-173">user.displayname</span></span> |
    | <span data-ttu-id="dbcc6-174">email</span><span class="sxs-lookup"><span data-stu-id="dbcc6-174">email</span></span> | <span data-ttu-id="dbcc6-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="dbcc6-175">user.mail</span></span> |
    
    <span data-ttu-id="dbcc6-176">а.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-176">a.</span></span> <span data-ttu-id="dbcc6-177">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="dbcc6-180">b.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-180">b.</span></span> <span data-ttu-id="dbcc6-181">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="dbcc6-182">c.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-182">c.</span></span> <span data-ttu-id="dbcc6-183">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="dbcc6-184">d.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-184">d.</span></span> <span data-ttu-id="dbcc6-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="dbcc6-186">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-186">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="dbcc6-188">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dbcc6-188">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="dbcc6-190">На hello **конфигурации Domo** щелкните **Настройка Domo** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-190">On hello **Domo Configuration** section, click **Configure Domo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dbcc6-191">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="dbcc6-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

   ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="dbcc6-193">tooconfigure единого входа на **Domo** стороны, необходимо загрузить hello toosend **сертификат**, **идентификатор сущности SAML**, hello **SAML единого входа службы URL-адрес** и hello **URL-адрес выхода** слишком[Domo поддержки](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="dbcc6-193">tooconfigure single sign-on on **Domo** side, you need toosend hello downloaded **Certificate**, **SAML Entity ID**, hello **SAML Single Sign-On Service URL** and hello **Sign-Out URL** too[Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="dbcc6-194">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-194">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="dbcc6-195">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="dbcc6-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dbcc6-196">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dbcc6-197">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dbcc6-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dbcc6-198">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbcc6-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="dbcc6-199">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dbcc6-201">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dbcc6-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbcc6-202">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dbcc6-204">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dbcc6-206">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="dbcc6-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dbcc6-208">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dbcc6-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dbcc6-210">а.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-210">a.</span></span> <span data-ttu-id="dbcc6-211">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dbcc6-212">b.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-212">b.</span></span> <span data-ttu-id="dbcc6-213">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dbcc6-214">c.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-214">c.</span></span> <span data-ttu-id="dbcc6-215">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dbcc6-216">d.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-216">d.</span></span> <span data-ttu-id="dbcc6-217">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="dbcc6-218">Создание тестового пользователя приложения Domo</span><span class="sxs-lookup"><span data-stu-id="dbcc6-218">Creating a Domo test user</span></span>

<span data-ttu-id="dbcc6-219">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Domo.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-219">hello objective of this section is toocreate a user called Britta Simon in Domo.</span></span> <span data-ttu-id="dbcc6-220">Приложение Domo поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="dbcc6-221">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-221">There is no action item for you in this section.</span></span> <span data-ttu-id="dbcc6-222">Новый пользователь создается во время попытки tooaccess Domo, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-222">A new user is created during an attempt tooaccess Domo if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dbcc6-223">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="dbcc6-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dbcc6-224">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooDomo доступа.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDomo.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dbcc6-226">**tooassign tooDomo Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dbcc6-226">**tooassign Britta Simon tooDomo, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbcc6-227">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dbcc6-229">В списке приложений hello выберите **Domo**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-229">In hello applications list, select **Domo**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="dbcc6-231">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dbcc6-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-233">Click **Add** button.</span></span> <span data-ttu-id="dbcc6-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dbcc6-236">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dbcc6-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dbcc6-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dbcc6-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dbcc6-239">Testing single sign-on</span></span>

<span data-ttu-id="dbcc6-240">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="dbcc6-241">При нажатии кнопки hello Domo плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Domo приложения.</span><span class="sxs-lookup"><span data-stu-id="dbcc6-241">When you click hello Domo tile in hello Access Panel, you should get automatically signed-on tooyour Domo application.</span></span>

<span data-ttu-id="dbcc6-242">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dbcc6-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dbcc6-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dbcc6-243">Additional resources</span></span>

* [<span data-ttu-id="dbcc6-244">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbcc6-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dbcc6-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dbcc6-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

