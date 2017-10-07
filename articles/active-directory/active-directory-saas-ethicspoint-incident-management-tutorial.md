---
title: "Руководство. Интеграция Azure Active Directory с решением EthicsPoint Incident Management (EPIM) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Управление инцидентами EthicsPoint (EPIM)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 73ef5fab815cddb3728f4b23173f99e62aec5bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="174ff-103">Руководство. Интеграция Azure Active Directory с решением EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="174ff-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="174ff-104">В этом учебнике вы узнаете, как toointegrate управления инцидентами EthicsPoint (EPIM) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="174ff-104">In this tutorial, you learn how toointegrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="174ff-105">Интеграция управления инцидентами EthicsPoint (EPIM) с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="174ff-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="174ff-106">Можно управлять в Azure AD, имеющего доступ tooEthicsPoint инцидент управления (EPIM)</span><span class="sxs-lookup"><span data-stu-id="174ff-106">You can control in Azure AD who has access tooEthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="174ff-107">Ваш пользователей tooautomatically get вошедшего tooEthicsPoint инцидент управления (EPIM) (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="174ff-107">You can enable your users tooautomatically get signed-on tooEthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="174ff-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="174ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="174ff-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="174ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="174ff-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="174ff-110">Prerequisites</span></span>

<span data-ttu-id="174ff-111">tooconfigure интеграция Azure AD с помощью управления инцидентами EthicsPoint (EPIM) требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="174ff-111">tooconfigure Azure AD integration with EthicsPoint Incident Management (EPIM), you need hello following items:</span></span>

