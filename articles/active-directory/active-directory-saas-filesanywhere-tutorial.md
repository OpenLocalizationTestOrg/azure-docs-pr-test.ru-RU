---
title: "Руководство по интеграции Azure Active Directory с FilesAnywhere | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="b48b9-103">Руководство по интеграции Azure Active Directory с FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="b48b9-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="b48b9-104">В этом учебнике вы узнаете, как toointegrate FilesAnywhere с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b48b9-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b48b9-105">Интеграция с Azure AD FilesAnywhere предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b48b9-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b48b9-106">Можно управлять в Azure AD, имеющего доступ tooFilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="b48b9-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="b48b9-107">Можно включить на пользователей tooautomatically get вошедшего tooFilesAnywhere (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b48b9-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b48b9-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="b48b9-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="b48b9-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b48b9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b48b9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b48b9-110">Prerequisites</span></span>

<span data-ttu-id="b48b9-111">tooconfigure интеграция Azure AD с FilesAnywhere требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b48b9-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="b48b9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b48b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b48b9-113">подписка FilesAnywhere с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b48b9-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="b48b9-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b48b9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="b48b9-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b48b9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b48b9-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="b48b9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b48b9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b48b9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b48b9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b48b9-118">Scenario description</span></span>
<span data-ttu-id="b48b9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b48b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b48b9-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b48b9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b48b9-121">Добавление FilesAnywhere из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b48b9-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="b48b9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b48b9-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="b48b9-123">Добавление FilesAnywhere из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b48b9-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="b48b9-124">tooconfigure hello интеграции FilesAnywhere в Azure AD, вы должны tooadd FilesAnywhere из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b48b9-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b48b9-125">**tooadd FilesAnywhere из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b48b9-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b48b9-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b48b9-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b48b9-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b48b9-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b48b9-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b48b9-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b48b9-133">Введите в поле поиска hello **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="b48b9-135">В панели результатов hello выберите **FilesAnywhere**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b48b9-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b48b9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b48b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b48b9-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение FilesAnywhere с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b48b9-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b48b9-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FilesAnywhere является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b48b9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="b48b9-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в FilesAnywhere должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b48b9-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="b48b9-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="b48b9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="b48b9-142">tooconfigure и теста Azure AD единого входа с FilesAnywhere, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b48b9-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b48b9-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b48b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b48b9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b48b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b48b9-145">**[Создание тестового пользователя FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave аналог Саймон Britta в FilesAnywhere, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="b48b9-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="b48b9-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b48b9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="b48b9-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b48b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b48b9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b48b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b48b9-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="b48b9-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="b48b9-150">**tooconfigure Azure AD единого входа с FilesAnywhere, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b48b9-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="b48b9-151">На портале управления Azure hello на hello **FilesAnywhere** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b48b9-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b48b9-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="b48b9-155">На hello **URL-адреса и домена FilesAnywhere** статьи, при желании tooconfigure приложения hello в **режиме, инициированный IDP**:</span><span class="sxs-lookup"><span data-stu-id="b48b9-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="b48b9-157">а.</span><span class="sxs-lookup"><span data-stu-id="b48b9-157">a.</span></span> <span data-ttu-id="b48b9-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="b48b9-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="b48b9-159">Обратите внимание, это значение hello **215** — **clientid** и указан для примера.</span><span class="sxs-lookup"><span data-stu-id="b48b9-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="b48b9-160">Требуется tooreplace его со значением фактических clientid hello.</span><span class="sxs-lookup"><span data-stu-id="b48b9-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="b48b9-161">На hello **URL-адреса и домена FilesAnywhere** статьи, при желании tooconfigure приложения hello в **режиме, инициируемая SP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b48b9-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="b48b9-163">а.</span><span class="sxs-lookup"><span data-stu-id="b48b9-163">a.</span></span> <span data-ttu-id="b48b9-164">Щелкните hello **Показывать дополнительные параметры URL-адреса** параметр</span><span class="sxs-lookup"><span data-stu-id="b48b9-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="b48b9-165">b.</span><span class="sxs-lookup"><span data-stu-id="b48b9-165">b.</span></span> <span data-ttu-id="b48b9-166">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="b48b9-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b48b9-167">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="b48b9-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="b48b9-168">У вас tooupdate эти значения с hello фактический на URL-адрес входа и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b48b9-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="b48b9-169">Обратитесь к [FilesAnywhere поддержки](mailto:support@FilesAnywhere.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b48b9-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="b48b9-170">Программное обеспечение FilesAnywhere приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="b48b9-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b48b9-171">Выполните настройку следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b48b9-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="b48b9-172">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="b48b9-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="b48b9-173">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="b48b9-173">hello following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="b48b9-175">Когда hello регистрирует пользователей с FilesAnywhere, они получают значение hello **clientid** атрибута из [FilesAnywhere команды](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="b48b9-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="b48b9-176">Атрибут «Идентификатор клиента» hello tooadd с hello уникальное значение, предоставляемые FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="b48b9-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="b48b9-177">Все указанные выше атрибуты являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="b48b9-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="b48b9-178">Обратите внимание, это значение hello **2331** из **clientid** лишь пример.</span><span class="sxs-lookup"><span data-stu-id="b48b9-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="b48b9-179">Необходимо получить фактическое значение tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="b48b9-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="b48b9-180">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="b48b9-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="b48b9-181">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="b48b9-181">Attribute Name</span></span> | <span data-ttu-id="b48b9-182">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="b48b9-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="b48b9-183">clientid</span><span class="sxs-lookup"><span data-stu-id="b48b9-183">clientid</span></span> | <span data-ttu-id="b48b9-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="b48b9-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="b48b9-185">а.</span><span class="sxs-lookup"><span data-stu-id="b48b9-185">a.</span></span> <span data-ttu-id="b48b9-186">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b48b9-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="b48b9-189">b.</span><span class="sxs-lookup"><span data-stu-id="b48b9-189">b.</span></span> <span data-ttu-id="b48b9-190">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b48b9-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b48b9-191">c.</span><span class="sxs-lookup"><span data-stu-id="b48b9-191">c.</span></span> <span data-ttu-id="b48b9-192">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b48b9-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b48b9-193">d.</span><span class="sxs-lookup"><span data-stu-id="b48b9-193">d.</span></span> <span data-ttu-id="b48b9-194">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-194">Click **Ok**</span></span>

7. <span data-ttu-id="b48b9-195">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b48b9-195">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b48b9-197">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b48b9-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="b48b9-199">На hello **конфигурации FilesAnywhere** щелкните **Настройка FilesAnywhere** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b48b9-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="b48b9-202">tooget единого входа: Завершение настройки приложения в конце FilesAnywhere контакт [FilesAnywhere поддержки](mailto:support@FilesAnywhere.com) и передавать их в маркер SAML загружаются hello подписи сертификата и единого входа (SSO) URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b48b9-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b48b9-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b48b9-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="b48b9-204">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b48b9-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b48b9-206">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b48b9-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b48b9-207">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b48b9-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b48b9-209">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="b48b9-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b48b9-211">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b48b9-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b48b9-213">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b48b9-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b48b9-215">а.</span><span class="sxs-lookup"><span data-stu-id="b48b9-215">a.</span></span> <span data-ttu-id="b48b9-216">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b48b9-217">b.</span><span class="sxs-lookup"><span data-stu-id="b48b9-217">b.</span></span> <span data-ttu-id="b48b9-218">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b48b9-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b48b9-219">c.</span><span class="sxs-lookup"><span data-stu-id="b48b9-219">c.</span></span> <span data-ttu-id="b48b9-220">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b48b9-221">d.</span><span class="sxs-lookup"><span data-stu-id="b48b9-221">d.</span></span> <span data-ttu-id="b48b9-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="b48b9-223">Создание тестового пользователя FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="b48b9-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="b48b9-224">В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение.</span><span class="sxs-lookup"><span data-stu-id="b48b9-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b48b9-225">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b48b9-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b48b9-226">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooFilesAnywhere доступа.</span><span class="sxs-lookup"><span data-stu-id="b48b9-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b48b9-228">**tooassign tooFilesAnywhere Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b48b9-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="b48b9-229">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b48b9-231">В списке приложений hello выберите **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="b48b9-233">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b48b9-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-235">Click **Add** button.</span></span> <span data-ttu-id="b48b9-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b48b9-238">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b48b9-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b48b9-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b48b9-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b48b9-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="b48b9-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b48b9-241">Testing single sign-on</span></span>

<span data-ttu-id="b48b9-242">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b48b9-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b48b9-243">При нажатии кнопки hello FilesAnywhere плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour FilesAnywhere приложения.</span><span class="sxs-lookup"><span data-stu-id="b48b9-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b48b9-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b48b9-244">Additional resources</span></span>

* [<span data-ttu-id="b48b9-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b48b9-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b48b9-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b48b9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
