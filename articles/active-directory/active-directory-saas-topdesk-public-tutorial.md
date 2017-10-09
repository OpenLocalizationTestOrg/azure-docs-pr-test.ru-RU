---
title: "Руководство. Интеграция Azure Active Directory с TOPdesk - Public | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и общедоступной версии TOPdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="3b57f-103">Учебник. Интеграция Azure Active Directory с TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="3b57f-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="3b57f-104">В этом учебнике вы узнаете, как toointegrate TOPdesk - Public с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3b57f-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b57f-105">Интеграция TOPdesk - Public с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3b57f-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3b57f-106">Можно управлять в Azure AD, имеющего tooTOPdesk доступа - открытый.</span><span class="sxs-lookup"><span data-stu-id="3b57f-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="3b57f-107">Можно включить на пользователей tooautomatically get вошедшего tooTOPdesk - Public (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b57f-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3b57f-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3b57f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="3b57f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3b57f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b57f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3b57f-110">Prerequisites</span></span>

<span data-ttu-id="3b57f-111">Интеграция Azure AD с версией TOPdesk - tooconfigure общим, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3b57f-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="3b57f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3b57f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b57f-113">Подписка TOPdesk — Public с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3b57f-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3b57f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3b57f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3b57f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3b57f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b57f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3b57f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3b57f-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b57f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3b57f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3b57f-118">Scenario description</span></span>
<span data-ttu-id="3b57f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3b57f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3b57f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3b57f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b57f-121">Добавление TOPdesk - Public из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3b57f-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="3b57f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b57f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="3b57f-123">Добавление TOPdesk - Public из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3b57f-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="3b57f-124">Интеграция hello tooconfigure общедоступной в Azure AD версии TOPdesk требуется tooadd TOPdesk - Public из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3b57f-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3b57f-125">**tooadd TOPdesk - Public из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3b57f-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b57f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3b57f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="3b57f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3b57f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="3b57f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3b57f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="3b57f-133">Введите в поле поиска hello **общедоступной версии TOPdesk**выберите **общедоступной версии TOPdesk** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3b57f-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TOPdesk - Public в списке результатов hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3b57f-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b57f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3b57f-136">В этом разделе описана настройка и проверка единого входа Azure AD в TOPdesk - Public с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b57f-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3b57f-137">Для единого входа toowork Azure AD необходима tooknow, какой пользователь hello аналога в TOPdesk - Public tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b57f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="3b57f-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в TOPdesk - Public должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3b57f-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="3b57f-139">В версии TOPdesk - Public, назначить значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="3b57f-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3b57f-140">tooconfigure и протестировать Azure AD единого входа с общедоступной версии TOPdesk, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3b57f-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3b57f-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3b57f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3b57f-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3b57f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b57f-143">**[Создание TOPdesk — открытый тестового пользователя](#create-a-topdesk---public-test-user)**  - toohave аналог Саймон Britta в TOPdesk - Public, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b57f-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3b57f-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3b57f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b57f-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3b57f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3b57f-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b57f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3b57f-147">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в ваш общедоступную версию TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="3b57f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="3b57f-148">**tooconfigure Azure AD единого входа с версией TOPdesk - открытым, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="3b57f-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b57f-149">В hello в hello портала Azure **общедоступной версии TOPdesk** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="3b57f-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3b57f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="3b57f-153">На hello **TOPdesk — общедоступный домен и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3b57f-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="3b57f-155">а.</span><span class="sxs-lookup"><span data-stu-id="3b57f-155">a.</span></span> <span data-ttu-id="3b57f-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="3b57f-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="3b57f-157">b.</span><span class="sxs-lookup"><span data-stu-id="3b57f-157">b.</span></span> <span data-ttu-id="3b57f-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="3b57f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="3b57f-159">c.</span><span class="sxs-lookup"><span data-stu-id="3b57f-159">c.</span></span> <span data-ttu-id="3b57f-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="3b57f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3b57f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3b57f-161">These values are not real.</span></span> <span data-ttu-id="3b57f-162">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="3b57f-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3b57f-163">URL-адрес ответа поясняется далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="3b57f-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="3b57f-164">Обратитесь к [TOPdesk - группа поддержки открытого клиента](https://help.topdesk.com/saas/enterprise/user/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="3b57f-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="3b57f-165">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3b57f-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="3b57f-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3b57f-167">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3b57f-169">На hello **TOPdesk - открытой конфигурации** щелкните **Настройка общедоступной версии TOPdesk** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="3b57f-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3b57f-170">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="3b57f-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="3b57f-172">Войдите на tooyour **общедоступной версии TOPdesk** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="3b57f-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="3b57f-173">В hello **TOPdesk** меню, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="3b57f-174">![Параметры](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="3b57f-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="3b57f-175">Щелкните **Параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="3b57f-176">![Параметры входа](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Параметры входа")</span><span class="sxs-lookup"><span data-stu-id="3b57f-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="3b57f-177">Разверните hello **параметры входа** меню, а затем нажмите **Общие**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="3b57f-178">![Общие](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Общие")</span><span class="sxs-lookup"><span data-stu-id="3b57f-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="3b57f-179">В hello **открытый** раздел hello **входа SAML** конфигурации выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3b57f-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3b57f-180">![Технические параметры](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Технические параметры")</span><span class="sxs-lookup"><span data-stu-id="3b57f-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="3b57f-181">а.</span><span class="sxs-lookup"><span data-stu-id="3b57f-181">a.</span></span> <span data-ttu-id="3b57f-182">Нажмите кнопку **загрузки** toodownload hello общедоступный файл метаданных, а затем сохраните его локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3b57f-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="3b57f-183">b.</span><span class="sxs-lookup"><span data-stu-id="3b57f-183">b.</span></span> <span data-ttu-id="3b57f-184">Откройте файл метаданных загружаются hello, а затем найдите hello **AssertionConsumerService** узла.</span><span class="sxs-lookup"><span data-stu-id="3b57f-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="3b57f-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="3b57f-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="3b57f-186">c.</span><span class="sxs-lookup"><span data-stu-id="3b57f-186">c.</span></span> <span data-ttu-id="3b57f-187">Копировать hello **AssertionConsumerService** значений, вставьте это значение в hello **URL-адрес ответа** текстовое поле в **TOPdesk — общедоступный домен и URL-адреса** раздела.</span><span class="sxs-lookup"><span data-stu-id="3b57f-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="3b57f-188">toocreate файлом сертификата, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="3b57f-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="3b57f-189">![Сертификат](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Сертификат")</span><span class="sxs-lookup"><span data-stu-id="3b57f-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="3b57f-190">а.</span><span class="sxs-lookup"><span data-stu-id="3b57f-190">a.</span></span> <span data-ttu-id="3b57f-191">Откройте hello скачать файл метаданных на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3b57f-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="3b57f-192">b.</span><span class="sxs-lookup"><span data-stu-id="3b57f-192">b.</span></span> <span data-ttu-id="3b57f-193">Разверните hello **RoleDescriptor** узла, имеющего **xsi: Type** из **fed: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="3b57f-194">c.</span><span class="sxs-lookup"><span data-stu-id="3b57f-194">c.</span></span> <span data-ttu-id="3b57f-195">Скопируйте значение hello hello **X509Certificate** узла.</span><span class="sxs-lookup"><span data-stu-id="3b57f-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="3b57f-196">d.</span><span class="sxs-lookup"><span data-stu-id="3b57f-196">d.</span></span> <span data-ttu-id="3b57f-197">Сохранить hello копируются **X509Certificate** значение на локальном компьютере в файле.</span><span class="sxs-lookup"><span data-stu-id="3b57f-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="3b57f-198">В hello **открытый** щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="3b57f-199">![Вход SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Вход SAML")</span><span class="sxs-lookup"><span data-stu-id="3b57f-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="3b57f-200">На hello **помощник по настройке SAML** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3b57f-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="3b57f-201">![Помощник по настройке SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Помощник по настройке SAML")</span><span class="sxs-lookup"><span data-stu-id="3b57f-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="3b57f-202">а.</span><span class="sxs-lookup"><span data-stu-id="3b57f-202">a.</span></span> <span data-ttu-id="3b57f-203">tooupload загруженных метаданных файла из портала Azure в разделе **метаданные федерации**, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="3b57f-204">b.</span><span class="sxs-lookup"><span data-stu-id="3b57f-204">b.</span></span> <span data-ttu-id="3b57f-205">файл сертификата, в разделе tooupload **сертификат (RSA)**, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="3b57f-206">c.</span><span class="sxs-lookup"><span data-stu-id="3b57f-206">c.</span></span> <span data-ttu-id="3b57f-207">Файл эмблемы hello tooupload, полученного от поддержки topdesk hello в разделе **значок логотипа**, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="3b57f-208">d.</span><span class="sxs-lookup"><span data-stu-id="3b57f-208">d.</span></span> <span data-ttu-id="3b57f-209">В hello **атрибут имени пользователя** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="3b57f-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="3b57f-210">д.</span><span class="sxs-lookup"><span data-stu-id="3b57f-210">e.</span></span> <span data-ttu-id="3b57f-211">В hello **отображаемое имя** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3b57f-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="3b57f-212">f.</span><span class="sxs-lookup"><span data-stu-id="3b57f-212">f.</span></span> <span data-ttu-id="3b57f-213">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3b57f-214">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3b57f-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3b57f-215">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3b57f-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3b57f-216">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3b57f-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3b57f-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b57f-217">Create an Azure AD test user</span></span>

<span data-ttu-id="3b57f-218">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3b57f-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="3b57f-220">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3b57f-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b57f-221">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="3b57f-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3b57f-223">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3b57f-225">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="3b57f-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3b57f-227">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3b57f-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3b57f-229">а.</span><span class="sxs-lookup"><span data-stu-id="3b57f-229">a.</span></span> <span data-ttu-id="3b57f-230">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3b57f-231">b.</span><span class="sxs-lookup"><span data-stu-id="3b57f-231">b.</span></span> <span data-ttu-id="3b57f-232">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3b57f-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3b57f-233">c.</span><span class="sxs-lookup"><span data-stu-id="3b57f-233">c.</span></span> <span data-ttu-id="3b57f-234">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="3b57f-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3b57f-235">d.</span><span class="sxs-lookup"><span data-stu-id="3b57f-235">d.</span></span> <span data-ttu-id="3b57f-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="3b57f-237">Создание тестового пользователя TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="3b57f-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="3b57f-238">В порядке tooenable Azure AD пользователи toolog в версии TOPdesk - открытым, их необходимо подготовить в общедоступной версии TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="3b57f-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="3b57f-239">В случае, когда hello TOPdesk - Public Подготовка пользователей осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="3b57f-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="3b57f-240">tooconfigure подготовки пользователей, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="3b57f-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="3b57f-241">Войдите на tooyour **общедоступной версии TOPdesk** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="3b57f-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="3b57f-242">В меню в верхней части hello hello выберите **TOPdesk \> New \> файлы поддержки \> лицо**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="3b57f-243">![Пользователь](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="3b57f-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="3b57f-244">В диалоговом окне Новый пользователь hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="3b57f-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="3b57f-245">![Новый пользователь](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="3b57f-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="3b57f-246">а.</span><span class="sxs-lookup"><span data-stu-id="3b57f-246">a.</span></span> <span data-ttu-id="3b57f-247">Щелкните вкладку Общие hello.</span><span class="sxs-lookup"><span data-stu-id="3b57f-247">Click hello General tab.</span></span>

    <span data-ttu-id="3b57f-248">b.</span><span class="sxs-lookup"><span data-stu-id="3b57f-248">b.</span></span> <span data-ttu-id="3b57f-249">В hello **Фамилия** текстовом поле введите фамилию пользователя hello как Simon</span><span class="sxs-lookup"><span data-stu-id="3b57f-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="3b57f-250">c.</span><span class="sxs-lookup"><span data-stu-id="3b57f-250">c.</span></span> <span data-ttu-id="3b57f-251">Выберите **сайта** hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3b57f-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="3b57f-252">d.</span><span class="sxs-lookup"><span data-stu-id="3b57f-252">d.</span></span> <span data-ttu-id="3b57f-253">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="3b57f-254">Можно использовать другие TOPdesk — открытый инструменты создания учетных записей или API-интерфейсы, предоставляемые версией TOPdesk - учетных записей пользователей открытый tooprovision Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b57f-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3b57f-255">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3b57f-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3b57f-256">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTOPdesk доступа - открытый.</span><span class="sxs-lookup"><span data-stu-id="3b57f-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="3b57f-258">**tooassign tooTOPdesk Britta Simon - открытым, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="3b57f-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b57f-259">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3b57f-261">В списке приложений hello выберите **общедоступной версии TOPdesk**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![Hello версии TOPdesk - Public ссылку в список приложений hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="3b57f-263">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="3b57f-265">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-265">Click **Add** button.</span></span> <span data-ttu-id="3b57f-266">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="3b57f-268">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3b57f-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3b57f-269">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3b57f-270">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3b57f-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3b57f-271">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3b57f-271">Test single sign-on</span></span>

<span data-ttu-id="3b57f-272">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="3b57f-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3b57f-273">При нажатии кнопки hello TOPdesk - Public плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour TOPdesk - открытые приложения.</span><span class="sxs-lookup"><span data-stu-id="3b57f-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="3b57f-274">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3b57f-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3b57f-275">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3b57f-275">Additional resources</span></span>

* [<span data-ttu-id="3b57f-276">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b57f-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b57f-277">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3b57f-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

