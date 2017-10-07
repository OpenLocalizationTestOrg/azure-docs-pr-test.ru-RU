---
title: "Учебник. Интеграция Azure Active Directory с Clever | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="b9b87-103">Руководство. Интеграция Azure Active Directory с Clever</span><span class="sxs-lookup"><span data-stu-id="b9b87-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="b9b87-104">В этом учебнике вы узнаете, как toointegrate Clever с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9b87-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9b87-105">Интеграция с Azure AD Clever предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b9b87-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9b87-106">Можно управлять в Azure AD, имеющего доступ tooClever.</span><span class="sxs-lookup"><span data-stu-id="b9b87-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="b9b87-107">Можно включить на пользователей tooautomatically get вошедшего tooClever (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9b87-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b9b87-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b9b87-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b9b87-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9b87-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9b87-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b9b87-110">Prerequisites</span></span>

<span data-ttu-id="b9b87-111">tooconfigure интеграция Azure AD с Clever требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b9b87-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="b9b87-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b9b87-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9b87-113">подписка Clever с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9b87-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9b87-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b9b87-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9b87-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b9b87-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9b87-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b9b87-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9b87-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9b87-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9b87-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b9b87-118">Scenario description</span></span>
<span data-ttu-id="b9b87-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b9b87-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9b87-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b9b87-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9b87-121">Добавление Clever из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b9b87-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="b9b87-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9b87-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="b9b87-123">Добавление Clever из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b9b87-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="b9b87-124">tooconfigure hello интеграции Clever в Azure AD, вы должны tooadd Clever из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b9b87-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9b87-125">**tooadd Clever из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9b87-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9b87-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b9b87-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="b9b87-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9b87-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="b9b87-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b9b87-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="b9b87-133">Введите в поле поиска hello **Clever**выберите **Clever** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b9b87-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![В списке результатов hello некий](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b9b87-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9b87-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b9b87-136">В этом разделе описана настройка и проверка единого входа Azure AD в Clever с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9b87-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9b87-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Clever является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9b87-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="b9b87-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Clever должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b9b87-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="b9b87-139">В Clever, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b9b87-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9b87-140">tooconfigure и теста Azure AD единого входа с Clever, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b9b87-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9b87-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b9b87-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9b87-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b9b87-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9b87-143">**[Создание некий тестового пользователя](#create-a-clever-test-user)**  -toohave аналог Саймон Britta в Clever, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b9b87-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9b87-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b9b87-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9b87-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b9b87-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b9b87-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9b87-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b9b87-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении некий.</span><span class="sxs-lookup"><span data-stu-id="b9b87-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="b9b87-148">**tooconfigure Azure AD единого входа с Clever, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9b87-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9b87-149">В hello в hello портала Azure **Clever** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="b9b87-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9b87-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="b9b87-153">На hello **URL-адреса и домена некий** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9b87-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="b9b87-155">а.</span><span class="sxs-lookup"><span data-stu-id="b9b87-155">a.</span></span> <span data-ttu-id="b9b87-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="b9b87-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="b9b87-157">b.</span><span class="sxs-lookup"><span data-stu-id="b9b87-157">b.</span></span> <span data-ttu-id="b9b87-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="b9b87-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9b87-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b9b87-159">These values are not real.</span></span> <span data-ttu-id="b9b87-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b9b87-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b9b87-161">Обратитесь к [группа поддержки некий клиента](https://clever.com/about/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b9b87-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="b9b87-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b9b87-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="b9b87-164">Hello некий приложения ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена SAML** конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b9b87-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="b9b87-165">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="b9b87-165">hello following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="b9b87-167">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="b9b87-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="b9b87-168">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="b9b87-168">Attribute Name</span></span>  | <span data-ttu-id="b9b87-169">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="b9b87-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="b9b87-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="b9b87-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="b9b87-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="b9b87-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="b9b87-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="b9b87-172">Firstname</span></span>  | <span data-ttu-id="b9b87-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b9b87-173">user.givenname</span></span> |
    | <span data-ttu-id="b9b87-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="b9b87-174">Lastname</span></span>  | <span data-ttu-id="b9b87-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="b9b87-175">user.surname</span></span> |    

    <span data-ttu-id="b9b87-176">а.</span><span class="sxs-lookup"><span data-stu-id="b9b87-176">a.</span></span> <span data-ttu-id="b9b87-177">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b9b87-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b9b87-180">b.</span><span class="sxs-lookup"><span data-stu-id="b9b87-180">b.</span></span> <span data-ttu-id="b9b87-181">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b9b87-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="b9b87-182">c.</span><span class="sxs-lookup"><span data-stu-id="b9b87-182">c.</span></span> <span data-ttu-id="b9b87-183">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b9b87-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="b9b87-184">d.</span><span class="sxs-lookup"><span data-stu-id="b9b87-184">d.</span></span> <span data-ttu-id="b9b87-185">Оставьте hello **имен** пустое текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="b9b87-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="b9b87-186">d.</span><span class="sxs-lookup"><span data-stu-id="b9b87-186">d.</span></span> <span data-ttu-id="b9b87-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="b9b87-188">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b9b87-188">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b9b87-190">toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9b87-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="b9b87-191">а.</span><span class="sxs-lookup"><span data-stu-id="b9b87-191">a.</span></span> <span data-ttu-id="b9b87-192">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-192">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="b9b87-194">b.</span><span class="sxs-lookup"><span data-stu-id="b9b87-194">b.</span></span> <span data-ttu-id="b9b87-195">Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b9b87-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="b9b87-197">c.</span><span class="sxs-lookup"><span data-stu-id="b9b87-197">c.</span></span> <span data-ttu-id="b9b87-198">Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="b9b87-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="b9b87-200">d.</span><span class="sxs-lookup"><span data-stu-id="b9b87-200">d.</span></span> <span data-ttu-id="b9b87-201">Теперь перейдите на странице свойств toohello **Clever** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="b9b87-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="b9b87-203">д.</span><span class="sxs-lookup"><span data-stu-id="b9b87-203">e.</span></span> <span data-ttu-id="b9b87-204">Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="b9b87-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="b9b87-205">В другом окне браузера войдите в tooyour некий корпоративный сайт в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b9b87-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="b9b87-206">Щелкните hello панели инструментов **мгновенный вход**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="b9b87-207">![Мгновенный вход](./media/active-directory-saas-clever-tutorial/ic798984.png "Мгновенный вход")</span><span class="sxs-lookup"><span data-stu-id="b9b87-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="b9b87-208">На hello **мгновенный вход** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9b87-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="b9b87-209">![Мгновенный вход](./media/active-directory-saas-clever-tutorial/ic798985.png "Мгновенный вход")</span><span class="sxs-lookup"><span data-stu-id="b9b87-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="b9b87-210">а.</span><span class="sxs-lookup"><span data-stu-id="b9b87-210">a.</span></span> <span data-ttu-id="b9b87-211">Тип hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="b9b87-212">Hello **URL-адрес входа** является пользовательским значением.</span><span class="sxs-lookup"><span data-stu-id="b9b87-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="b9b87-213">Обратитесь к [группа поддержки некий клиента](https://clever.com/about/contact/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="b9b87-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="b9b87-214">b.</span><span class="sxs-lookup"><span data-stu-id="b9b87-214">b.</span></span> <span data-ttu-id="b9b87-215">Для параметра **Identity System** (Система идентификации) выберите значение **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="b9b87-216">c.</span><span class="sxs-lookup"><span data-stu-id="b9b87-216">c.</span></span> <span data-ttu-id="b9b87-217">Тип hello **URL-адрес метаданных** в hello **URL-адрес метаданных** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b9b87-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="b9b87-218">d.</span><span class="sxs-lookup"><span data-stu-id="b9b87-218">d.</span></span> <span data-ttu-id="b9b87-219">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b9b87-220">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b9b87-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9b87-221">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b9b87-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9b87-222">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9b87-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b9b87-223">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9b87-223">Create an Azure AD test user</span></span>

<span data-ttu-id="b9b87-224">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b9b87-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="b9b87-226">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9b87-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9b87-227">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b9b87-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b9b87-229">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b9b87-231">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b9b87-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b9b87-233">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9b87-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b9b87-235">а.</span><span class="sxs-lookup"><span data-stu-id="b9b87-235">a.</span></span> <span data-ttu-id="b9b87-236">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9b87-237">b.</span><span class="sxs-lookup"><span data-stu-id="b9b87-237">b.</span></span> <span data-ttu-id="b9b87-238">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b9b87-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b9b87-239">c.</span><span class="sxs-lookup"><span data-stu-id="b9b87-239">c.</span></span> <span data-ttu-id="b9b87-240">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="b9b87-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b9b87-241">d.</span><span class="sxs-lookup"><span data-stu-id="b9b87-241">d.</span></span> <span data-ttu-id="b9b87-242">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="b9b87-243">Создание тестового пользователя Clever</span><span class="sxs-lookup"><span data-stu-id="b9b87-243">Create a Clever test user</span></span>

<span data-ttu-id="b9b87-244">Пользователи toolog tooenable Azure AD в tooClever, их необходимо подготовить в Clever.</span><span class="sxs-lookup"><span data-stu-id="b9b87-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="b9b87-245">В случае Clever, работать с [группа поддержки некий клиента](https://clever.com/about/contact/) для добавления пользователей hello hello некий платформы.</span><span class="sxs-lookup"><span data-stu-id="b9b87-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="b9b87-246">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="b9b87-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="b9b87-247">Можно использовать любые другие некий пользователя средства создания учетных записей или интерфейсы API, предоставляемые некий tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9b87-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b9b87-248">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b9b87-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b9b87-249">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooClever доступа.</span><span class="sxs-lookup"><span data-stu-id="b9b87-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="b9b87-251">**tooassign tooClever Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9b87-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9b87-252">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b9b87-254">В списке приложений hello выберите **Clever**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-254">In hello applications list, select **Clever**.</span></span>

    ![Hello Clever ссылку в списке приложений hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="b9b87-256">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="b9b87-258">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-258">Click **Add** button.</span></span> <span data-ttu-id="b9b87-259">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="b9b87-261">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b9b87-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9b87-262">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9b87-263">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b9b87-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b9b87-264">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b9b87-264">Test single sign-on</span></span>

<span data-ttu-id="b9b87-265">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b9b87-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b9b87-266">При нажатии кнопки hello некий плитки в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour некий приложения.</span><span class="sxs-lookup"><span data-stu-id="b9b87-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="b9b87-267">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9b87-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9b87-268">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b9b87-268">Additional resources</span></span>

* [<span data-ttu-id="b9b87-269">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9b87-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9b87-270">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9b87-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

