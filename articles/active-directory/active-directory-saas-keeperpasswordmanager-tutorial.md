---
title: "Руководство по интеграции Azure Active Directory с Keeper Password Manager & Digital Vault | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и диспетчер паролей хранителю & цифровой хранилища."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="3d78d-103">Руководство по интеграции Azure Active Directory с Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="3d78d-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="3d78d-104">В этом учебнике вы узнаете, как toointegrate диспетчер паролей хранителю & цифровой хранилища в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d78d-104">In this tutorial, you learn how toointegrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d78d-105">Интеграция с Azure AD диспетчер паролей хранителю & цифровой хранилища предоставляет следующие преимущества hello:</span><span class="sxs-lookup"><span data-stu-id="3d78d-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3d78d-106">Можно управлять в Azure AD, имеющего доступ к tooKeeper диспетчер паролей & цифровой хранилища</span><span class="sxs-lookup"><span data-stu-id="3d78d-106">You can control in Azure AD who has access tooKeeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="3d78d-107">Вы можете включить их учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooKeeper диспетчер паролей & цифровой хранилища (Single Sign-On)</span><span class="sxs-lookup"><span data-stu-id="3d78d-107">You can enable your users tooautomatically get signed-on tooKeeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d78d-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3d78d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3d78d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d78d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d78d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3d78d-110">Prerequisites</span></span>

<span data-ttu-id="3d78d-111">tooconfigure интеграция Azure AD с диспетчер паролей хранителю & цифровой хранилища необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3d78d-111">tooconfigure Azure AD integration with Keeper Password Manager & Digital Vault, you need hello following items:</span></span>

- <span data-ttu-id="3d78d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3d78d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d78d-113">подписка на Keeper Password Manager & Digital Vault с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3d78d-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d78d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3d78d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d78d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3d78d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d78d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3d78d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d78d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d78d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d78d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3d78d-118">Scenario description</span></span>
<span data-ttu-id="3d78d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3d78d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d78d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3d78d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d78d-121">Добавление диспетчера паролей хранителю & цифровой хранилища из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3d78d-121">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
2. <span data-ttu-id="3d78d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d78d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a><span data-ttu-id="3d78d-123">Добавление диспетчера паролей хранителю & цифровой хранилища из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3d78d-123">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
<span data-ttu-id="3d78d-124">tooconfigure hello интеграции диспетчер паролей хранителю & цифровой хранилища в Azure AD, вы должны tooadd диспетчер паролей хранителю & цифровой хранилища из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3d78d-124">tooconfigure hello integration of Keeper Password Manager & Digital Vault into Azure AD, you need tooadd Keeper Password Manager & Digital Vault from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3d78d-125">**tooadd диспетчер паролей хранителю & цифровой хранилища из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3d78d-125">**tooadd Keeper Password Manager & Digital Vault from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d78d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3d78d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d78d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3d78d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3d78d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3d78d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3d78d-133">Введите в поле поиска hello **диспетчер паролей хранителю & хранилище цифровых**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-133">In hello search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="3d78d-135">В панели результатов hello выберите **диспетчер паролей хранителю & цифровой хранилище**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3d78d-135">In hello results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d78d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d78d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d78d-138">В этом разделе описана настройка и проверка единого входа Azure AD в Keeper Password Manager & Digital Vault с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d78d-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3d78d-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в диспетчер паролей хранителю & цифровой хранилища является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d78d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Keeper Password Manager & Digital Vault is tooa user in Azure AD.</span></span> <span data-ttu-id="3d78d-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в диспетчер паролей хранителю & цифровой хранилища должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3d78d-140">In other words, a link relationship between an Azure AD user and hello related user in Keeper Password Manager & Digital Vault needs toobe established.</span></span>

