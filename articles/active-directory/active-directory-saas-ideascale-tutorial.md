---
title: "Учебник. Интеграция Azure Active Directory с IdeaScale | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="1e776-103">Руководство. Интеграция Azure Active Directory с IdeaScale</span><span class="sxs-lookup"><span data-stu-id="1e776-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="1e776-104">В этом учебнике вы узнаете, как toointegrate IdeaScale с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e776-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e776-105">Интеграция IdeaScale с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1e776-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e776-106">Можно управлять в Azure AD, имеющего доступ tooIdeaScale</span><span class="sxs-lookup"><span data-stu-id="1e776-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="1e776-107">Можно включить на пользователей tooautomatically get вошедшего tooIdeaScale (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e776-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e776-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1e776-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1e776-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e776-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e776-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1e776-110">Prerequisites</span></span>

<span data-ttu-id="1e776-111">tooconfigure интеграция Azure AD с IdeaScale требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1e776-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="1e776-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1e776-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e776-113">подписка IdeaScale с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e776-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e776-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1e776-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e776-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1e776-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e776-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1e776-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e776-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e776-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e776-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1e776-118">Scenario description</span></span>
<span data-ttu-id="1e776-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1e776-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e776-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1e776-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e776-121">Добавление IdeaScale из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1e776-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="1e776-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e776-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="1e776-123">Добавление IdeaScale из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1e776-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="1e776-124">tooconfigure hello интеграции IdeaScale в Azure AD, вы должны tooadd IdeaScale из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e776-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e776-125">**tooadd IdeaScale из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e776-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e776-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1e776-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e776-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1e776-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1e776-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e776-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1e776-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1e776-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1e776-133">Введите в поле поиска hello **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="1e776-133">In hello search box, type **IdeaScale**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="1e776-135">В панели результатов hello выберите **IdeaScale**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1e776-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e776-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e776-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e776-138">В этом разделе описана настройка и проверка единого входа Azure AD в IdeaScale с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e776-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1e776-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в IdeaScale является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e776-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="1e776-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в IdeaScale должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="1e776-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="1e776-141">В IdeaScale, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="1e776-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1e776-142">tooconfigure и теста Azure AD единого входа с IdeaScale, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1e776-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e776-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1e776-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e776-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1e776-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e776-145">**[Создание тестового пользователя, прошедшего IdeaScale](#creating-an-ideascale-test-user)**  -toohave аналог Саймон Britta в IdeaScale, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e776-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e776-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1e776-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e776-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1e776-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e776-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e776-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e776-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в свое приложение IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="1e776-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="1e776-150">**tooconfigure Azure AD единого входа с IdeaScale, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e776-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e776-151">В hello в hello портала Azure **IdeaScale** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1e776-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1e776-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e776-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="1e776-155">На hello **URL-адреса и домена IdeaScale** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e776-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="1e776-157">а.</span><span class="sxs-lookup"><span data-stu-id="1e776-157">a.</span></span> <span data-ttu-id="1e776-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="1e776-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="1e776-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e776-159">b.</span></span> <span data-ttu-id="1e776-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="1e776-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="1e776-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1e776-161">These values are not real.</span></span> <span data-ttu-id="1e776-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1e776-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e776-163">Обратитесь к [группа поддержки клиента IdeaScale](http://support.ideascale.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="1e776-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="1e776-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="1e776-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="1e776-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1e776-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e776-168">На hello **конфигурации IdeaScale** щелкните **Настройка IdeaScale** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="1e776-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1e776-169">Копировать hello **URL-адрес выхода и идентификатор сущности SAML** из hello **краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="1e776-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="1e776-171">В другом окне браузера войти в корпоративный сайт IdeaScale tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="1e776-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="1e776-172">Go слишком**параметры сообщества**.</span><span class="sxs-lookup"><span data-stu-id="1e776-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="1e776-173">![Параметры сообщества](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Параметры сообщества")</span><span class="sxs-lookup"><span data-stu-id="1e776-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="1e776-174">Go слишком**безопасности \> параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1e776-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="1e776-175">![Параметры единого входа](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="1e776-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="1e776-176">Выберите для параметра **Single-Signon Type** (Тип единого входа) значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="1e776-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="1e776-177">![Тип единого входа](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Тип единого входа")</span><span class="sxs-lookup"><span data-stu-id="1e776-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="1e776-178">На hello **параметры единого входа** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e776-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="1e776-179">![Параметры единого входа](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="1e776-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="1e776-180">а.</span><span class="sxs-lookup"><span data-stu-id="1e776-180">a.</span></span> <span data-ttu-id="1e776-181">В **идентификатор сущности поставщика удостоверений SAML** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1e776-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1e776-182">b.</span><span class="sxs-lookup"><span data-stu-id="1e776-182">b.</span></span> <span data-ttu-id="1e776-183">Скопируйте содержимое hello скачанный файл метаданных из портала Azure и вставьте его в hello **метаданные поставщика удостоверений SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="1e776-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="1e776-184">c.</span><span class="sxs-lookup"><span data-stu-id="1e776-184">c.</span></span> <span data-ttu-id="1e776-185">В **URL-адрес успешного выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1e776-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1e776-186">d.</span><span class="sxs-lookup"><span data-stu-id="1e776-186">d.</span></span> <span data-ttu-id="1e776-187">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="1e776-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1e776-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1e776-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1e776-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1e776-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1e776-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e776-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e776-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e776-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e776-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1e776-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1e776-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e776-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e776-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1e776-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e776-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1e776-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e776-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="1e776-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e776-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e776-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e776-203">а.</span><span class="sxs-lookup"><span data-stu-id="1e776-203">a.</span></span> <span data-ttu-id="1e776-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e776-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e776-205">b.</span><span class="sxs-lookup"><span data-stu-id="1e776-205">b.</span></span> <span data-ttu-id="1e776-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e776-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e776-207">c.</span><span class="sxs-lookup"><span data-stu-id="1e776-207">c.</span></span> <span data-ttu-id="1e776-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="1e776-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1e776-209">d.</span><span class="sxs-lookup"><span data-stu-id="1e776-209">d.</span></span> <span data-ttu-id="1e776-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1e776-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="1e776-211">Создание тестового пользователя IdeaScale</span><span class="sxs-lookup"><span data-stu-id="1e776-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="1e776-212">Пользователи toolog tooenable Azure AD в IdeaScale, их необходимо подготовить в tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="1e776-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="1e776-213">В случае IdeaScale hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="1e776-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="1e776-214">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e776-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e776-215">Войдите в tooyour **IdeaScale** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="1e776-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="1e776-216">Go слишком**параметры сообщества**.</span><span class="sxs-lookup"><span data-stu-id="1e776-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="1e776-217">![Параметры сообщества](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Параметры сообщества")</span><span class="sxs-lookup"><span data-stu-id="1e776-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="1e776-218">Go слишком**основные параметры \> элемента управления**.</span><span class="sxs-lookup"><span data-stu-id="1e776-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="1e776-219">Щелкните **Добавить участника**.</span><span class="sxs-lookup"><span data-stu-id="1e776-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="1e776-220">![Управление участниками](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Управление участниками")</span><span class="sxs-lookup"><span data-stu-id="1e776-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="1e776-221">В hello раздел добавить нового члена выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1e776-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1e776-222">![Добавление новой записи](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Добавление новой записи")</span><span class="sxs-lookup"><span data-stu-id="1e776-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="1e776-223">а.</span><span class="sxs-lookup"><span data-stu-id="1e776-223">a.</span></span> <span data-ttu-id="1e776-224">В hello **адреса электронной почты** текстовом поле введите адрес электронной почты hello действительной учетной записи AAD, вы хотите tooprovision.</span><span class="sxs-lookup"><span data-stu-id="1e776-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="1e776-225">b.</span><span class="sxs-lookup"><span data-stu-id="1e776-225">b.</span></span> <span data-ttu-id="1e776-226">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="1e776-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="1e776-227">Hello владельцем учетной записи Azure Active Directory получает сообщение электронной почты с помощью учетной записи ссылка tooconfirm hello, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="1e776-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="1e776-228">Можно использовать любые другие IdeaScale пользователя средства создания учетных записей или интерфейсы API, предоставляемые IdeaScale tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="1e776-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1e776-229">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1e776-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1e776-230">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooIdeaScale доступа.</span><span class="sxs-lookup"><span data-stu-id="1e776-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1e776-232">**tooassign tooIdeaScale Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e776-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e776-233">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e776-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1e776-235">В списке приложений hello выберите **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="1e776-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="1e776-237">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1e776-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1e776-239">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e776-239">Click **Add** button.</span></span> <span data-ttu-id="1e776-240">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1e776-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1e776-242">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1e776-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1e776-243">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1e776-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e776-244">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1e776-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e776-245">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1e776-245">Testing single sign-on</span></span>


<span data-ttu-id="1e776-246">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="1e776-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1e776-247">При нажатии кнопки hello IdeaScale плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="1e776-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e776-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1e776-248">Additional resources</span></span>

* [<span data-ttu-id="1e776-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e776-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e776-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e776-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

