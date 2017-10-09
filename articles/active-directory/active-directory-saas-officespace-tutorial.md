---
title: "Руководство по интеграции Azure Active Directory с OfficeSpace Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="231f3-103">Учебник. Интеграция Azure Active Directory с OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="231f3-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="231f3-104">В этом учебнике вы узнаете, как toointegrate OfficeSpace Software с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="231f3-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="231f3-105">Интеграция OfficeSpace Software с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="231f3-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="231f3-106">Можно управлять в Azure AD, имеющего доступ tooOfficeSpace программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="231f3-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="231f3-107">Можно включить на пользователей tooautomatically get вошедшего tooOfficeSpace программного обеспечения (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="231f3-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="231f3-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="231f3-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="231f3-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="231f3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="231f3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="231f3-110">Prerequisites</span></span>

<span data-ttu-id="231f3-111">tooconfigure интеграция Azure AD с OfficeSpace Software необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="231f3-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="231f3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="231f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="231f3-113">подписка OfficeSpace Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="231f3-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="231f3-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="231f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="231f3-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="231f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="231f3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="231f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="231f3-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="231f3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="231f3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="231f3-118">Scenario description</span></span>
<span data-ttu-id="231f3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="231f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="231f3-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="231f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="231f3-121">Добавление OfficeSpace Software из галереи hello</span><span class="sxs-lookup"><span data-stu-id="231f3-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="231f3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="231f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="231f3-123">Добавление OfficeSpace Software из галереи hello</span><span class="sxs-lookup"><span data-stu-id="231f3-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="231f3-124">tooconfigure hello интеграции OfficeSpace Software в Azure AD, вы должны tooadd OfficeSpace Software из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="231f3-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="231f3-125">**tooadd OfficeSpace Software из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="231f3-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="231f3-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="231f3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="231f3-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="231f3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="231f3-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="231f3-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="231f3-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="231f3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="231f3-133">Введите в поле поиска hello **OfficeSpace Software**выберите **OfficeSpace Software** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="231f3-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Список результатов OfficeSpace Software в hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="231f3-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="231f3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="231f3-136">В этом разделе описана настройка и проверка единого входа Azure AD в OfficeSpace Software с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="231f3-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="231f3-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в OfficeSpace Software является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="231f3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="231f3-138">Иными словами связи между пользователя Azure AD и связанных пользователей hello в OfficeSpace Software необходимо установить toobe.</span><span class="sxs-lookup"><span data-stu-id="231f3-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="231f3-139">В OfficeSpace Software, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="231f3-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="231f3-140">tooconfigure и теста Azure AD единого входа с OfficeSpace Software, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="231f3-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="231f3-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="231f3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="231f3-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="231f3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="231f3-143">**[Создание тестового пользователя OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave аналог Саймон Britta в OfficeSpace Software, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="231f3-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="231f3-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="231f3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="231f3-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="231f3-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="231f3-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="231f3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="231f3-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="231f3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="231f3-148">**tooconfigure Azure AD единого входа с OfficeSpace Software, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="231f3-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="231f3-149">В hello в hello портала Azure **OfficeSpace Software** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="231f3-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="231f3-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="231f3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="231f3-153">На hello **URL-адреса и домена программного обеспечения OfficeSpace** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="231f3-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="231f3-155">а.</span><span class="sxs-lookup"><span data-stu-id="231f3-155">a.</span></span> <span data-ttu-id="231f3-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="231f3-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="231f3-157">b.</span><span class="sxs-lookup"><span data-stu-id="231f3-157">b.</span></span> <span data-ttu-id="231f3-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="231f3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="231f3-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="231f3-159">These values are not real.</span></span> <span data-ttu-id="231f3-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="231f3-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="231f3-161">Обратитесь к [OfficeSpace клиентское программное обеспечение поддержки](mailto:support@officespacesoftware.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="231f3-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="231f3-162">Приложение OfficeSpace Software ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="231f3-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="231f3-163">Выполните настройку следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="231f3-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="231f3-164">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="231f3-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="231f3-165">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="231f3-165">hello following screenshot shows an example for this.</span></span>
    
    ![Настройка атрибута](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="231f3-167">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна выберите **user.mail** как **идентификатор пользователя** и для каждой строки показано в следующей таблице hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="231f3-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="231f3-168">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="231f3-168">Attribute Name</span></span> | <span data-ttu-id="231f3-169">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="231f3-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="231f3-170">email</span><span class="sxs-lookup"><span data-stu-id="231f3-170">email</span></span> | <span data-ttu-id="231f3-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="231f3-171">user.mail</span></span> |
    | <span data-ttu-id="231f3-172">name</span><span class="sxs-lookup"><span data-stu-id="231f3-172">name</span></span> | <span data-ttu-id="231f3-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="231f3-173">user.displayname</span></span> |
    | <span data-ttu-id="231f3-174">first_name</span><span class="sxs-lookup"><span data-stu-id="231f3-174">first_name</span></span> | <span data-ttu-id="231f3-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="231f3-175">user.givenname</span></span> |
    | <span data-ttu-id="231f3-176">last_name</span><span class="sxs-lookup"><span data-stu-id="231f3-176">last_name</span></span> | <span data-ttu-id="231f3-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="231f3-177">user.surname</span></span> |

    <span data-ttu-id="231f3-178">а.</span><span class="sxs-lookup"><span data-stu-id="231f3-178">a.</span></span> <span data-ttu-id="231f3-179">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="231f3-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="231f3-180">Настройка при добавлении</span><span class="sxs-lookup"><span data-stu-id="231f3-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Настройка атрибута](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="231f3-182">b.</span><span class="sxs-lookup"><span data-stu-id="231f3-182">b.</span></span> <span data-ttu-id="231f3-183">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="231f3-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="231f3-184">c.</span><span class="sxs-lookup"><span data-stu-id="231f3-184">c.</span></span> <span data-ttu-id="231f3-185">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="231f3-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="231f3-186">d.</span><span class="sxs-lookup"><span data-stu-id="231f3-186">d.</span></span> <span data-ttu-id="231f3-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="231f3-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="231f3-188">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="231f3-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="231f3-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="231f3-190">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="231f3-192">На hello **конфигурации программного обеспечения OfficeSpace** щелкните **Настройка OfficeSpace Software** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="231f3-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="231f3-193">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="231f3-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="231f3-195">В другом окне веб-браузера войдите в свой клиент OfficeSpace Software в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="231f3-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="231f3-196">Go слишком**параметры** и нажмите кнопку **соединители**.</span><span class="sxs-lookup"><span data-stu-id="231f3-196">Go too**Settings** and click **Connectors**.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="231f3-198">Щелкните **SAML Authentication** (Аутентификация SAML).</span><span class="sxs-lookup"><span data-stu-id="231f3-198">Click **SAML Authentication**.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="231f3-200">В hello **проверку подлинности SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="231f3-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="231f3-202">а.</span><span class="sxs-lookup"><span data-stu-id="231f3-202">a.</span></span> <span data-ttu-id="231f3-203">В hello **URL-адрес выхода поставщика** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="231f3-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="231f3-204">b.</span><span class="sxs-lookup"><span data-stu-id="231f3-204">b.</span></span> <span data-ttu-id="231f3-205">В hello **URL-адрес назначения idp клиента** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="231f3-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="231f3-206">c.</span><span class="sxs-lookup"><span data-stu-id="231f3-206">c.</span></span> <span data-ttu-id="231f3-207">Вставить hello **отпечаток** значение, которое было скопировано из портала Azure в hello **отпечаток сертификата IDP клиента** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="231f3-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="231f3-208">d.</span><span class="sxs-lookup"><span data-stu-id="231f3-208">d.</span></span> <span data-ttu-id="231f3-209">Нажмите кнопку **Сохранить параметры**.</span><span class="sxs-lookup"><span data-stu-id="231f3-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="231f3-210">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="231f3-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="231f3-211">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="231f3-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="231f3-212">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="231f3-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="231f3-213">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="231f3-213">Create an Azure AD test user</span></span>

<span data-ttu-id="231f3-214">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="231f3-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="231f3-216">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="231f3-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="231f3-217">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="231f3-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="231f3-219">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="231f3-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="231f3-221">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="231f3-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="231f3-223">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="231f3-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="231f3-225">а.</span><span class="sxs-lookup"><span data-stu-id="231f3-225">a.</span></span> <span data-ttu-id="231f3-226">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="231f3-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="231f3-227">b.</span><span class="sxs-lookup"><span data-stu-id="231f3-227">b.</span></span> <span data-ttu-id="231f3-228">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="231f3-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="231f3-229">c.</span><span class="sxs-lookup"><span data-stu-id="231f3-229">c.</span></span> <span data-ttu-id="231f3-230">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="231f3-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="231f3-231">d.</span><span class="sxs-lookup"><span data-stu-id="231f3-231">d.</span></span> <span data-ttu-id="231f3-232">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="231f3-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="231f3-233">Создание тестового пользователя OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="231f3-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="231f3-234">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="231f3-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="231f3-235">Приложение OfficeSpace Software поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="231f3-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="231f3-236">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="231f3-236">There is no action item for you in this section.</span></span> <span data-ttu-id="231f3-237">Новый пользователь создается во время попытки tooaccess OfficeSpace Software, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="231f3-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="231f3-238">Если требуется toocreate пользователя вручную, необходимо tooContact [OfficeSpace Software поддержки](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="231f3-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="231f3-239">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="231f3-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="231f3-240">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooOfficeSpace программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="231f3-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="231f3-242">**tooassign tooOfficeSpace Britta Simon программное обеспечение, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="231f3-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="231f3-243">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="231f3-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="231f3-245">В списке приложений hello выберите **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="231f3-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![Hello OfficeSpace Software ссылку в списке приложений hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="231f3-247">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="231f3-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="231f3-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="231f3-249">Click **Add** button.</span></span> <span data-ttu-id="231f3-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="231f3-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="231f3-252">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="231f3-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="231f3-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="231f3-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="231f3-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="231f3-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="231f3-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="231f3-255">Test single sign-on</span></span>

<span data-ttu-id="231f3-256">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="231f3-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="231f3-257">При нажатии кнопки OfficeSpace Software плитки в панели доступа hello hello, вы должны получить tooyour автоматически подписан в приложение OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="231f3-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="231f3-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="231f3-258">Additional resources</span></span>

* [<span data-ttu-id="231f3-259">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="231f3-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="231f3-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="231f3-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

