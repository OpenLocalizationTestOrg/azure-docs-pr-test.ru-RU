---
title: "Учебник. Интеграция Azure Active Directory с Egnyte | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="b86fd-103">Руководство. Интеграция Azure Active Directory с Egnyte</span><span class="sxs-lookup"><span data-stu-id="b86fd-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="b86fd-104">В этом учебнике вы узнаете, как toointegrate Egnyte с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b86fd-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b86fd-105">Интеграция Egnyte с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b86fd-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b86fd-106">Можно управлять в Azure AD, имеющего доступ tooEgnyte</span><span class="sxs-lookup"><span data-stu-id="b86fd-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="b86fd-107">Можно включить на пользователей tooautomatically get вошедшего tooEgnyte (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86fd-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b86fd-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b86fd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b86fd-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b86fd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b86fd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b86fd-110">Prerequisites</span></span>

<span data-ttu-id="b86fd-111">tooconfigure интеграция Azure AD с Egnyte, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b86fd-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="b86fd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b86fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b86fd-113">Подписка с поддержкой единого входа Egnyte</span><span class="sxs-lookup"><span data-stu-id="b86fd-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b86fd-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b86fd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b86fd-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b86fd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b86fd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b86fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b86fd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b86fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b86fd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b86fd-118">Scenario description</span></span>
<span data-ttu-id="b86fd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b86fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b86fd-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b86fd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b86fd-121">Добавление Egnyte из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b86fd-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="b86fd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="b86fd-123">Добавление Egnyte из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b86fd-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="b86fd-124">tooconfigure hello интеграции Egnyte в Azure AD, вы должны tooadd Egnyte из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b86fd-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b86fd-125">**tooadd Egnyte из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b86fd-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86fd-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b86fd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b86fd-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b86fd-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b86fd-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b86fd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b86fd-133">Введите в поле поиска hello **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-133">In hello search box, type **Egnyte**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="b86fd-135">В панели результатов hello выберите **Egnyte**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b86fd-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b86fd-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b86fd-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Egnyte для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b86fd-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b86fd-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Egnyte является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b86fd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="b86fd-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Egnyte должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b86fd-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="b86fd-141">В Egnyte, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b86fd-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b86fd-142">tooconfigure и теста Azure AD единого входа с Egnyte, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b86fd-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b86fd-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b86fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b86fd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b86fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b86fd-145">**[Создание тестового пользователя, прошедшего Egnyte](#creating-an-egnyte-test-user) ** -toohave аналог Саймон Britta в Egnyte, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b86fd-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b86fd-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b86fd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b86fd-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b86fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b86fd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b86fd-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Egnyte.</span><span class="sxs-lookup"><span data-stu-id="b86fd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="b86fd-150">**Azure AD tooconfigure единого входа с Egnyte, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b86fd-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86fd-151">В hello в hello портала Azure **Egnyte** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b86fd-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b86fd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="b86fd-155">На hello **URL-адреса и домена Egnyte** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b86fd-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="b86fd-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="b86fd-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b86fd-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="b86fd-158">This value is not real.</span></span> <span data-ttu-id="b86fd-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="b86fd-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b86fd-160">Обратитесь к [группа поддержки клиента Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="b86fd-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="b86fd-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b86fd-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="b86fd-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b86fd-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b86fd-165">На hello **конфигурации Egnyte** щелкните **Настройка Egnyte** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b86fd-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b86fd-166">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="b86fd-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="b86fd-168">В другом окне браузера войти в корпоративный сайт Egnyte tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="b86fd-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="b86fd-169">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="b86fd-170">![Параметры](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="b86fd-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="b86fd-171">В меню "hello" щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="b86fd-172">![Параметры](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="b86fd-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="b86fd-173">Нажмите кнопку hello **конфигурации** , а затем щелкните **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="b86fd-174">![Безопасность](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="b86fd-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="b86fd-175">В hello **единого входа для проверки подлинности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b86fd-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="b86fd-176">![Аутентификация единого входа](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Аутентификация единого входа")</span><span class="sxs-lookup"><span data-stu-id="b86fd-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="b86fd-177">а.</span><span class="sxs-lookup"><span data-stu-id="b86fd-177">a.</span></span> <span data-ttu-id="b86fd-178">Выберите для параметра **Single sign-on authentication** (Аутентификация единого входа) значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="b86fd-179">b.</span><span class="sxs-lookup"><span data-stu-id="b86fd-179">b.</span></span> <span data-ttu-id="b86fd-180">Выберите для параметра **Identity provider** (Поставщик удостоверений) значение **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="b86fd-181">c.</span><span class="sxs-lookup"><span data-stu-id="b86fd-181">c.</span></span> <span data-ttu-id="b86fd-182">Вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure в hello **URL-адрес входа поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b86fd-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="b86fd-183">d.</span><span class="sxs-lookup"><span data-stu-id="b86fd-183">d.</span></span> <span data-ttu-id="b86fd-184">Вставить **идентификатор сущности SAML** скопирован из портала Azure в hello **идентификатор сущности поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b86fd-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="b86fd-185">д.</span><span class="sxs-lookup"><span data-stu-id="b86fd-185">e.</span></span> <span data-ttu-id="b86fd-186">Откройте сертификат в кодировке base-64 в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b86fd-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="b86fd-187">f.</span><span class="sxs-lookup"><span data-stu-id="b86fd-187">f.</span></span> <span data-ttu-id="b86fd-188">Выберите для параметра **Default user mapping** (Сопоставление пользователя по умолчанию) значение **Email address** (Адрес электронной почты).</span><span class="sxs-lookup"><span data-stu-id="b86fd-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="b86fd-189">ж.</span><span class="sxs-lookup"><span data-stu-id="b86fd-189">g.</span></span> <span data-ttu-id="b86fd-190">Выберите для параметра **Use domain-specific issuer value** (Использовать значение издателя домена) значение **disabled** (отключено).</span><span class="sxs-lookup"><span data-stu-id="b86fd-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="b86fd-191">h.</span><span class="sxs-lookup"><span data-stu-id="b86fd-191">h.</span></span> <span data-ttu-id="b86fd-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b86fd-193">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b86fd-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b86fd-194">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b86fd-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b86fd-195">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b86fd-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b86fd-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b86fd-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="b86fd-197">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b86fd-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b86fd-199">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b86fd-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86fd-200">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b86fd-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b86fd-202">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b86fd-204">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b86fd-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b86fd-206">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b86fd-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b86fd-208">а.</span><span class="sxs-lookup"><span data-stu-id="b86fd-208">a.</span></span> <span data-ttu-id="b86fd-209">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b86fd-210">b.</span><span class="sxs-lookup"><span data-stu-id="b86fd-210">b.</span></span> <span data-ttu-id="b86fd-211">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b86fd-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b86fd-212">c.</span><span class="sxs-lookup"><span data-stu-id="b86fd-212">c.</span></span> <span data-ttu-id="b86fd-213">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b86fd-214">d.</span><span class="sxs-lookup"><span data-stu-id="b86fd-214">d.</span></span> <span data-ttu-id="b86fd-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="b86fd-216">Создание тестового пользователя Egnyte</span><span class="sxs-lookup"><span data-stu-id="b86fd-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="b86fd-217">Пользователи toolog tooenable Azure AD в tooEgnyte, их необходимо подготовить в Egnyte.</span><span class="sxs-lookup"><span data-stu-id="b86fd-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="b86fd-218">В случае hello объекта Egnyte Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="b86fd-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="b86fd-219">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="b86fd-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86fd-220">Войдите в tooyour **Egnyte** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="b86fd-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="b86fd-221">Go слишком**параметры \> пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="b86fd-222">Нажмите кнопку **добавить пользователя**, а затем выберите тип hello пользователя требуется tooadd.</span><span class="sxs-lookup"><span data-stu-id="b86fd-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="b86fd-223">![Пользователи](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="b86fd-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="b86fd-224">В hello **новый обычный пользователь** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b86fd-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="b86fd-225">![Новый обычный пользователь](./media/active-directory-saas-egnyte-tutorial/ic787825.png "Новый обычный пользователь")</span><span class="sxs-lookup"><span data-stu-id="b86fd-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="b86fd-226">а.</span><span class="sxs-lookup"><span data-stu-id="b86fd-226">a.</span></span> <span data-ttu-id="b86fd-227">Тип hello **электронной почты**, **Username**и другие сведения о действительной учетной записи Azure Active Directory требуется tooprovision.</span><span class="sxs-lookup"><span data-stu-id="b86fd-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="b86fd-228">b.</span><span class="sxs-lookup"><span data-stu-id="b86fd-228">b.</span></span> <span data-ttu-id="b86fd-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="b86fd-230">Владелец учетной записи Azure Active Directory Hello получит уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="b86fd-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="b86fd-231">Можно использовать любые другие Egnyte пользователя средства создания учетных записей или интерфейсы API, предоставляемые Egnyte tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="b86fd-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b86fd-232">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b86fd-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b86fd-233">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooEgnyte доступа.</span><span class="sxs-lookup"><span data-stu-id="b86fd-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b86fd-235">**tooassign tooEgnyte Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b86fd-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="b86fd-236">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b86fd-238">В списке приложений hello выберите **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-238">In hello applications list, select **Egnyte**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="b86fd-240">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b86fd-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-242">Click **Add** button.</span></span> <span data-ttu-id="b86fd-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b86fd-245">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b86fd-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b86fd-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b86fd-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b86fd-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b86fd-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b86fd-248">Testing single sign-on</span></span>

<span data-ttu-id="b86fd-249">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b86fd-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b86fd-250">При нажатии кнопки hello Egnyte плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на Egnyte приложения.</span><span class="sxs-lookup"><span data-stu-id="b86fd-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="b86fd-251">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b86fd-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b86fd-252">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b86fd-252">Additional resources</span></span>

* [<span data-ttu-id="b86fd-253">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b86fd-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b86fd-254">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b86fd-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