<span data-ttu-id="3d78d-141">В диспетчер паролей хранителю & цифровой хранилища, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="3d78d-141">In Keeper Password Manager & Digital Vault, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3d78d-142">tooconfigure и теста Azure AD единого входа с диспетчер паролей хранителю & цифровой хранилище, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="3d78d-142">tooconfigure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3d78d-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3d78d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3d78d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3d78d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d78d-145">**[Создание тестового пользователя диспетчер паролей хранителю & цифровой хранилище](#creating-a-keeperpasswordmanager-test-user)**  -toohave аналог Саймон Britta в диспетчер паролей хранителю & цифровой хранилища, которое представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3d78d-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - toohave a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d78d-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3d78d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d78d-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3d78d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d78d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d78d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d78d-149">В этом разделе Azure AD единым входом в портал Azure hello включить и настроить единый вход в приложение диспетчер паролей хранителю & цифровой хранилища.</span><span class="sxs-lookup"><span data-stu-id="3d78d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="3d78d-150">**tooconfigure Azure AD единого входа с диспетчер паролей хранителю & цифровой хранилища выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="3d78d-150">**tooconfigure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d78d-151">В hello в hello портала Azure **диспетчер паролей хранителю & цифровой хранилище** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-151">In hello Azure portal, on hello **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3d78d-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3d78d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="3d78d-155">На hello **диспетчер паролей хранителю & цифровой хранилище домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3d78d-155">On hello **Keeper Password Manager & Digital Vault Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="3d78d-157">а.</span><span class="sxs-lookup"><span data-stu-id="3d78d-157">a.</span></span> <span data-ttu-id="3d78d-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="3d78d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="3d78d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3d78d-159">b.</span></span> <span data-ttu-id="3d78d-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="3d78d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="3d78d-161">c.</span><span class="sxs-lookup"><span data-stu-id="3d78d-161">c.</span></span> <span data-ttu-id="3d78d-162">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="3d78d-162">In hello **Identifier** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d78d-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3d78d-163">These values are not real.</span></span> <span data-ttu-id="3d78d-164">Обновите эти значения с hello фактический URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="3d78d-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3d78d-165">Обратитесь к [диспетчер паролей хранителю & цифровой клиентов хранилища поддержки](https://keepersecurity.com/contact.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="3d78d-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="3d78d-166">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3d78d-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="3d78d-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3d78d-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3d78d-170">На hello **диспетчер паролей хранителю & цифровой настройки хранилища** щелкните **настроить диспетчер паролей хранителю & цифровой хранилище** tooopen **Настройкавхода**окна.</span><span class="sxs-lookup"><span data-stu-id="3d78d-170">On hello **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3d78d-171">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="3d78d-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="3d78d-173">tooconfigure единого входа на **диспетчер паролей хранителю & цифровой настройки хранилища** стороны, выполните рекомендации hello, предоставленных во [хранителю руководство](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="3d78d-173">tooconfigure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow hello guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="3d78d-174">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3d78d-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3d78d-175">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3d78d-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3d78d-176">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d78d-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d78d-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d78d-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d78d-178">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3d78d-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3d78d-180">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3d78d-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d78d-181">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3d78d-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d78d-183">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d78d-185">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="3d78d-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d78d-187">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3d78d-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d78d-189">а.</span><span class="sxs-lookup"><span data-stu-id="3d78d-189">a.</span></span> <span data-ttu-id="3d78d-190">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d78d-191">b.</span><span class="sxs-lookup"><span data-stu-id="3d78d-191">b.</span></span> <span data-ttu-id="3d78d-192">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3d78d-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d78d-193">c.</span><span class="sxs-lookup"><span data-stu-id="3d78d-193">c.</span></span> <span data-ttu-id="3d78d-194">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3d78d-195">d.</span><span class="sxs-lookup"><span data-stu-id="3d78d-195">d.</span></span> <span data-ttu-id="3d78d-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="3d78d-197">Создание тестового пользователя Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="3d78d-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="3d78d-198">Пользователи toolog tooenable Azure AD в tooKeeper диспетчер паролей & цифровой хранилища, их необходимо подготовить в диспетчер паролей хранителю & цифровой хранилища.</span><span class="sxs-lookup"><span data-stu-id="3d78d-198">tooenable Azure AD users toolog in tooKeeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="3d78d-199">В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение.</span><span class="sxs-lookup"><span data-stu-id="3d78d-199">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="3d78d-200">Вы можете связаться [поддержки хранителю](https://keepersecurity.com/contact.html), если пользователи toosetup вручную.</span><span class="sxs-lookup"><span data-stu-id="3d78d-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want toosetup users manually.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3d78d-201">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3d78d-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3d78d-202">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа к tooKeeper диспетчер паролей & цифровой хранилища.</span><span class="sxs-lookup"><span data-stu-id="3d78d-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKeeper Password Manager & Digital Vault.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3d78d-204">**tooassign tooKeeper Britta Simon диспетчер паролей & цифровой хранилища выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="3d78d-204">**tooassign Britta Simon tooKeeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d78d-205">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3d78d-207">В списке приложений hello выберите **диспетчер паролей хранителю & хранилище цифровых**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-207">In hello applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="3d78d-209">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3d78d-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-211">Click **Add** button.</span></span> <span data-ttu-id="3d78d-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3d78d-214">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3d78d-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3d78d-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d78d-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3d78d-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d78d-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3d78d-217">Testing single sign-on</span></span>

<span data-ttu-id="3d78d-218">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="3d78d-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3d78d-219">При нажатии кнопки hello диспетчер паролей хранителю & цифровой хранилище плитки в панели доступа hello, вы должны получить страницы входа диспетчер паролей хранителю & цифровой хранилища приложения.</span><span class="sxs-lookup"><span data-stu-id="3d78d-219">When you click hello Keeper Password Manager & Digital Vault tile in hello Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="3d78d-220">После успешной проверки подлинности должно появиться в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="3d78d-220">Upon successful authentication, you should get into hello application.</span></span> <span data-ttu-id="3d78d-221">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d78d-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3d78d-222">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3d78d-222">Additional resources</span></span>

* [<span data-ttu-id="3d78d-223">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d78d-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d78d-224">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d78d-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

