---
title: "Руководство по интеграции Azure Active Directory с Onit | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="84e0c-103">Учебник. Интеграция Azure Active Directory с Onit</span><span class="sxs-lookup"><span data-stu-id="84e0c-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="84e0c-104">В этом учебнике вы узнаете, как toointegrate Onit с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84e0c-104">In this tutorial, you learn how toointegrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84e0c-105">Интеграция Onit с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="84e0c-105">Integrating Onit with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="84e0c-106">Можно управлять в Azure AD, имеющего доступ tooOnit.</span><span class="sxs-lookup"><span data-stu-id="84e0c-106">You can control in Azure AD who has access tooOnit.</span></span>
- <span data-ttu-id="84e0c-107">Можно включить на пользователей tooautomatically get вошедшего tooOnit (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84e0c-107">You can enable your users tooautomatically get signed-on tooOnit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="84e0c-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="84e0c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="84e0c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84e0c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84e0c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84e0c-110">Prerequisites</span></span>

<span data-ttu-id="84e0c-111">tooconfigure интеграция Azure AD с Onit требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="84e0c-111">tooconfigure Azure AD integration with Onit, you need hello following items:</span></span>

- <span data-ttu-id="84e0c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="84e0c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84e0c-113">Подписка с поддержкой единого входа Onit.</span><span class="sxs-lookup"><span data-stu-id="84e0c-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84e0c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="84e0c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84e0c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="84e0c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84e0c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="84e0c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84e0c-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84e0c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84e0c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="84e0c-118">Scenario description</span></span>

<span data-ttu-id="84e0c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="84e0c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84e0c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="84e0c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84e0c-121">Добавление Onit из галереи hello</span><span class="sxs-lookup"><span data-stu-id="84e0c-121">Adding Onit from hello gallery</span></span>
2. <span data-ttu-id="84e0c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="84e0c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-hello-gallery"></a><span data-ttu-id="84e0c-123">Добавление Onit из галереи hello</span><span class="sxs-lookup"><span data-stu-id="84e0c-123">Adding Onit from hello gallery</span></span>
<span data-ttu-id="84e0c-124">tooconfigure hello интеграции Onit в Azure AD, вы должны tooadd Onit из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="84e0c-124">tooconfigure hello integration of Onit into Azure AD, you need tooadd Onit from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84e0c-125">**tooadd Onit из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84e0c-125">**tooadd Onit from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84e0c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="84e0c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="84e0c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="84e0c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="84e0c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="84e0c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="84e0c-133">Введите в поле поиска hello **Onit**выберите **Onit** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="84e0c-133">In hello search box, type **Onit**, select **Onit** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Onit в списке результатов hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="84e0c-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="84e0c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="84e0c-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Onit с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84e0c-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="84e0c-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Onit является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84e0c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Onit is tooa user in Azure AD.</span></span> <span data-ttu-id="84e0c-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Onit должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="84e0c-138">In other words, a link relationship between an Azure AD user and hello related user in Onit needs toobe established.</span></span>

<span data-ttu-id="84e0c-139">В Onit, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="84e0c-139">In Onit, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="84e0c-140">tooconfigure и теста Azure AD единого входа с Onit, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="84e0c-140">tooconfigure and test Azure AD single sign-on with Onit, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84e0c-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="84e0c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84e0c-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="84e0c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84e0c-143">**[Создание тестового пользователя, прошедшего Onit](#create-an-onit-test-user)**  -toohave аналог Саймон Britta в Onit, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="84e0c-143">**[Create an Onit test user](#create-an-onit-test-user)** - toohave a counterpart of Britta Simon in Onit that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="84e0c-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="84e0c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84e0c-145">**[Тестирование единого входа](#test-single-sign-on)**  tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="84e0c-145">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="84e0c-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="84e0c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="84e0c-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Onit.</span><span class="sxs-lookup"><span data-stu-id="84e0c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="84e0c-148">**tooconfigure Azure AD единого входа с Onit, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84e0c-148">**tooconfigure Azure AD single sign-on with Onit, perform hello following steps:**</span></span>

1. <span data-ttu-id="84e0c-149">В hello в hello портала Azure **Onit** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-149">In hello Azure portal, on hello **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="84e0c-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="84e0c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="84e0c-153">На hello **URL-адреса и домена Onit** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84e0c-153">On hello **Onit Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="84e0c-155">а.</span><span class="sxs-lookup"><span data-stu-id="84e0c-155">a.</span></span> <span data-ttu-id="84e0c-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="84e0c-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="84e0c-157">b.</span><span class="sxs-lookup"><span data-stu-id="84e0c-157">b.</span></span> <span data-ttu-id="84e0c-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="84e0c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84e0c-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="84e0c-159">These values are not real.</span></span> <span data-ttu-id="84e0c-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="84e0c-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="84e0c-161">Обратитесь к [группа поддержки клиента Onit](https://www.onit.com/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="84e0c-161">Contact [Onit Client support team](https://www.onit.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="84e0c-162">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="84e0c-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="84e0c-164">Приложение Onit ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="84e0c-164">Onit application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="84e0c-165">Выполните настройку следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="84e0c-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="84e0c-166">Вы можете управлять hello значения этих атрибутов из hello **«Атрибутов»** вкладку приложения hello.</span><span class="sxs-lookup"><span data-stu-id="84e0c-166">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="84e0c-167">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="84e0c-167">hello following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="84e0c-169">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84e0c-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="84e0c-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="84e0c-170">Attribute Name</span></span> | <span data-ttu-id="84e0c-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="84e0c-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="84e0c-172">email</span><span class="sxs-lookup"><span data-stu-id="84e0c-172">email</span></span> | <span data-ttu-id="84e0c-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="84e0c-173">user.mail</span></span> |
    
    <span data-ttu-id="84e0c-174">а.</span><span class="sxs-lookup"><span data-stu-id="84e0c-174">a.</span></span> <span data-ttu-id="84e0c-175">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="84e0c-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="84e0c-178">b.</span><span class="sxs-lookup"><span data-stu-id="84e0c-178">b.</span></span> <span data-ttu-id="84e0c-179">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="84e0c-179">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="84e0c-180">c.</span><span class="sxs-lookup"><span data-stu-id="84e0c-180">c.</span></span> <span data-ttu-id="84e0c-181">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="84e0c-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="84e0c-182">d.</span><span class="sxs-lookup"><span data-stu-id="84e0c-182">d.</span></span> <span data-ttu-id="84e0c-183">Оставьте hello **имен** пустым.</span><span class="sxs-lookup"><span data-stu-id="84e0c-183">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="84e0c-184">д.</span><span class="sxs-lookup"><span data-stu-id="84e0c-184">e.</span></span> <span data-ttu-id="84e0c-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-185">Click **Ok**.</span></span>

7. <span data-ttu-id="84e0c-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="84e0c-186">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="84e0c-188">На hello **конфигурации Onit** щелкните **Настройка Onit** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="84e0c-188">On hello **Onit Configuration** section, click **Configure Onit** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="84e0c-189">Копировать hello **URL-адрес выхода, единого входа службы URL-адрес SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="84e0c-189">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="84e0c-191">В другом окне веб-браузера войдите на свой корпоративный сайт Onit в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="84e0c-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="84e0c-192">В меню в верхней части hello hello выберите **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-192">In hello menu on hello top, click **Administration**.</span></span>
   
   <span data-ttu-id="84e0c-193">![Администрирование](./media/active-directory-saas-onit-tutorial/IC791174.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="84e0c-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="84e0c-194">Щелкните **Изменить корпорацию**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="84e0c-195">![Изменить корпорацию](./media/active-directory-saas-onit-tutorial/IC791175.png "Изменить корпорацию")</span><span class="sxs-lookup"><span data-stu-id="84e0c-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="84e0c-196">Нажмите кнопку hello **безопасности** вкладки.</span><span class="sxs-lookup"><span data-stu-id="84e0c-196">Click hello **Security** tab.</span></span>
    
    <span data-ttu-id="84e0c-197">![Изменение информации о компании](./media/active-directory-saas-onit-tutorial/IC791176.png "Изменение информации о компании")</span><span class="sxs-lookup"><span data-stu-id="84e0c-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="84e0c-198">На hello **безопасности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84e0c-198">On hello **Security** tab, perform hello following steps:</span></span>

    <span data-ttu-id="84e0c-199">![Единый вход](./media/active-directory-saas-onit-tutorial/IC791177.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="84e0c-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="84e0c-200">а.</span><span class="sxs-lookup"><span data-stu-id="84e0c-200">a.</span></span> <span data-ttu-id="84e0c-201">Для параметра **Authentication Strategy** (Стратегия проверки подлинности) выберите значение **Single Sign On and Password** (Единый вход и пароль).</span><span class="sxs-lookup"><span data-stu-id="84e0c-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="84e0c-202">b.</span><span class="sxs-lookup"><span data-stu-id="84e0c-202">b.</span></span> <span data-ttu-id="84e0c-203">В **URL-адрес назначения Idp** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="84e0c-203">In **Idp Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="84e0c-204">c.</span><span class="sxs-lookup"><span data-stu-id="84e0c-204">c.</span></span> <span data-ttu-id="84e0c-205">В **URL-адрес выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="84e0c-205">In **Idp logout URL** textbox, paste hello value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="84e0c-206">d.</span><span class="sxs-lookup"><span data-stu-id="84e0c-206">d.</span></span> <span data-ttu-id="84e0c-207">В **отпечаток сертификата поставщика удостоверений (SHA1)** текстовое поле, вставить hello **отпечаток** значение сертификат, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="84e0c-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste hello  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="84e0c-208">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="84e0c-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="84e0c-209">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="84e0c-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="84e0c-210">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84e0c-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="84e0c-211">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="84e0c-211">Create an Azure AD test user</span></span>

<span data-ttu-id="84e0c-212">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="84e0c-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="84e0c-214">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84e0c-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84e0c-215">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="84e0c-215">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="84e0c-217">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-217">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="84e0c-219">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="84e0c-219">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="84e0c-221">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84e0c-221">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="84e0c-223">а.</span><span class="sxs-lookup"><span data-stu-id="84e0c-223">a.</span></span> <span data-ttu-id="84e0c-224">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-224">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84e0c-225">b.</span><span class="sxs-lookup"><span data-stu-id="84e0c-225">b.</span></span> <span data-ttu-id="84e0c-226">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="84e0c-226">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="84e0c-227">c.</span><span class="sxs-lookup"><span data-stu-id="84e0c-227">c.</span></span> <span data-ttu-id="84e0c-228">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="84e0c-228">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="84e0c-229">d.</span><span class="sxs-lookup"><span data-stu-id="84e0c-229">d.</span></span> <span data-ttu-id="84e0c-230">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="84e0c-231">Создание тестового пользователя Onit</span><span class="sxs-lookup"><span data-stu-id="84e0c-231">Create an Onit test user</span></span>

<span data-ttu-id="84e0c-232">В порядке tooenable toolog пользователей Azure AD в Onit их необходимо подготовить в Onit.</span><span class="sxs-lookup"><span data-stu-id="84e0c-232">In order tooenable Azure AD users toolog into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="84e0c-233">В случае hello объекта Onit Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="84e0c-233">In hello case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="84e0c-234">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84e0c-234">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="84e0c-235">Войдите на tooyour **Onit** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="84e0c-235">Sign on tooyour **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="84e0c-236">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="84e0c-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="84e0c-237">![Администрирование](./media/active-directory-saas-onit-tutorial/IC791180.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="84e0c-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="84e0c-238">На hello **добавить пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84e0c-238">On hello **Add User** dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="84e0c-239">![Добавление пользователя](./media/active-directory-saas-onit-tutorial/IC791181.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="84e0c-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="84e0c-240">Тип hello **имя** и hello **адрес электронной почты** из допустимых Azure текстовые поля, связанные с учетной записью AD, которые должны tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="84e0c-240">Type hello **Name** and hello **Email Address** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>
  2. <span data-ttu-id="84e0c-241">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="84e0c-242">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="84e0c-242">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="84e0c-243">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="84e0c-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="84e0c-244">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooOnit доступа.</span><span class="sxs-lookup"><span data-stu-id="84e0c-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOnit.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="84e0c-246">**tooassign tooOnit Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84e0c-246">**tooassign Britta Simon tooOnit, perform hello following steps:**</span></span>

1. <span data-ttu-id="84e0c-247">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="84e0c-249">В списке приложений hello выберите **Onit**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-249">In hello applications list, select **Onit**.</span></span>

    ![ссылка Onit Hello в списке приложений hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="84e0c-251">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="84e0c-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-253">Click **Add** button.</span></span> <span data-ttu-id="84e0c-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="84e0c-256">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="84e0c-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="84e0c-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84e0c-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="84e0c-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="84e0c-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="84e0c-259">Test single sign-on</span></span>

<span data-ttu-id="84e0c-260">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="84e0c-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="84e0c-261">При нажатии кнопки hello Onit плитки в панели доступа hello, вы должны получить tooyour автоматически подписан в приложение Onit.</span><span class="sxs-lookup"><span data-stu-id="84e0c-261">When you click hello Onit tile in hello Access Panel, you should get automatically signed-on tooyour Onit application.</span></span>
<span data-ttu-id="84e0c-262">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="84e0c-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="84e0c-263">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="84e0c-263">Additional resources</span></span>

* [<span data-ttu-id="84e0c-264">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84e0c-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84e0c-265">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="84e0c-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

