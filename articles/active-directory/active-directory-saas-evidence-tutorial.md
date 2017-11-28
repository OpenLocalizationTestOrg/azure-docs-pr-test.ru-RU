---
title: "Учебник. Интеграция Azure Active Directory с Evidence.com | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="1e220-103">Руководство. Интеграция Azure Active Directory с Evidence.com</span><span class="sxs-lookup"><span data-stu-id="1e220-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="1e220-104">В этом учебнике вы узнаете, как toointegrate Evidence.com с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e220-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e220-105">Интеграция с Azure AD Evidence.com предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1e220-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e220-106">Можно управлять в Azure AD, имеющего доступ tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="1e220-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="1e220-107">Можно включить на пользователей tooautomatically get вошедшего tooEvidence.com (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e220-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1e220-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1e220-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1e220-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e220-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e220-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1e220-110">Prerequisites</span></span>

<span data-ttu-id="1e220-111">tooconfigure интеграция Azure AD с Evidence.com требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1e220-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="1e220-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1e220-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e220-113">Подписка Evidence.com с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e220-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e220-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1e220-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e220-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1e220-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e220-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1e220-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e220-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e220-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e220-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1e220-118">Scenario description</span></span>
<span data-ttu-id="1e220-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1e220-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e220-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1e220-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e220-121">Добавление Evidence.com из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1e220-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="1e220-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e220-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="1e220-123">Добавление Evidence.com из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1e220-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="1e220-124">tooconfigure hello интеграции Evidence.com в Azure AD, вы должны tooadd Evidence.com из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e220-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e220-125">**tooadd Evidence.com из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e220-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e220-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1e220-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="1e220-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1e220-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1e220-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e220-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="1e220-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1e220-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="1e220-133">Введите в поле поиска hello **Evidence.com**выберите **Evidence.com** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1e220-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evidence.com в списке результатов hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1e220-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e220-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1e220-136">В этом разделе описана настройка и проверка единого входа Azure AD в Evidence.com с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e220-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e220-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Evidence.com является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e220-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="1e220-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Evidence.com должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="1e220-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="1e220-139">В Evidence.com, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="1e220-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1e220-140">tooconfigure и теста Azure AD единого входа с Evidence.com, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1e220-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e220-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1e220-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e220-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1e220-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e220-143">**[Создание тестового пользователя Evidence.com](#create-a-evidencecom-test-user)**  -toohave аналог Саймон Britta в Evidence.com, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e220-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e220-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1e220-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e220-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1e220-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1e220-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e220-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1e220-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="1e220-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="1e220-148">**tooconfigure Azure AD единого входа с Evidence.com, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e220-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e220-149">В hello в hello портала Azure **Evidence.com** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1e220-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="1e220-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e220-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="1e220-153">На hello **URL-адреса и домена Evidence.com** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e220-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="1e220-155">а.</span><span class="sxs-lookup"><span data-stu-id="1e220-155">a.</span></span> <span data-ttu-id="1e220-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="1e220-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="1e220-157">b.</span><span class="sxs-lookup"><span data-stu-id="1e220-157">b.</span></span> <span data-ttu-id="1e220-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="1e220-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e220-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1e220-159">These values are not real.</span></span> <span data-ttu-id="1e220-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1e220-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e220-161">Обратитесь к [группа поддержки клиента Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="1e220-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="1e220-162">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="1e220-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="1e220-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1e220-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e220-166">На hello **конфигурации Evidence.com** щелкните **Настройка Evidence.com** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="1e220-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1e220-167">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="1e220-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="1e220-169">В отдельном окне браузера, tooyour входа Evidence.com клиента с правами администратора и перейдите слишком**администратора** вкладка</span><span class="sxs-lookup"><span data-stu-id="1e220-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="1e220-170">Щелкните **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="1e220-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="1e220-171">Выберите параметр **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="1e220-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="1e220-172">Копировать hello **идентификатор сущности SAML**, **SAML единого входа URL-адрес службы** и **URL-адрес выхода** значения, отображаемые в hello портал Azure и соответствующих полей toohello Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="1e220-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="1e220-173">Откройте скачанный файл Certificate(Base64) в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат безопасности** поле.</span><span class="sxs-lookup"><span data-stu-id="1e220-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="1e220-174">Сохранение конфигурации hello в Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="1e220-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="1e220-175">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1e220-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1e220-176">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1e220-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1e220-177">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e220-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1e220-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e220-178">Create an Azure AD test user</span></span>

<span data-ttu-id="1e220-179">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1e220-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="1e220-181">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e220-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e220-182">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="1e220-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1e220-184">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1e220-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1e220-186">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="1e220-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1e220-188">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1e220-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1e220-190">а.</span><span class="sxs-lookup"><span data-stu-id="1e220-190">a.</span></span> <span data-ttu-id="1e220-191">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e220-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e220-192">b.</span><span class="sxs-lookup"><span data-stu-id="1e220-192">b.</span></span> <span data-ttu-id="1e220-193">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1e220-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1e220-194">c.</span><span class="sxs-lookup"><span data-stu-id="1e220-194">c.</span></span> <span data-ttu-id="1e220-195">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="1e220-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1e220-196">d.</span><span class="sxs-lookup"><span data-stu-id="1e220-196">d.</span></span> <span data-ttu-id="1e220-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1e220-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="1e220-198">Создание тестового пользователя Evidence.com</span><span class="sxs-lookup"><span data-stu-id="1e220-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="1e220-199">Azure AD пользователи toobe может toosign в их необходимо подготовить для доступа внутри hello Evidence.com приложения.</span><span class="sxs-lookup"><span data-stu-id="1e220-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="1e220-200">В этом разделе описывается, как учетные записи пользователей Azure AD toocreate внутри Evidence.com</span><span class="sxs-lookup"><span data-stu-id="1e220-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="1e220-201">**tooprovision учетной записи пользователя в Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="1e220-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="1e220-202">В окне веб-браузера войдите на корпоративный веб-сайт Evidence.com в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="1e220-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="1e220-203">Перейдите в слишком**администратора** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1e220-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="1e220-204">Щелкните **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="1e220-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="1e220-205">Нажмите кнопку hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="1e220-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="1e220-206">Hello **адрес электронной почты** hello added пользователя должно соответствовать пользователя hello hello пользователей в Azure AD, который вы хотите toogive доступа.</span><span class="sxs-lookup"><span data-stu-id="1e220-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="1e220-207">Если hello имя пользователя и адрес электронной почты не являются hello одинакового значения в вашей организации, можно использовать hello **Evidence.com > атрибуты > Single Sign-On** раздел hello Azure портала toochange hello nameidenitifer отправки адрес электронной почты tooEvidence.com toobe hello.</span><span class="sxs-lookup"><span data-stu-id="1e220-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1e220-208">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1e220-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1e220-209">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooEvidence.com доступа.</span><span class="sxs-lookup"><span data-stu-id="1e220-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="1e220-211">**tooassign tooEvidence.com Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1e220-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e220-212">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e220-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1e220-214">В списке приложений hello выберите **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="1e220-214">In hello applications list, select **Evidence.com**.</span></span>

    ![ссылка Evidence.com Hello в списке приложений hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="1e220-216">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1e220-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="1e220-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e220-218">Click **Add** button.</span></span> <span data-ttu-id="1e220-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1e220-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="1e220-221">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1e220-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1e220-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1e220-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e220-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1e220-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1e220-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1e220-224">Test single sign-on</span></span>

<span data-ttu-id="1e220-225">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="1e220-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1e220-226">При нажатии кнопки hello Evidence.com плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Evidence.com приложения.</span><span class="sxs-lookup"><span data-stu-id="1e220-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="1e220-227">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e220-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1e220-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1e220-228">Additional resources</span></span>

* [<span data-ttu-id="1e220-229">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e220-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e220-230">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e220-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

