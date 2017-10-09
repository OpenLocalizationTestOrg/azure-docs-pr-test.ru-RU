---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и рабочей области с Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="250b2-103">Руководство по интеграции Azure Active Directory с Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="250b2-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="250b2-104">В этом учебнике вы узнаете, как toointegrate рабочему месту с Facebook с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="250b2-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="250b2-105">Интеграция рабочему месту с Facebook с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="250b2-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="250b2-106">Можно управлять в Azure AD, имеющего доступ tooWorkplace с Facebook</span><span class="sxs-lookup"><span data-stu-id="250b2-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="250b2-107">Можно включить на пользователей tooautomatically get вошедшего tooWorkplace с Facebook (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="250b2-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="250b2-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="250b2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="250b2-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="250b2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="250b2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="250b2-110">Prerequisites</span></span>

<span data-ttu-id="250b2-111">tooconfigure интеграция Azure AD в рабочей области с Facebook, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="250b2-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="250b2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="250b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="250b2-113">подписка Workplace by Facebook с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="250b2-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="250b2-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="250b2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="250b2-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="250b2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="250b2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="250b2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="250b2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="250b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="250b2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="250b2-118">Scenario description</span></span>
<span data-ttu-id="250b2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="250b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="250b2-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="250b2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="250b2-121">Добавление рабочей области с Facebook из галереи hello</span><span class="sxs-lookup"><span data-stu-id="250b2-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="250b2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="250b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="250b2-123">Добавление рабочей области с Facebook из галереи hello</span><span class="sxs-lookup"><span data-stu-id="250b2-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="250b2-124">tooconfigure hello интеграции рабочему месту с Facebook в Azure AD, вы должны tooadd рабочему месту с Facebook из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="250b2-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="250b2-125">**tooadd рабочему месту с Facebook из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="250b2-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="250b2-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="250b2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="250b2-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="250b2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="250b2-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="250b2-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="250b2-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="250b2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="250b2-133">Введите в поле поиска hello **рабочему месту с Facebook**.</span><span class="sxs-lookup"><span data-stu-id="250b2-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="250b2-135">В панели результатов hello выберите **рабочему месту с Facebook**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="250b2-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="250b2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="250b2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="250b2-138">В этом разделе описана настройка и проверка единого входа Azure AD в Workplace by Facebook с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="250b2-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="250b2-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочей области с Facebook является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="250b2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="250b2-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочей области с Facebook должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="250b2-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="250b2-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в рабочей области с Facebook.</span><span class="sxs-lookup"><span data-stu-id="250b2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="250b2-142">tooconfigure и тестирования Azure AD единого входа в рабочей области с Facebook, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="250b2-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="250b2-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="250b2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="250b2-144">**[Настройка частоты повторная проверка подлинности](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt рабочему месту для проверки SAML.</span><span class="sxs-lookup"><span data-stu-id="250b2-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="250b2-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="250b2-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="250b2-146">**[Создание рабочей области с Facebook тестового пользователя](#creating-a-workplace-by-facebook-test-user)**  -toohave аналог Саймон Britta в рабочей области с Facebook, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="250b2-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="250b2-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="250b2-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="250b2-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="250b2-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="250b2-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="250b2-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="250b2-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в рабочую область приложения Facebook.</span><span class="sxs-lookup"><span data-stu-id="250b2-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="250b2-151">**tooconfigure Azure AD единого входа в рабочей области с Facebook, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="250b2-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="250b2-152">В hello в hello портала Azure **рабочему месту с Facebook** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="250b2-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="250b2-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="250b2-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="250b2-156">На hello **рабочему месту с URL-адреса и домена Facebook** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="250b2-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="250b2-158">а.</span><span class="sxs-lookup"><span data-stu-id="250b2-158">a.</span></span> <span data-ttu-id="250b2-159">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="250b2-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="250b2-160">b.</span><span class="sxs-lookup"><span data-stu-id="250b2-160">b.</span></span> <span data-ttu-id="250b2-161">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="250b2-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="250b2-162">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="250b2-162">These values are not hello real.</span></span> <span data-ttu-id="250b2-163">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="250b2-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="250b2-164">Обратитесь к [рабочей группой поддержки клиент Facebook](https://workplace.fb.com/faq/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="250b2-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="250b2-165">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="250b2-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="250b2-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="250b2-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="250b2-169">На hello **рабочему месту конфигурацией Facebook** щелкните **Настройка рабочей области с Facebook** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="250b2-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="250b2-170">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="250b2-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="250b2-172">В другом окне браузера, tooyour входа рабочему месту с Facebook сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="250b2-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="250b2-173">Как часть процесса проверки подлинности SAML hello рабочее место может использовать строки запроса из копии too2.5 килобайт в размер в порядке toopass параметры tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="250b2-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="250b2-174">В hello **панели мониторинга компании**, go toohello **проверки подлинности** вкладки.</span><span class="sxs-lookup"><span data-stu-id="250b2-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="250b2-175">В разделе **проверку подлинности SAML**выберите **SSO только** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="250b2-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="250b2-176">Hello входные значения, скопированные из **рабочему месту конфигурацией Facebook** раздел hello портал Azure в соответствующие поля hello:</span><span class="sxs-lookup"><span data-stu-id="250b2-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="250b2-177">В **SAML URL-адрес** текстовое значение hello вставить **единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="250b2-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="250b2-178">В **текстовое поле URL-адрес издателя SAML**, вставьте значение hello **идентификатор сущности SAML**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="250b2-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="250b2-179">В **перенаправление выхода SAML** (необязательно) вставьте значение hello **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="250b2-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="250b2-180">Откройте ваш **сертификат в кодировке base-64** в блокноте, Скачанный с портала Azure скопируйте hello содержимое в буфер обмена, а затем вставьте его toothe **сертификат SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="250b2-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="250b2-181">Может потребоваться tooenter hello аудитории URL-адрес, URL-адрес получателя, и URL-адрес ACS (службы обработчика утверждений), перечисленные в папке hello **конфигурация SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="250b2-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="250b2-182">Прокрутите toohello нижней части раздела hello и щелкните hello **тестирования единого входа** кнопки.</span><span class="sxs-lookup"><span data-stu-id="250b2-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="250b2-183">Появится всплывающее окно со страницей входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="250b2-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="250b2-184">Введите свои учетные данные в виде обычных tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="250b2-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="250b2-185">**Устранение неполадок:** Здравствуйте убедитесь, что адрес электронной почты на hello возвращается обратно из Azure AD, так же, как hello рабочей учетной записи, на который выполнен вход в систему.</span><span class="sxs-lookup"><span data-stu-id="250b2-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="250b2-186">После успешного выполнения теста hello, прокрутите toohello внизу страницы приветствия и нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="250b2-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="250b2-187">Теперь для аутентификации всех пользователей Workplace будет отображаться страница входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="250b2-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="250b2-188">**Перенаправление для выхода SAML (необязательно)** -</span><span class="sxs-lookup"><span data-stu-id="250b2-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="250b2-189">Вы можете toooptionally настроить URL-адрес выхода SAML, которой может быть toopoint, используемые в Azure AD страницы выхода.</span><span class="sxs-lookup"><span data-stu-id="250b2-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="250b2-190">Если этот параметр включен и настроен, hello пользователь больше не будет страницы выхода направленной toohello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="250b2-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="250b2-191">Вместо этого пользователь hello будет перенаправленный toohello URL-адрес, которое было добавлено в приветствия перенаправление выхода SAML.</span><span class="sxs-lookup"><span data-stu-id="250b2-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="250b2-192">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="250b2-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="250b2-193">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="250b2-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="250b2-194">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="250b2-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="250b2-195">Настройка частоты повторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="250b2-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="250b2-196">Можно настроить tooprompt рабочему месту для проверки SAML каждый день, три дня недели, в две недели, месяц или никогда.</span><span class="sxs-lookup"><span data-stu-id="250b2-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="250b2-197">Hello минимальное значение для проверки SAML hello мобильных приложений имеет значение tooone недели.</span><span class="sxs-lookup"><span data-stu-id="250b2-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="250b2-198">Можно также принудительно выполнить сброс для всех пользователей с помощью кнопки hello SAML: требуется проверка подлинности SAML для всех пользователей сейчас.</span><span class="sxs-lookup"><span data-stu-id="250b2-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="250b2-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="250b2-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="250b2-200">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="250b2-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="250b2-202">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="250b2-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="250b2-203">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="250b2-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="250b2-205">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="250b2-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="250b2-207">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="250b2-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="250b2-209">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="250b2-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="250b2-211">а.</span><span class="sxs-lookup"><span data-stu-id="250b2-211">a.</span></span> <span data-ttu-id="250b2-212">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="250b2-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="250b2-213">b.</span><span class="sxs-lookup"><span data-stu-id="250b2-213">b.</span></span> <span data-ttu-id="250b2-214">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="250b2-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="250b2-215">c.</span><span class="sxs-lookup"><span data-stu-id="250b2-215">c.</span></span> <span data-ttu-id="250b2-216">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="250b2-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="250b2-217">d.</span><span class="sxs-lookup"><span data-stu-id="250b2-217">d.</span></span> <span data-ttu-id="250b2-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="250b2-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="250b2-219">Создание тестового пользователя Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="250b2-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="250b2-220">В этом разделе вы создадите в Workplace by Facebook пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="250b2-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="250b2-221">Workplace by Facebook поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="250b2-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="250b2-222">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="250b2-222">There is no action for you in this section.</span></span> <span data-ttu-id="250b2-223">Если пользователь не существует в рабочей области с Facebook, новый созданный при попытке tooaccess рабочему месту Facebook.</span><span class="sxs-lookup"><span data-stu-id="250b2-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="250b2-224">При необходимости пользователь вручную, обратитесь в службу toocreate [рабочей группой поддержки клиент Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="250b2-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="250b2-225">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="250b2-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="250b2-226">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="250b2-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="250b2-228">**tooassign tooWorkplace Britta Simon с Facebook, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="250b2-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="250b2-229">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="250b2-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="250b2-231">В списке приложений hello выберите **рабочему месту с Facebook**.</span><span class="sxs-lookup"><span data-stu-id="250b2-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="250b2-233">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="250b2-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="250b2-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="250b2-235">Click **Add** button.</span></span> <span data-ttu-id="250b2-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="250b2-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="250b2-238">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="250b2-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="250b2-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="250b2-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="250b2-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="250b2-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="250b2-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="250b2-241">Testing single sign-on</span></span>

<span data-ttu-id="250b2-242">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="250b2-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="250b2-243">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="250b2-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="250b2-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="250b2-244">Additional resources</span></span>

* [<span data-ttu-id="250b2-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="250b2-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="250b2-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="250b2-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="250b2-247">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="250b2-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

