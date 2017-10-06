---
title: "Руководство по интеграции Azure Active Directory с Pluralsight | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8394eed79f21fb889816d8dafe2d71187be72b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="00961-103">Учебник. Интеграция Azure Active Directory с Pluralsight</span><span class="sxs-lookup"><span data-stu-id="00961-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="00961-104">В этом учебнике вы узнаете, как toointegrate Pluralsight с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="00961-104">In this tutorial, you learn how toointegrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00961-105">Интеграция с Azure AD Pluralsight предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="00961-105">Integrating Pluralsight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="00961-106">Можно управлять в Azure AD, имеющего доступ tooPluralsight</span><span class="sxs-lookup"><span data-stu-id="00961-106">You can control in Azure AD who has access tooPluralsight</span></span>
- <span data-ttu-id="00961-107">Можно включить на пользователей tooautomatically get вошедшего tooPluralsight (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="00961-107">You can enable your users tooautomatically get signed-on tooPluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="00961-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="00961-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="00961-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00961-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00961-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="00961-110">Prerequisites</span></span>

<span data-ttu-id="00961-111">tooconfigure интеграция Azure AD с Pluralsight требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="00961-111">tooconfigure Azure AD integration with Pluralsight, you need hello following items:</span></span>

- <span data-ttu-id="00961-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="00961-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00961-113">подписка Pluralsight с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="00961-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00961-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="00961-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00961-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="00961-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00961-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="00961-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00961-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00961-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00961-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="00961-118">Scenario description</span></span>
<span data-ttu-id="00961-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="00961-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00961-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="00961-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00961-121">Добавление Pluralsight из галереи hello</span><span class="sxs-lookup"><span data-stu-id="00961-121">Adding Pluralsight from hello gallery</span></span>
2. <span data-ttu-id="00961-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00961-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-hello-gallery"></a><span data-ttu-id="00961-123">Добавление Pluralsight из галереи hello</span><span class="sxs-lookup"><span data-stu-id="00961-123">Adding Pluralsight from hello gallery</span></span>
<span data-ttu-id="00961-124">tooconfigure hello интеграции Pluralsight в Azure AD, вы должны tooadd Pluralsight из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="00961-124">tooconfigure hello integration of Pluralsight into Azure AD, you need tooadd Pluralsight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="00961-125">**tooadd Pluralsight из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="00961-125">**tooadd Pluralsight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="00961-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="00961-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="00961-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="00961-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="00961-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00961-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="00961-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="00961-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="00961-133">Введите в поле поиска hello **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="00961-133">In hello search box, type **Pluralsight**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="00961-135">В панели результатов hello выберите **Pluralsight**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="00961-135">In hello results panel, select **Pluralsight**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="00961-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00961-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="00961-138">В этом разделе описана настройка и проверка единого входа Azure AD в Pluralsight с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00961-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="00961-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Pluralsight является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00961-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pluralsight is tooa user in Azure AD.</span></span> <span data-ttu-id="00961-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Pluralsight должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="00961-140">In other words, a link relationship between an Azure AD user and hello related user in Pluralsight needs toobe established.</span></span>

<span data-ttu-id="00961-141">В Pluralsight, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="00961-141">In Pluralsight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="00961-142">tooconfigure и теста Azure AD единого входа с Pluralsight, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="00961-142">tooconfigure and test Azure AD single sign-on with Pluralsight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="00961-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="00961-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="00961-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="00961-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00961-145">**[Создание тестового пользователя Pluralsight](#creating-a-pluralsight-test-user)**  -toohave аналог Саймон Britta в Pluralsight, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="00961-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - toohave a counterpart of Britta Simon in Pluralsight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="00961-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="00961-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00961-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="00961-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="00961-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00961-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="00961-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="00961-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="00961-150">**tooconfigure Azure AD единого входа с Pluralsight, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="00961-150">**tooconfigure Azure AD single sign-on with Pluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="00961-151">В hello в hello портала Azure **Pluralsight** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="00961-151">In hello Azure portal, on hello **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="00961-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="00961-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="00961-155">На hello **URL-адреса и домена Pluralsight** выполните hello следующее:</span><span class="sxs-lookup"><span data-stu-id="00961-155">On hello **Pluralsight Domain and URLs** section, perform hello following:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="00961-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="00961-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="00961-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="00961-158">This value is not real.</span></span> <span data-ttu-id="00961-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="00961-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="00961-160">Обратитесь к [группа поддержки клиента Pluralsight](mailto:support@pluralsight.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="00961-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="00961-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="00961-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="00961-163">Цель этого раздела Hello является tooenable Azure AD единым входом в портал Azure hello и tooconfigure единого входа в приложение hello Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="00961-163">hello objective of this section is tooenable Azure AD single sign-on in hello Azure portal and tooconfigure SSO in hello Pluralsight application.</span></span>

    <span data-ttu-id="00961-164">Hello Pluralsight приложения ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="00961-164">hello Pluralsight application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="00961-165">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="00961-165">hello following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="00961-167">Можно также добавить hello **«Уникальный идентификатор»** атрибута с hello соответствующее значение как EmployeeID, или что-нибудь другое которая подходит для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="00961-167">You can also add hello **"Unique ID"** attribute with hello appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="00961-168">Также Обратите внимание, что это не hello обязательный атрибут; Тем не менее, можно добавить его слишком идентификации уникального пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="00961-168">Also note that this is not hello required attribute; however, you can add it too identify hello unique user.</span></span> 

6. <span data-ttu-id="00961-169">требуется hello tooadd **атрибутов токена SAML**, для каждой строки, показано в следующей таблице hello, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="00961-169">tooadd hello required **SAML token attributes**, for each row shown in hello table below, perform hello following steps:</span></span>
   
   | <span data-ttu-id="00961-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="00961-170">Attribute Name</span></span> | <span data-ttu-id="00961-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="00961-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="00961-172">Имя</span><span class="sxs-lookup"><span data-stu-id="00961-172">First Name</span></span> |<span data-ttu-id="00961-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="00961-173">user.givenname</span></span> |
   | <span data-ttu-id="00961-174">Фамилия</span><span class="sxs-lookup"><span data-stu-id="00961-174">Last Name</span></span> |<span data-ttu-id="00961-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="00961-175">user.surname</span></span> |
   | <span data-ttu-id="00961-176">Email</span><span class="sxs-lookup"><span data-stu-id="00961-176">Email</span></span> |<span data-ttu-id="00961-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="00961-177">user.mail</span></span> |
   
   <span data-ttu-id="00961-178">а.</span><span class="sxs-lookup"><span data-stu-id="00961-178">a.</span></span> <span data-ttu-id="00961-179">Нажмите кнопку **добавить атрибут пользователя** tooopen hello **Attribure добавить пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="00961-179">Click **add user attribute** tooopen hello **Add User Attribure** dialog.</span></span>
    
     ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="00961-181">b.</span><span class="sxs-lookup"><span data-stu-id="00961-181">b.</span></span> <span data-ttu-id="00961-182">В hello **имя атрибута** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="00961-182">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
  
   <span data-ttu-id="00961-183">c.</span><span class="sxs-lookup"><span data-stu-id="00961-183">c.</span></span> <span data-ttu-id="00961-184">Из hello **значение атрибута** список, выберите hello значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="00961-184">From hello **Attribute Value** list, select hello attribute value shown for that row.</span></span>
  
   <span data-ttu-id="00961-185">d.</span><span class="sxs-lookup"><span data-stu-id="00961-185">d.</span></span> <span data-ttu-id="00961-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="00961-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="00961-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="00961-187">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="00961-189">tooget SSO настроен для вашего приложения, обратитесь в службу [служб Professional Pluralsight](mailTo:professionalservices@pluralsight.com) группы и предоставить hello скачанный файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="00961-189">tooget SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide hello downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="00961-190">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="00961-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="00961-191">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="00961-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="00961-192">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="00961-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="00961-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="00961-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="00961-194">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="00961-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="00961-196">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="00961-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="00961-197">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="00961-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00961-199">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="00961-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00961-201">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="00961-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00961-203">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="00961-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="00961-205">а.</span><span class="sxs-lookup"><span data-stu-id="00961-205">a.</span></span> <span data-ttu-id="00961-206">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="00961-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00961-207">b.</span><span class="sxs-lookup"><span data-stu-id="00961-207">b.</span></span> <span data-ttu-id="00961-208">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="00961-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="00961-209">c.</span><span class="sxs-lookup"><span data-stu-id="00961-209">c.</span></span> <span data-ttu-id="00961-210">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="00961-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="00961-211">d.</span><span class="sxs-lookup"><span data-stu-id="00961-211">d.</span></span> <span data-ttu-id="00961-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="00961-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="00961-213">Создание тестового пользователя Pluralsight</span><span class="sxs-lookup"><span data-stu-id="00961-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="00961-214">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="00961-214">hello objective of this section is toocreate a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="00961-215">Можно работать с [группа поддержки клиента Pluralsight](mailto:support@pluralsight.com) tooadd hello пользователей в учетной записи Pluralsight hello.</span><span class="sxs-lookup"><span data-stu-id="00961-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) tooadd hello users in hello Pluralsight account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="00961-216">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="00961-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="00961-217">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPluralsight доступа.</span><span class="sxs-lookup"><span data-stu-id="00961-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPluralsight.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="00961-219">**tooassign tooPluralsight Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="00961-219">**tooassign Britta Simon tooPluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="00961-220">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00961-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="00961-222">В списке приложений hello выберите **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="00961-222">In hello applications list, select **Pluralsight**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="00961-224">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="00961-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="00961-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00961-226">Click **Add** button.</span></span> <span data-ttu-id="00961-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="00961-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="00961-229">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="00961-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="00961-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="00961-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00961-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="00961-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="00961-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="00961-232">Testing single sign-on</span></span>

<span data-ttu-id="00961-233">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="00961-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="00961-234">При выборе плитки Pluralsight hello в hello панели доступа, следует получать автоматически вошедшего tooyour Pluralsight приложения.</span><span class="sxs-lookup"><span data-stu-id="00961-234">When you click hello Pluralsight tile in hello Access Panel, you should get automatically signed-on tooyour Pluralsight application.</span></span> <span data-ttu-id="00961-235">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00961-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="00961-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="00961-236">Additional resources</span></span>

* [<span data-ttu-id="00961-237">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00961-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00961-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="00961-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

