---
title: "Руководство по интеграции Azure Active Directory с UNIFI | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="dbb33-103">Руководство по интеграции Azure Active Directory с UNIFI</span><span class="sxs-lookup"><span data-stu-id="dbb33-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="dbb33-104">В этом учебнике вы узнаете, как toointegrate UNIFI с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dbb33-104">In this tutorial, you learn how toointegrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dbb33-105">Интеграция с Azure AD UNIFI предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="dbb33-105">Integrating UNIFI with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dbb33-106">Можно управлять в Azure AD, имеющего доступ tooUNIFI</span><span class="sxs-lookup"><span data-stu-id="dbb33-106">You can control in Azure AD who has access tooUNIFI</span></span>
- <span data-ttu-id="dbb33-107">Можно включить на пользователей tooautomatically get вошедшего tooUNIFI (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbb33-107">You can enable your users tooautomatically get signed-on tooUNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dbb33-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="dbb33-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dbb33-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dbb33-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbb33-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dbb33-110">Prerequisites</span></span>

<span data-ttu-id="dbb33-111">tooconfigure интеграция Azure AD с UNIFI требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="dbb33-111">tooconfigure Azure AD integration with UNIFI, you need hello following items:</span></span>

- <span data-ttu-id="dbb33-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dbb33-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dbb33-113">подписка UNIFI с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dbb33-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dbb33-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="dbb33-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dbb33-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="dbb33-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dbb33-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dbb33-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dbb33-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbb33-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dbb33-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dbb33-118">Scenario description</span></span>
<span data-ttu-id="dbb33-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dbb33-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dbb33-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="dbb33-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dbb33-121">Добавление UNIFI из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dbb33-121">Adding UNIFI from hello gallery</span></span>
2. <span data-ttu-id="dbb33-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbb33-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-hello-gallery"></a><span data-ttu-id="dbb33-123">Добавление UNIFI из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dbb33-123">Adding UNIFI from hello gallery</span></span>
<span data-ttu-id="dbb33-124">tooconfigure hello интеграции UNIFI в Azure AD, вы должны tooadd UNIFI из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dbb33-124">tooconfigure hello integration of UNIFI into Azure AD, you need tooadd UNIFI from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dbb33-125">**tooadd UNIFI из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dbb33-125">**tooadd UNIFI from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbb33-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dbb33-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dbb33-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dbb33-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dbb33-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="dbb33-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dbb33-133">Введите в поле поиска hello **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-133">In hello search box, type **UNIFI**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="dbb33-135">В панели результатов hello выберите **UNIFI**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="dbb33-135">In hello results panel, select **UNIFI**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dbb33-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbb33-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dbb33-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение UNIFI с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbb33-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dbb33-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в UNIFI является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbb33-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UNIFI is tooa user in Azure AD.</span></span> <span data-ttu-id="dbb33-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в UNIFI должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="dbb33-140">In other words, a link relationship between an Azure AD user and hello related user in UNIFI needs toobe established.</span></span>

<span data-ttu-id="dbb33-141">В UNIFI, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="dbb33-141">In UNIFI, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dbb33-142">tooconfigure и теста Azure AD единого входа с UNIFI, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="dbb33-142">tooconfigure and test Azure AD single sign-on with UNIFI, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dbb33-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="dbb33-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dbb33-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="dbb33-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dbb33-145">**[Создание UNIFI тестовый пользователь](#creating-a-unifi-test-user)**  -toohave аналог Саймон Britta в UNIFI, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="dbb33-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - toohave a counterpart of Britta Simon in UNIFI that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dbb33-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="dbb33-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dbb33-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dbb33-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dbb33-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbb33-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dbb33-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении UNIFI.</span><span class="sxs-lookup"><span data-stu-id="dbb33-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="dbb33-150">**tooconfigure Azure AD единого входа с UNIFI, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dbb33-150">**tooconfigure Azure AD single sign-on with UNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbb33-151">В hello в hello портала Azure **UNIFI** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-151">In hello Azure portal, on hello **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dbb33-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="dbb33-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="dbb33-155">На hello **UNIFI доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="dbb33-155">On hello **UNIFI Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="dbb33-157">В hello **идентификатор** текстовое значение hello типа:`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="dbb33-157">In hello **Identifier** textbox, type hello value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="dbb33-158">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="dbb33-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="dbb33-160">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="dbb33-160">In hello **Sign-on URL** textbox, type hello URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="dbb33-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="dbb33-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="dbb33-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dbb33-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="dbb33-165">На hello **конфигурации UNIFI** щелкните **Настройка UNIFI** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="dbb33-165">On hello **UNIFI Configuration** section, click **Configure UNIFI** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dbb33-166">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="dbb33-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="dbb33-168">В другом окне браузера, войдите на tooyour **UNIFI** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="dbb33-168">In a different web browser window, sign on tooyour **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="dbb33-169">Щелкните hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-169">Click on hello **Users**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="dbb33-171">Щелкните hello **Добавление поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-171">Click on hello **Add New Identity Provider**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="dbb33-173">В hello **Добавление поставщика удостоверений** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dbb33-173">In hello **Add Identity Provider** section, perform hello following steps:</span></span>   

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="dbb33-175">а.</span><span class="sxs-lookup"><span data-stu-id="dbb33-175">a.</span></span> <span data-ttu-id="dbb33-176">В hello **имя поставщика** текстовое поле, имя типа hello hello поставщика удостоверений...</span><span class="sxs-lookup"><span data-stu-id="dbb33-176">In hello **Provider Name** textbox, type hello name of hello Identity Provider..</span></span>

    <span data-ttu-id="dbb33-177">b.</span><span class="sxs-lookup"><span data-stu-id="dbb33-177">b.</span></span> <span data-ttu-id="dbb33-178">В hello hello **URL-адрес поставщика** текстовое поле вставьте hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb33-178">In hello hello **Provider URL** textbox paste hello **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dbb33-179">c.</span><span class="sxs-lookup"><span data-stu-id="dbb33-179">c.</span></span> <span data-ttu-id="dbb33-180">Привет открыть сертификат, загруженный из hello портал Azure в блокноте, удалите hello **---BEGIN CERTIFICATE---** и **---конечный СЕРТИФИКАТ---** тега, а затем вставьте hello оставшееся содержимое Hello **сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="dbb33-180">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Certificate** textbox.</span></span>

    <span data-ttu-id="dbb33-181">d.</span><span class="sxs-lookup"><span data-stu-id="dbb33-181">d.</span></span> <span data-ttu-id="dbb33-182">Выберите hello **является поставщиком по умолчанию** флажок.</span><span class="sxs-lookup"><span data-stu-id="dbb33-182">Select hello **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="dbb33-183">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="dbb33-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dbb33-184">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="dbb33-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dbb33-185">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dbb33-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dbb33-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbb33-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="dbb33-187">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb33-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dbb33-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dbb33-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbb33-190">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dbb33-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dbb33-192">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dbb33-194">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="dbb33-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dbb33-196">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dbb33-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dbb33-198">а.</span><span class="sxs-lookup"><span data-stu-id="dbb33-198">a.</span></span> <span data-ttu-id="dbb33-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dbb33-200">b.</span><span class="sxs-lookup"><span data-stu-id="dbb33-200">b.</span></span> <span data-ttu-id="dbb33-201">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dbb33-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dbb33-202">c.</span><span class="sxs-lookup"><span data-stu-id="dbb33-202">c.</span></span> <span data-ttu-id="dbb33-203">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dbb33-204">d.</span><span class="sxs-lookup"><span data-stu-id="dbb33-204">d.</span></span> <span data-ttu-id="dbb33-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="dbb33-206">Создание тестового пользователя UNIFI</span><span class="sxs-lookup"><span data-stu-id="dbb33-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="dbb33-207">В этом разделе описано, как создать пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbb33-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="dbb33-208">Приложение **UNIFI** поддерживает автоматическую подготовку пользователей, поэтому действия вручную не требуются.</span><span class="sxs-lookup"><span data-stu-id="dbb33-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="dbb33-209">Пользователи создаются автоматически после успешной проверки подлинности из hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbb33-209">Users are created automatically after successful authentication from hello Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dbb33-210">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="dbb33-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dbb33-211">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooUNIFI доступа.</span><span class="sxs-lookup"><span data-stu-id="dbb33-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUNIFI.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dbb33-213">**tooassign tooUNIFI Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dbb33-213">**tooassign Britta Simon tooUNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbb33-214">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dbb33-216">В списке приложений hello выберите **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-216">In hello applications list, select **UNIFI**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="dbb33-218">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dbb33-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-220">Click **Add** button.</span></span> <span data-ttu-id="dbb33-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dbb33-223">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="dbb33-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dbb33-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dbb33-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dbb33-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dbb33-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dbb33-226">Testing single sign-on</span></span>

<span data-ttu-id="dbb33-227">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="dbb33-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dbb33-228">При нажатии кнопки UNIFI плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour UNIFI приложения.</span><span class="sxs-lookup"><span data-stu-id="dbb33-228">When you click hello UNIFI tile in hello Access Panel, you should get automatically signed-on tooyour UNIFI application.</span></span>
<span data-ttu-id="dbb33-229">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dbb33-229">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dbb33-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dbb33-230">Additional resources</span></span>

* [<span data-ttu-id="dbb33-231">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbb33-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dbb33-232">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dbb33-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

