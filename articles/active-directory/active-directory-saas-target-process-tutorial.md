---
title: "Руководство по интеграции Azure Active Directory с TargetProcess | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="e1250-103">Руководство. Интеграция Azure Active Directory с TargetProcess</span><span class="sxs-lookup"><span data-stu-id="e1250-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="e1250-104">В этом учебнике вы узнаете, как toointegrate TargetProcess с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1250-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1250-105">Интеграция с Azure AD TargetProcess предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e1250-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1250-106">Можно управлять в Azure AD, имеющего доступ tooTargetProcess</span><span class="sxs-lookup"><span data-stu-id="e1250-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="e1250-107">Можно включить на пользователей tooautomatically get вошедшего tooTargetProcess (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1250-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1250-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e1250-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e1250-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1250-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1250-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e1250-110">Prerequisites</span></span>

<span data-ttu-id="e1250-111">tooconfigure интеграция Azure AD с TargetProcess требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="e1250-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="e1250-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e1250-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1250-113">подписка TargetProcess с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e1250-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1250-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e1250-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1250-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="e1250-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1250-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e1250-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1250-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1250-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1250-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e1250-118">Scenario description</span></span>
<span data-ttu-id="e1250-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e1250-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1250-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="e1250-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1250-121">Добавление TargetProcess из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="e1250-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="e1250-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1250-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="e1250-123">Добавление TargetProcess из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="e1250-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="e1250-124">tooconfigure hello интеграции TargetProcess в Azure AD, вы должны tooadd TargetProcess из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e1250-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1250-125">**tooadd TargetProcess из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e1250-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1250-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e1250-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1250-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="e1250-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1250-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e1250-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e1250-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e1250-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e1250-133">Введите в поле поиска hello **TargetProcess**выберите **TargetProcess** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e1250-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Добавление TargetProcess из коллекции](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e1250-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1250-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e1250-136">В этом разделе описана настройка и проверка единого входа Azure AD в TargetProcess с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1250-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1250-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в TargetProcess является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1250-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="e1250-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в TargetProcess должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="e1250-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="e1250-139">В TargetProcess, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="e1250-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e1250-140">tooconfigure и теста Azure AD единого входа с TargetProcess, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e1250-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1250-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="e1250-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1250-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e1250-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1250-143">**[Создание тестового пользователя TargetProcess](#create-a-targetprocess-test-user)**  -toohave аналог Саймон Britta в TargetProcess, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e1250-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1250-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="e1250-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1250-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e1250-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e1250-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1250-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e1250-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="e1250-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="e1250-148">**tooconfigure Azure AD единого входа с TargetProcess, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e1250-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1250-149">В hello в hello портала Azure **TargetProcess** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e1250-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e1250-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="e1250-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="e1250-153">На hello **URL-адреса и домена TargetProcess** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e1250-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Раздел "Домены и URL-адреса приложения TargetProcess"](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="e1250-155">а.</span><span class="sxs-lookup"><span data-stu-id="e1250-155">a.</span></span> <span data-ttu-id="e1250-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="e1250-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="e1250-157">b.</span><span class="sxs-lookup"><span data-stu-id="e1250-157">b.</span></span> <span data-ttu-id="e1250-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="e1250-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1250-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e1250-159">These values are not real.</span></span> <span data-ttu-id="e1250-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="e1250-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e1250-161">Обратитесь к [группа поддержки клиента TargetProcess](mailto:support@targetprocess.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="e1250-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="e1250-162">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e1250-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="e1250-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e1250-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1250-166">На hello **конфигурации TargetProcess** щелкните **Настройка TargetProcess** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="e1250-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e1250-167">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="e1250-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Раздел "Конфигурация TargetProcess"](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="e1250-169">Вход tooyour TargetProcess приложения от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e1250-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="e1250-170">В меню в верхней части hello hello выберите **установки**.</span><span class="sxs-lookup"><span data-stu-id="e1250-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Настройка](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="e1250-172">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="e1250-172">Click **Settings**.</span></span>
   
    ![данных](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="e1250-174">Щелкните **Single Sign-on**(Единый вход).</span><span class="sxs-lookup"><span data-stu-id="e1250-174">Click **Single Sign-on**.</span></span>
   
    ![Щелчок "Single Sign-on" (Единый вход)](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="e1250-176">На hello единым входом параметры диалогового окна выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="e1250-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="e1250-178">а.</span><span class="sxs-lookup"><span data-stu-id="e1250-178">a.</span></span> <span data-ttu-id="e1250-179">Щелкните **Enable Single Sign-on**(Включить единый вход).</span><span class="sxs-lookup"><span data-stu-id="e1250-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="e1250-180">b.</span><span class="sxs-lookup"><span data-stu-id="e1250-180">b.</span></span> <span data-ttu-id="e1250-181">В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="e1250-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e1250-182">c.</span><span class="sxs-lookup"><span data-stu-id="e1250-182">c.</span></span> <span data-ttu-id="e1250-183">Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **сертификат** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="e1250-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="e1250-184">d.</span><span class="sxs-lookup"><span data-stu-id="e1250-184">d.</span></span> <span data-ttu-id="e1250-185">Установите флажок **Enable JIT Provisioning**(Включить JIT-подготовку).</span><span class="sxs-lookup"><span data-stu-id="e1250-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="e1250-186">д.</span><span class="sxs-lookup"><span data-stu-id="e1250-186">e.</span></span> <span data-ttu-id="e1250-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e1250-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e1250-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="e1250-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1250-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="e1250-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1250-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1250-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e1250-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1250-191">Create an Azure AD test user</span></span>
<span data-ttu-id="e1250-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e1250-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e1250-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e1250-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1250-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e1250-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1250-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e1250-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Список hello toodisplay пользователей](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1250-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="e1250-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1250-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e1250-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Раздел "Пользователь"](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1250-203">а.</span><span class="sxs-lookup"><span data-stu-id="e1250-203">a.</span></span> <span data-ttu-id="e1250-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1250-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1250-205">b.</span><span class="sxs-lookup"><span data-stu-id="e1250-205">b.</span></span> <span data-ttu-id="e1250-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e1250-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1250-207">c.</span><span class="sxs-lookup"><span data-stu-id="e1250-207">c.</span></span> <span data-ttu-id="e1250-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="e1250-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e1250-209">d.</span><span class="sxs-lookup"><span data-stu-id="e1250-209">d.</span></span> <span data-ttu-id="e1250-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e1250-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="e1250-211">Создание тестового пользователя TargetProcess</span><span class="sxs-lookup"><span data-stu-id="e1250-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="e1250-212">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="e1250-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="e1250-213">Приложение TargetProcess поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="e1250-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="e1250-214">Эта функция уже включена в ходе [настройки единого входа в Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="e1250-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="e1250-215">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="e1250-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e1250-216">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="e1250-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e1250-217">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTargetProcess доступа.</span><span class="sxs-lookup"><span data-stu-id="e1250-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e1250-219">**tooassign tooTargetProcess Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e1250-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1250-220">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e1250-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e1250-222">В списке приложений hello выберите **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="e1250-222">In hello applications list, select **TargetProcess**.</span></span>

    ![TargetProcess в списке приложений](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="e1250-224">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e1250-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e1250-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e1250-226">Click **Add** button.</span></span> <span data-ttu-id="e1250-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e1250-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e1250-229">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e1250-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1250-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e1250-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1250-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e1250-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e1250-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e1250-232">Test single sign-on</span></span>

<span data-ttu-id="e1250-233">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="e1250-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1250-234">При нажатии кнопки TargetProcess плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour TargetProcess приложения.</span><span class="sxs-lookup"><span data-stu-id="e1250-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="e1250-235">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e1250-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1250-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e1250-236">Additional resources</span></span>

* [<span data-ttu-id="e1250-237">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1250-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1250-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1250-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

