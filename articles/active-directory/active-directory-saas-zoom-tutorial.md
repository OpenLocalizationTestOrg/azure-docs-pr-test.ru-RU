---
title: "Руководство по интеграции Azure Active Directory с Zoom | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и масштаба."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="1e6dc-103">Руководство. Интеграция Azure Active Directory с Zoom</span><span class="sxs-lookup"><span data-stu-id="1e6dc-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="1e6dc-104">В этом учебнике вы узнаете, как увеличить toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e6dc-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e6dc-105">Интеграция масштаба с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1e6dc-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e6dc-106">Можно управлять в Azure AD, имеющего доступ tooZoom.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="1e6dc-107">Можно включить на пользователей tooautomatically get вошедшего tooZoom (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1e6dc-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1e6dc-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e6dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e6dc-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1e6dc-110">Prerequisites</span></span>

<span data-ttu-id="1e6dc-111">Интеграция tooconfigure Azure AD с масштабом, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1e6dc-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="1e6dc-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1e6dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e6dc-113">подписка Zoom с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e6dc-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e6dc-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1e6dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e6dc-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e6dc-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e6dc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e6dc-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1e6dc-118">Scenario description</span></span>
<span data-ttu-id="1e6dc-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e6dc-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1e6dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e6dc-121">Добавление масштаба из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1e6dc-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="1e6dc-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e6dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="1e6dc-123">Добавление масштаба из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1e6dc-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="1e6dc-124">Интеграция hello tooconfigure масштабирования в Azure AD, вы должны tooadd масштаба из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e6dc-125">**tooadd масштаба из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e6dc-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e6dc-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="1e6dc-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1e6dc-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="1e6dc-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="1e6dc-133">Введите в поле поиска hello **масштаб**выберите **масштаб** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Масштаб в списке результатов hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1e6dc-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e6dc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1e6dc-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Zoom с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e6dc-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в масштаба является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="1e6dc-138">Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в toobe потребностей масштаба установлено.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="1e6dc-139">В масштаб, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1e6dc-140">tooconfigure и теста Azure AD единого входа с масштабом, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1e6dc-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e6dc-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e6dc-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e6dc-143">**[Создание тестового пользователя масштаба](#create-a-zoom-test-user)**  -toohave аналог Саймон Britta в масштаб, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e6dc-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e6dc-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1e6dc-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e6dc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1e6dc-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении масштаба.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="1e6dc-148">**tooconfigure Azure AD единого входа «масштаб» выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e6dc-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e6dc-149">В hello в hello портала Azure **масштаб** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="1e6dc-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="1e6dc-153">На hello **URL-адреса и домена масштаб** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e6dc-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="1e6dc-155">а.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-155">a.</span></span> <span data-ttu-id="1e6dc-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="1e6dc-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="1e6dc-157">b.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-157">b.</span></span> <span data-ttu-id="1e6dc-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="1e6dc-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e6dc-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-159">These values are not real.</span></span> <span data-ttu-id="1e6dc-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e6dc-161">Обратитесь к [группа поддержки масштаб клиента](https://support.zoom.us/hc) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="1e6dc-162">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="1e6dc-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1e6dc-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e6dc-166">На hello **масштаб конфигурации** щелкните **настроить масштаб** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1e6dc-167">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="1e6dc-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="1e6dc-169">В другом окне браузера Войдите на сайте компании tooyour масштабирования в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="1e6dc-170">Нажмите кнопку hello **Single Sign-On** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="1e6dc-171">![Вкладка единого входа](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1e6dc-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="1e6dc-172">Щелкните hello **управления безопасностью** вкладку, а затем перейдите toohello **Single Sign-On** параметры.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="1e6dc-173">В hello единым входом раздел выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1e6dc-174">![Раздел единого входа](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="1e6dc-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="1e6dc-175">а.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-175">a.</span></span> <span data-ttu-id="1e6dc-176">В hello **входа в URL-адрес страницы** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="1e6dc-177">b.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-177">b.</span></span> <span data-ttu-id="1e6dc-178">В hello **URL-адрес страницы выхода** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="1e6dc-179">c.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-179">c.</span></span> <span data-ttu-id="1e6dc-180">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="1e6dc-181">d.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-181">d.</span></span> <span data-ttu-id="1e6dc-182">В hello **издателя** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1e6dc-183">д.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-183">e.</span></span> <span data-ttu-id="1e6dc-184">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1e6dc-185">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1e6dc-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1e6dc-186">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1e6dc-187">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e6dc-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1e6dc-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e6dc-188">Create an Azure AD test user</span></span>

<span data-ttu-id="1e6dc-189">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="1e6dc-191">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e6dc-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e6dc-192">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1e6dc-194">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1e6dc-196">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1e6dc-198">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e6dc-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1e6dc-200">а.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-200">a.</span></span> <span data-ttu-id="1e6dc-201">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e6dc-202">b.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-202">b.</span></span> <span data-ttu-id="1e6dc-203">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1e6dc-204">c.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-204">c.</span></span> <span data-ttu-id="1e6dc-205">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1e6dc-206">d.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-206">d.</span></span> <span data-ttu-id="1e6dc-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="1e6dc-208">Создание тестового пользователя Zoom</span><span class="sxs-lookup"><span data-stu-id="1e6dc-208">Create a Zoom test user</span></span>

<span data-ttu-id="1e6dc-209">В порядке tooenable Azure AD пользователи toolog в tooZoom их необходимо подготовить в Zoom.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="1e6dc-210">В случае hello масштабирования Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="1e6dc-211">tooprovision учетной записи пользователя, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="1e6dc-212">Войдите в tooyour **масштаб** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="1e6dc-213">Нажмите кнопку hello **управление учетными записями** , а затем щелкните **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="1e6dc-214">В hello раздел управления пользователями, щелкните **Добавление пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="1e6dc-215">![Управление пользователями](./media/active-directory-saas-zoom-tutorial/IC784703.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="1e6dc-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="1e6dc-216">На hello **Добавление пользователей** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e6dc-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="1e6dc-217">![Добавление пользователей](./media/active-directory-saas-zoom-tutorial/IC784704.png "Добавление пользователей")</span><span class="sxs-lookup"><span data-stu-id="1e6dc-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="1e6dc-218">а.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-218">a.</span></span> <span data-ttu-id="1e6dc-219">В поле **User Type** (Тип пользователя) задайте значение **Basic** (Базовый).</span><span class="sxs-lookup"><span data-stu-id="1e6dc-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="1e6dc-220">b.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-220">b.</span></span> <span data-ttu-id="1e6dc-221">В hello **сообщений электронной почты** текстовом поле введите адрес электронной почты hello допустимым Azure AD счета, tooprovision.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="1e6dc-222">c.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-222">c.</span></span> <span data-ttu-id="1e6dc-223">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="1e6dc-224">Можно использовать любой масштаб пользователя инструменты создания учетных записей или интерфейсы API, предоставляемые tooprovision масштабирования Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1e6dc-225">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1e6dc-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1e6dc-226">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooZoom доступа.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="1e6dc-228">**tooassign tooZoom Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e6dc-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e6dc-229">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1e6dc-231">В списке приложений hello выберите **масштаб**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-231">In hello applications list, select **Zoom**.</span></span>

    ![ссылка масштаба Hello в списке приложений hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="1e6dc-233">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="1e6dc-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-235">Click **Add** button.</span></span> <span data-ttu-id="1e6dc-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="1e6dc-238">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1e6dc-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e6dc-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1e6dc-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1e6dc-241">Test single sign-on</span></span>

<span data-ttu-id="1e6dc-242">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="1e6dc-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1e6dc-243">При выборе плитки масштаба hello в hello панели доступа, следует получать автоматически вошедшего tooyour масштабирования приложения.</span><span class="sxs-lookup"><span data-stu-id="1e6dc-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e6dc-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1e6dc-244">Additional resources</span></span>

* [<span data-ttu-id="1e6dc-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e6dc-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e6dc-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e6dc-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