- <span data-ttu-id="174ff-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="174ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="174ff-113">подписка EthicsPoint Incident Management (EPIM) с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="174ff-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="174ff-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="174ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="174ff-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="174ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="174ff-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="174ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="174ff-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="174ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="174ff-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="174ff-118">Scenario description</span></span>
<span data-ttu-id="174ff-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="174ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="174ff-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="174ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="174ff-121">Добавление управления инцидентами EthicsPoint (EPIM) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="174ff-121">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
2. <span data-ttu-id="174ff-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="174ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-hello-gallery"></a><span data-ttu-id="174ff-123">Добавление управления инцидентами EthicsPoint (EPIM) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="174ff-123">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
<span data-ttu-id="174ff-124">tooconfigure hello Интеграция управления инцидентами в EthicsPoint (EPIM) в Azure AD, вы должны tooadd управления инцидентами EthicsPoint (EPIM) из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="174ff-124">tooconfigure hello integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need tooadd EthicsPoint Incident Management (EPIM) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="174ff-125">**tooadd управления инцидентами EthicsPoint (EPIM) из коллекции hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="174ff-125">**tooadd EthicsPoint Incident Management (EPIM) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="174ff-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="174ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="174ff-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="174ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="174ff-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="174ff-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="174ff-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="174ff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="174ff-133">Введите в поле поиска hello **управления инцидентами EthicsPoint (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="174ff-133">In hello search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="174ff-135">В панели результатов hello выберите **управления инцидентами EthicsPoint (EPIM)**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="174ff-135">In hello results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="174ff-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="174ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="174ff-138">В этом разделе описывается настройка и проверка единого входа Azure AD в EthicsPoint Incident Management (EPIM) с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="174ff-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="174ff-139">Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello инцидент управления EthicsPoint (EPIM) является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="174ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EthicsPoint Incident Management (EPIM) is tooa user in Azure AD.</span></span> <span data-ttu-id="174ff-140">Иными словами связи между пользователя Azure AD и связанных пользователей hello инцидент управления EthicsPoint (EPIM) необходимо установить toobe.</span><span class="sxs-lookup"><span data-stu-id="174ff-140">In other words, a link relationship between an Azure AD user and hello related user in EthicsPoint Incident Management (EPIM) needs toobe established.</span></span>

<span data-ttu-id="174ff-141">В Управление инцидентами EthicsPoint (EPIM), присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="174ff-141">In EthicsPoint Incident Management (EPIM), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="174ff-142">tooconfigure и тестирования Azure AD единого входа с помощью управления инцидентами EthicsPoint (EPIM), необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="174ff-142">tooconfigure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="174ff-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="174ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="174ff-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="174ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="174ff-145">**[Создание тестового пользователя управления инцидентами EthicsPoint (EPIM)](#creating-a-ethicspoint-incident-management-epim-test-user)**  -toohave аналог Саймон Britta в EthicsPoint инцидент управления (EPIM), являющийся представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="174ff-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - toohave a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="174ff-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="174ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="174ff-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="174ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="174ff-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="174ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="174ff-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении управления инцидентами EthicsPoint (EPIM).</span><span class="sxs-lookup"><span data-stu-id="174ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="174ff-150">**tooconfigure Azure AD единого входа с помощью управления инцидентами EthicsPoint (EPIM), выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="174ff-150">**tooconfigure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="174ff-151">В hello в hello портала Azure **управления инцидентами EthicsPoint (EPIM)** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="174ff-151">In hello Azure portal, on hello **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="174ff-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="174ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="174ff-155">На hello **URL-адреса и домена управления инцидентами EthicsPoint (EPIM)** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="174ff-155">On hello **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="174ff-157">а.</span><span class="sxs-lookup"><span data-stu-id="174ff-157">a.</span></span> <span data-ttu-id="174ff-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="174ff-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="174ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="174ff-159">b.</span></span> <span data-ttu-id="174ff-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="174ff-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="174ff-161">c.</span><span class="sxs-lookup"><span data-stu-id="174ff-161">c.</span></span> <span data-ttu-id="174ff-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="174ff-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="174ff-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="174ff-163">These values are not real.</span></span> <span data-ttu-id="174ff-164">Обновите эти значения с hello фактический URL-адрес ответа, идентификатора и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="174ff-164">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="174ff-165">Обратитесь к [группа поддержки клиента для управления инцидентами EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="174ff-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="174ff-166">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="174ff-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="174ff-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="174ff-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="174ff-170">tooconfigure единого входа на **управления инцидентами EthicsPoint (EPIM)** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки управления инцидентами EthicsPoint (EPIM) команда](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="174ff-170">tooconfigure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need toosend hello downloaded **Metadata XML** too[EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="174ff-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="174ff-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="174ff-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="174ff-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="174ff-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="174ff-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="174ff-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="174ff-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="174ff-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="174ff-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="174ff-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="174ff-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="174ff-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="174ff-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="174ff-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="174ff-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="174ff-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="174ff-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="174ff-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="174ff-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="174ff-186">а.</span><span class="sxs-lookup"><span data-stu-id="174ff-186">a.</span></span> <span data-ttu-id="174ff-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="174ff-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="174ff-188">b.</span><span class="sxs-lookup"><span data-stu-id="174ff-188">b.</span></span> <span data-ttu-id="174ff-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="174ff-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="174ff-190">c.</span><span class="sxs-lookup"><span data-stu-id="174ff-190">c.</span></span> <span data-ttu-id="174ff-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="174ff-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="174ff-192">d.</span><span class="sxs-lookup"><span data-stu-id="174ff-192">d.</span></span> <span data-ttu-id="174ff-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="174ff-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="174ff-194">Создание тестового пользователя EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="174ff-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="174ff-195">В этом разделе описано, как создать пользователя Britta Simon в EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="174ff-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="174ff-196">Можно работать с [группа поддержки управления инцидентами EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooadd пользователей hello hello платформы управления инцидентами EthicsPoint (EPIM).</span><span class="sxs-lookup"><span data-stu-id="174ff-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) tooadd hello users in hello EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="174ff-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="174ff-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="174ff-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooEthicsPoint инцидент управления (EPIM).</span><span class="sxs-lookup"><span data-stu-id="174ff-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEthicsPoint Incident Management (EPIM).</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="174ff-200">**tooassign tooEthicsPoint Britta Simon инцидент управления (EPIM) выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="174ff-200">**tooassign Britta Simon tooEthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="174ff-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="174ff-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="174ff-203">В списке приложений hello выберите **управления инцидентами EthicsPoint (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="174ff-203">In hello applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="174ff-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="174ff-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="174ff-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="174ff-207">Click **Add** button.</span></span> <span data-ttu-id="174ff-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="174ff-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="174ff-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="174ff-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="174ff-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="174ff-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="174ff-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="174ff-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="174ff-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="174ff-213">Testing single sign-on</span></span>

<span data-ttu-id="174ff-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="174ff-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="174ff-215">При нажатии кнопки hello управления инцидентами EthicsPoint (EPIM) плитки в панели доступа hello, вы должны получить приложения автоматически вошедшего tooyour управления инцидентами EthicsPoint (EPIM).</span><span class="sxs-lookup"><span data-stu-id="174ff-215">When you click hello EthicsPoint Incident Management (EPIM) tile in hello Access Panel, you should get automatically signed-on tooyour EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="174ff-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="174ff-216">Additional resources</span></span>

* [<span data-ttu-id="174ff-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="174ff-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="174ff-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="174ff-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

