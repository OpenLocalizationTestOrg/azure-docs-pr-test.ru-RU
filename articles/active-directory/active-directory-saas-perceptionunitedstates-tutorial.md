---
title: "Руководство по интеграции Azure Active Directory с Perception United States (Non-UltiPro) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и восприятия США (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="79628-103">Руководство по интеграции Azure Active Directory с Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="79628-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="79628-104">В этом учебнике вы узнаете, как toointegrate восприятии United States (Non-UltiPro) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79628-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79628-105">Интеграция впечатление США (Non-UltiPro) с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="79628-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79628-106">Можно управлять в Azure AD, имеющего доступ tooPerception США (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79628-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="79628-107">Можно включить на пользователей tooautomatically get вошедшего tooPerception США (Non-UltiPro) (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79628-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="79628-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="79628-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="79628-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79628-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79628-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="79628-110">Prerequisites</span></span>

<span data-ttu-id="79628-111">tooconfigure интеграция Azure AD с впечатление США (Non-UltiPro) требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="79628-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="79628-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="79628-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79628-113">подписка Perception United States (Non-UltiPro) с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="79628-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79628-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="79628-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79628-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="79628-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79628-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="79628-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79628-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79628-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79628-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="79628-118">Scenario description</span></span>
<span data-ttu-id="79628-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="79628-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79628-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="79628-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79628-121">Добавление впечатление США (Non-UltiPro) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="79628-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="79628-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="79628-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="79628-123">Добавление впечатление США (Non-UltiPro) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="79628-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="79628-124">tooconfigure hello интеграции для восприятия США (Non-UltiPro) в Azure AD, вы должны tooadd восприятии США (Non-UltiPro) из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="79628-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79628-125">**tooadd восприятии United States (Non-UltiPro) из коллекции hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="79628-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79628-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="79628-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="79628-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="79628-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79628-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="79628-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="79628-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="79628-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="79628-133">Введите в поле поиска hello **восприятия США (Non-UltiPro)**выберите **восприятия США (Non-UltiPro)** из панели результатов щелкните **добавить** tooadd кнопку приложение Hello.</span><span class="sxs-lookup"><span data-stu-id="79628-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Впечатление United States (Non-UltiPro) в списке результатов hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="79628-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="79628-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="79628-136">В этом разделе описана настройка и проверка единого входа Azure AD в Perception United States (Non-UltiPro) с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79628-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79628-137">Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello в восприятии США (Non-UltiPro) является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79628-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="79628-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в восприятии США (Non-UltiPro) должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="79628-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="79628-139">В восприятии США (Non-UltiPro), присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="79628-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="79628-140">tooconfigure и тестирования Azure AD единого входа с впечатление США (Non-UltiPro), необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="79628-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79628-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="79628-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79628-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="79628-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79628-143">**[Создание тестового пользователя впечатление США (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave аналог Саймон Britta в восприятии США (Non-UltiPro), являющийся представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="79628-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79628-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="79628-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79628-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="79628-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="79628-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="79628-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="79628-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении впечатление США (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79628-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="79628-148">**tooconfigure Azure AD единого входа с впечатление США (Non-UltiPro), выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="79628-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="79628-149">В hello в hello портала Azure **восприятии США (Non-UltiPro)** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="79628-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="79628-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="79628-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="79628-153">На hello **URL-адреса и домена впечатление США (Non-UltiPro)** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="79628-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="79628-155">а.</span><span class="sxs-lookup"><span data-stu-id="79628-155">a.</span></span> <span data-ttu-id="79628-156">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="79628-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="79628-157">b.</span><span class="sxs-lookup"><span data-stu-id="79628-157">b.</span></span> <span data-ttu-id="79628-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="79628-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79628-159">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="79628-159">hello value is not real.</span></span> <span data-ttu-id="79628-160">Значение hello будет обновляться hello фактический URL-адрес ответа, который описывается далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="79628-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="79628-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="79628-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="79628-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="79628-163">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79628-165">На hello **конфигурации впечатление США (Non-UltiPro)** щелкните **настройки восприятия США (Non-UltiPro)** tooopen **Настройка входа** окно.</span><span class="sxs-lookup"><span data-stu-id="79628-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="79628-166">Копировать hello **идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="79628-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="79628-167">а.</span><span class="sxs-lookup"><span data-stu-id="79628-167">a.</span></span> <span data-ttu-id="79628-168">Hello **восприятия США (Non-UltiPro)** приложению hello **идентификатор сущности SAML** закодированный toobe uri значение, которое вы скопировали.</span><span class="sxs-lookup"><span data-stu-id="79628-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="79628-169">значения uri кодируются tooget hello, используйте hello следующей ссылке:**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="79628-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="79628-170">b.</span><span class="sxs-lookup"><span data-stu-id="79628-170">b.</span></span> <span data-ttu-id="79628-171">После получения hello uri закодированное значение совместно с hello **URL-адрес ответа** описанным ниже -</span><span class="sxs-lookup"><span data-stu-id="79628-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="79628-172">c.</span><span class="sxs-lookup"><span data-stu-id="79628-172">c.</span></span> <span data-ttu-id="79628-173">Вставить hello выше значения в hello **URL-адрес ответа** текстовое поле в **URL-адреса и домена впечатление США (Non-UltiPro)** раздела.</span><span class="sxs-lookup"><span data-stu-id="79628-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Настройка Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="79628-175">В другом окне браузера Войдите на сайт компании tooyour восприятии США (Non-UltiPro) с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="79628-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="79628-176">На главной панели инструментов hello, щелкните **параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="79628-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Пользователь Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="79628-178">На hello **параметры учетной записи** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="79628-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Пользователь Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="79628-180">а.</span><span class="sxs-lookup"><span data-stu-id="79628-180">a.</span></span> <span data-ttu-id="79628-181">В hello **название компании** в текстовое поле имя типа hello hello **компании**.</span><span class="sxs-lookup"><span data-stu-id="79628-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="79628-182">b.</span><span class="sxs-lookup"><span data-stu-id="79628-182">b.</span></span> <span data-ttu-id="79628-183">В hello **имя учетной записи** в текстовое поле имя типа hello hello **учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="79628-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="79628-184">c.</span><span class="sxs-lookup"><span data-stu-id="79628-184">c.</span></span> <span data-ttu-id="79628-185">В **ответа по умолчанию-tooEmail** текстовое поле, тип hello допустимым **электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="79628-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="79628-186">d.</span><span class="sxs-lookup"><span data-stu-id="79628-186">d.</span></span> <span data-ttu-id="79628-187">Выберите для параметра **SSO Identity Provider** (Поставщик удостоверений единого входа) значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="79628-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="79628-188">На hello **Настройка единого входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="79628-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![Настройка единого входа Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="79628-190">а.</span><span class="sxs-lookup"><span data-stu-id="79628-190">a.</span></span> <span data-ttu-id="79628-191">Выберите для параметра **SAML NameID Type** (Тип NameID SAML) значение **EMAIL** (Электронная почта).</span><span class="sxs-lookup"><span data-stu-id="79628-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="79628-192">b.</span><span class="sxs-lookup"><span data-stu-id="79628-192">b.</span></span> <span data-ttu-id="79628-193">В hello **имя конфигурации единого входа** в текстовое поле имя типа hello вашей **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="79628-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="79628-194">c.</span><span class="sxs-lookup"><span data-stu-id="79628-194">c.</span></span> <span data-ttu-id="79628-195">В **имя поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="79628-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="79628-196">d.</span><span class="sxs-lookup"><span data-stu-id="79628-196">d.</span></span> <span data-ttu-id="79628-197">В **текстовое поле для домена SAML**, введите домен hello как  **@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="79628-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="79628-198">д.</span><span class="sxs-lookup"><span data-stu-id="79628-198">e.</span></span> <span data-ttu-id="79628-199">Щелкните **попытку отправить** tooupload hello **метаданные в формате XML** файла.</span><span class="sxs-lookup"><span data-stu-id="79628-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="79628-200">f.</span><span class="sxs-lookup"><span data-stu-id="79628-200">f.</span></span> <span data-ttu-id="79628-201">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="79628-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="79628-202">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="79628-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79628-203">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="79628-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79628-204">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79628-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="79628-205">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="79628-205">Create an Azure AD test user</span></span>

<span data-ttu-id="79628-206">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="79628-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="79628-208">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="79628-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79628-209">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="79628-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="79628-211">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="79628-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="79628-213">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="79628-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="79628-215">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="79628-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="79628-217">а.</span><span class="sxs-lookup"><span data-stu-id="79628-217">a.</span></span> <span data-ttu-id="79628-218">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79628-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79628-219">b.</span><span class="sxs-lookup"><span data-stu-id="79628-219">b.</span></span> <span data-ttu-id="79628-220">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="79628-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="79628-221">c.</span><span class="sxs-lookup"><span data-stu-id="79628-221">c.</span></span> <span data-ttu-id="79628-222">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="79628-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="79628-223">d.</span><span class="sxs-lookup"><span data-stu-id="79628-223">d.</span></span> <span data-ttu-id="79628-224">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="79628-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="79628-225">Создание тестового пользователя Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="79628-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="79628-226">В этом разделе описано, как создать пользователя Britta Simon в приложении Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79628-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="79628-227">Работать с [группа поддержки впечатление США (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello пользователей на платформе hello впечатление США (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79628-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="79628-228">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="79628-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="79628-229">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooPerception США (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="79628-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="79628-231">**tooassign Britta Simon tooPerception США (Non-UltiPro) выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="79628-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="79628-232">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="79628-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="79628-234">В списке приложений hello выберите **восприятии США (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="79628-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![ссылка впечатление США (Non-UltiPro) Hello в списке приложений hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="79628-236">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="79628-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="79628-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="79628-238">Click **Add** button.</span></span> <span data-ttu-id="79628-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="79628-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="79628-241">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="79628-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79628-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="79628-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79628-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="79628-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="79628-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="79628-244">Test single sign-on</span></span>

<span data-ttu-id="79628-245">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="79628-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79628-246">При нажатии кнопки hello впечатление США (Non-UltiPro) плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на восприятие США (Non-UltiPro) приложения.</span><span class="sxs-lookup"><span data-stu-id="79628-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="79628-247">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79628-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="79628-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="79628-248">Additional resources</span></span>

* [<span data-ttu-id="79628-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79628-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79628-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79628-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

