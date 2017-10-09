---
title: "Руководство по интеграции Azure Active Directory с приложением MOVEit Transfer - Azure AD integration | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и передачи MOVEit - интеграция Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="a3fbf-103">Руководство по интеграции Azure Active Directory с MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="a3fbf-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="a3fbf-104">В этом учебнике вы узнаете, как toointegrate MOVEit передача — интеграция Azure AD с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3fbf-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3fbf-105">Интеграция MOVEit передача — интеграция Azure AD с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a3fbf-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a3fbf-106">Можно управлять в Azure AD, имеющего доступ tooMOVEit передача — интеграция Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="a3fbf-107">Можно включить на пользователей tooautomatically get вошедшего tooMOVEit передача — интеграция Azure AD (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a3fbf-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a3fbf-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3fbf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3fbf-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a3fbf-110">Prerequisites</span></span>

<span data-ttu-id="a3fbf-111">Интеграция Azure AD с MOVEit передача — интеграция Azure AD tooconfigure требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a3fbf-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="a3fbf-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a3fbf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3fbf-113">подписка MOVEit Transfer с Azure AD integration с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3fbf-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3fbf-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a3fbf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3fbf-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3fbf-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3fbf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3fbf-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a3fbf-118">Scenario description</span></span>
<span data-ttu-id="a3fbf-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3fbf-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a3fbf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3fbf-121">Добавление MOVEit передача — интеграция Azure AD из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a3fbf-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="a3fbf-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3fbf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="a3fbf-123">Добавление MOVEit передача — интеграция Azure AD из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a3fbf-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="a3fbf-124">Интеграция hello tooconfigure передачи MOVEit - интеграция Azure AD в Azure AD необходимо tooadd MOVEit передача — интеграция Azure AD из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a3fbf-125">**tooadd передача MOVEit — интеграция Azure AD из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a3fbf-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3fbf-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="a3fbf-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a3fbf-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="a3fbf-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="a3fbf-133">Введите в поле поиска hello **MOVEit передача — интеграция Azure AD**выберите **MOVEit передача — интеграция Azure AD** из панели результатов щелкните **добавить** hello tooadd кнопку приложение.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Передача MOVEit — интеграция Azure AD в списке результатов hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a3fbf-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3fbf-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a3fbf-136">В этом разделе показано, как настроить и проверить единый вход Azure AD в приложение MOVEit Transfer - Azure AD integration с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a3fbf-137">Для единого входа toowork Azure AD необходима tooknow hello аналог пользователя во время передачи MOVEit - интеграция Azure AD tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="a3fbf-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей во время передачи MOVEit - интеграция Azure AD должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="a3fbf-139">Во время передачи MOVEit - интеграция Azure AD, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a3fbf-140">tooconfigure и тестирования Azure AD единого входа для передачи MOVEit - интеграция Azure AD, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a3fbf-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a3fbf-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a3fbf-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3fbf-143">**[Создание тестового пользователя Azure AD интеграции переноса MOVEit -](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave аналог Саймон Britta во время передачи MOVEit - интеграция Azure AD, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3fbf-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3fbf-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a3fbf-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3fbf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a3fbf-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в MOVEit передачи - интеграция приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="a3fbf-148">**tooconfigure Azure AD единого входа для передачи MOVEit - интеграция Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a3fbf-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3fbf-149">В hello в hello портала Azure **MOVEit передача — интеграция Azure AD** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="a3fbf-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="a3fbf-153">На hello **MOVEit передача — интеграция Azure AD доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a3fbf-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="a3fbf-155">а.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-155">a.</span></span> <span data-ttu-id="a3fbf-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="a3fbf-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="a3fbf-157">b.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-157">b.</span></span> <span data-ttu-id="a3fbf-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="a3fbf-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="a3fbf-159">c.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-159">c.</span></span> <span data-ttu-id="a3fbf-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="a3fbf-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="a3fbf-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-161">These values are not real.</span></span> <span data-ttu-id="a3fbf-162">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a3fbf-163">Можно ссылаться эти значения позже в **URL-адрес метаданных службы поставщика** разделу или обратитесь в службу [MOVEit передача — группа поддержки клиента Azure AD интеграции](https://community.ipswitch.com/s/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="a3fbf-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="a3fbf-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a3fbf-166">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="a3fbf-168">Войдите на tooyour MOVEit передачи клиента с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="a3fbf-169">На панели навигации слева hello, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Раздел Settings (Параметры) на стороне приложения](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="a3fbf-171">Щелкните ссылку **Single Signon** (Единый вход), которая расположена в разделе **Security Policies -> User Auth** (Политики безопасности -> Проверка подлинности пользователя).</span><span class="sxs-lookup"><span data-stu-id="a3fbf-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Политики безопасности на стороне приложения](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="a3fbf-173">Щелкните hello hello URL-адрес метаданных ссылки toodownload документа метаданных.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![URL-адрес метаданных поставщика службы](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="a3fbf-175">Проверьте **entityID** соответствует **идентификатор** в hello **MOVEit передача — интеграция Azure AD доменов и URL-адреса** раздела.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="a3fbf-176">Проверьте **AssertionConsumerService** соответствует URL-адрес расположения **URL-адрес ОТВЕТА** в hello **MOVEit передача — интеграция Azure AD доменов и URL-адреса** раздела.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="a3fbf-178">Нажмите кнопку **Добавление поставщика удостоверений** кнопку tooadd новый поставщик федеративных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![Добавление поставщика удостоверений](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="a3fbf-180">Нажмите кнопку **Обзор...**  tooselect hello файл метаданных, который был загружен с портала Azure, а затем щелкните **Добавление поставщика удостоверений** tooupload hello загрузили файл.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![Поставщик удостоверений SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="a3fbf-182">Выберите «**Да**» как **включено** в hello **изменить параметры поставщика федеративных удостоверений...**  и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Параметры федеративного поставщика удостоверений](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="a3fbf-184">В hello **изменение федеративного удостоверения пользователя параметры поставщика** выполните hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a3fbf-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Изменение параметров федеративного поставщика удостоверений](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="a3fbf-186">а.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-186">a.</span></span> <span data-ttu-id="a3fbf-187">Выберите значение **SAML NameID** для параметра **Login name** (Имя для входа).</span><span class="sxs-lookup"><span data-stu-id="a3fbf-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="a3fbf-188">b.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-188">b.</span></span> <span data-ttu-id="a3fbf-189">Выберите **других** как **полное имя** и в hello **имя атрибута** текстовое поле поместить значение hello: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="a3fbf-190">c.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-190">c.</span></span> <span data-ttu-id="a3fbf-191">Выберите **других** как **электронной почты** и в hello **имя атрибута** текстовое поле поместить значение hello: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="a3fbf-192">d.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-192">d.</span></span> <span data-ttu-id="a3fbf-193">Выберите значение **Yes** (Да) для параметра **Auto-create account on signon** (Автоматическое создание учетной записи при первом входе).</span><span class="sxs-lookup"><span data-stu-id="a3fbf-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="a3fbf-194">д.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-194">e.</span></span> <span data-ttu-id="a3fbf-195">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a3fbf-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="a3fbf-196">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a3fbf-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a3fbf-197">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a3fbf-198">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3fbf-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a3fbf-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3fbf-199">Create an Azure AD test user</span></span>

<span data-ttu-id="a3fbf-200">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="a3fbf-202">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a3fbf-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3fbf-203">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a3fbf-205">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a3fbf-207">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a3fbf-209">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a3fbf-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a3fbf-211">а.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-211">a.</span></span> <span data-ttu-id="a3fbf-212">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3fbf-213">b.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-213">b.</span></span> <span data-ttu-id="a3fbf-214">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a3fbf-215">c.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-215">c.</span></span> <span data-ttu-id="a3fbf-216">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a3fbf-217">d.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-217">d.</span></span> <span data-ttu-id="a3fbf-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="a3fbf-219">Создание тестового пользователя MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="a3fbf-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="a3fbf-220">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon во время передачи MOVEit - интеграция Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="a3fbf-221">Приложение MOVEit Transfer - Azure AD integration поддерживает JIT-подготовку, и вы уже включили ее.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="a3fbf-222">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-222">There is no action item for you in this section.</span></span> <span data-ttu-id="a3fbf-223">Новый пользователь создается во время попытки tooaccess MOVEit передача — интеграция Azure AD, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a3fbf-224">Если требуется toocreate пользователя вручную, необходимо toocontact hello [MOVEit передача — группа поддержки клиента Azure AD интеграции](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="a3fbf-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a3fbf-225">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a3fbf-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a3fbf-226">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooMOVEit передача — интеграция Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="a3fbf-228">**tooassign tooMOVEit Britta Simon передача — интеграция Azure AD, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a3fbf-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3fbf-229">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a3fbf-231">В списке приложений hello выберите **MOVEit передача — интеграция Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Hello MOVEit передача — интеграция Azure AD ссылку в список приложений hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="a3fbf-233">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="a3fbf-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-235">Click **Add** button.</span></span> <span data-ttu-id="a3fbf-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="a3fbf-238">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a3fbf-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3fbf-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a3fbf-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a3fbf-241">Test single sign-on</span></span>

<span data-ttu-id="a3fbf-242">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="a3fbf-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a3fbf-243">При нажатии кнопки hello передача MOVEit — Azure AD интеграции плитки в hello панели доступа, вы должны получить автоматически вошедшего tooyour передачи MOVEit - интеграция приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3fbf-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a3fbf-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a3fbf-244">Additional resources</span></span>

* [<span data-ttu-id="a3fbf-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3fbf-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3fbf-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3fbf-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

