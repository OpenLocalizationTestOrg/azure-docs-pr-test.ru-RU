---
title: "Руководство по интеграции Azure Active Directory с BenSelect | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c3705da337bf8f6e76de58cd21c5b047c8f5e12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="e1d5c-103">Руководство. Интеграция Azure Active Directory с BenSelect</span><span class="sxs-lookup"><span data-stu-id="e1d5c-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="e1d5c-104">В этом учебнике вы узнаете, как toointegrate BenSelect с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1d5c-104">In this tutorial, you learn how toointegrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1d5c-105">Интеграция с Azure AD BenSelect предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e1d5c-105">Integrating BenSelect with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1d5c-106">Можно управлять в Azure AD, имеющего доступ tooBenSelect</span><span class="sxs-lookup"><span data-stu-id="e1d5c-106">You can control in Azure AD who has access tooBenSelect</span></span>
- <span data-ttu-id="e1d5c-107">Можно включить на пользователей tooautomatically get вошедшего tooBenSelect (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d5c-107">You can enable your users tooautomatically get signed-on tooBenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1d5c-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e1d5c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e1d5c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1d5c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1d5c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e1d5c-110">Prerequisites</span></span>

<span data-ttu-id="e1d5c-111">tooconfigure интеграция Azure AD с BenSelect требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="e1d5c-111">tooconfigure Azure AD integration with BenSelect, you need hello following items:</span></span>

- <span data-ttu-id="e1d5c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e1d5c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1d5c-113">подписка BenSelect с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1d5c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1d5c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="e1d5c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1d5c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1d5c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1d5c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1d5c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e1d5c-118">Scenario description</span></span>
<span data-ttu-id="e1d5c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1d5c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="e1d5c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1d5c-121">Добавление BenSelect из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e1d5c-121">Adding BenSelect from hello gallery</span></span>
2. <span data-ttu-id="e1d5c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d5c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-hello-gallery"></a><span data-ttu-id="e1d5c-123">Добавление BenSelect из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e1d5c-123">Adding BenSelect from hello gallery</span></span>
<span data-ttu-id="e1d5c-124">tooconfigure hello интеграции BenSelect в Azure AD, вы должны tooadd BenSelect из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-124">tooconfigure hello integration of BenSelect into Azure AD, you need tooadd BenSelect from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1d5c-125">**tooadd BenSelect из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e1d5c-125">**tooadd BenSelect from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d5c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1d5c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1d5c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e1d5c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e1d5c-133">Введите в поле поиска hello **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-133">In hello search box, type **BenSelect**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="e1d5c-135">В панели результатов hello выберите **BenSelect**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-135">In hello results panel, select **BenSelect**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1d5c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d5c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1d5c-138">В этом разделе описана настройка и проверка единого входа Azure AD в BenSelect с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e1d5c-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BenSelect является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenSelect is tooa user in Azure AD.</span></span> <span data-ttu-id="e1d5c-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в BenSelect должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-140">In other words, a link relationship between an Azure AD user and hello related user in BenSelect needs toobe established.</span></span>

<span data-ttu-id="e1d5c-141">В BenSelect, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-141">In BenSelect, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e1d5c-142">tooconfigure и теста Azure AD единого входа с BenSelect, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e1d5c-142">tooconfigure and test Azure AD single sign-on with BenSelect, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1d5c-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1d5c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1d5c-145">**[Создание тестового пользователя BenSelect](#creating-a-benselect-test-user)**  -toohave аналог Саймон Britta в BenSelect, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - toohave a counterpart of Britta Simon in BenSelect that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1d5c-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1d5c-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1d5c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d5c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1d5c-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении BenSelect.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="e1d5c-150">**tooconfigure Azure AD единого входа с BenSelect, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e1d5c-150">**tooconfigure Azure AD single sign-on with BenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d5c-151">В hello в hello портала Azure **BenSelect** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-151">In hello Azure portal, on hello **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e1d5c-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="e1d5c-155">На hello **URL-адреса и домена BenSelect** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e1d5c-155">On hello **BenSelect Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="e1d5c-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="e1d5c-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1d5c-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-158">This value is not real.</span></span> <span data-ttu-id="e1d5c-159">Измените значение этого параметра hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="e1d5c-160">Обратитесь к [BenSelect поддержки](mailto:support@selerix.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-160">Contact [BenSelect support team](mailto:support@selerix.com) tooget this value.</span></span>
 
4. <span data-ttu-id="e1d5c-161">На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="e1d5c-163">BenSelect приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-163">BenSelect application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="e1d5c-164">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-164">Configure hello following claims for this application.</span></span> <span data-ttu-id="e1d5c-165">Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** раздел на странице интеграции приложений.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-165">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="e1d5c-166">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-166">hello following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="e1d5c-168">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="e1d5c-168">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="e1d5c-169">а.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-169">a.</span></span> <span data-ttu-id="e1d5c-170">В hello **идентификатор пользователя** раскрывающегося списка выберите **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-170">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="e1d5c-171">b.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-171">b.</span></span> <span data-ttu-id="e1d5c-172">В hello **Mail** раскрывающегося списка выберите **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-172">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="e1d5c-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e1d5c-173">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e1d5c-175">На hello **конфигурации BenSelect** щелкните **Настройка BenSelect** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-175">On hello **BenSelect Configuration** section, click **Configure BenSelect** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e1d5c-176">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="e1d5c-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="e1d5c-178">tooconfigure единого входа на **BenSelect** стороны, необходимо загрузить hello toosend **Certificate(Raw)** и **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы**слишком[BenSelect поддержки](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="e1d5c-178">tooconfigure single sign-on on **BenSelect** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="e1d5c-179">Требуется toomention, данная интеграция потребует алгоритм hello SHA256 (не поддерживается SHA1) tooset hello единого входа на соответствующий сервер hello как app2101 и т. д.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-179">You need toomention that this integration requires hello SHA256 algorithm (SHA1 is not supported) tooset hello SSO on hello appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="e1d5c-180">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="e1d5c-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1d5c-181">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1d5c-182">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1d5c-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1d5c-183">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d5c-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1d5c-184">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e1d5c-186">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e1d5c-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d5c-187">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1d5c-189">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1d5c-191">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="e1d5c-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1d5c-193">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e1d5c-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1d5c-195">а.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-195">a.</span></span> <span data-ttu-id="e1d5c-196">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1d5c-197">b.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-197">b.</span></span> <span data-ttu-id="e1d5c-198">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1d5c-199">c.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-199">c.</span></span> <span data-ttu-id="e1d5c-200">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e1d5c-201">d.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-201">d.</span></span> <span data-ttu-id="e1d5c-202">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="e1d5c-203">Создание тестового пользователя BenSelect</span><span class="sxs-lookup"><span data-stu-id="e1d5c-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="e1d5c-204">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в BenSelect.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-204">hello objective of this section is toocreate a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="e1d5c-205">Работать с [BenSelect поддержки](mailto:support@selerix.com) tooadd пользователей hello в hello BenSelect учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-205">Work with [BenSelect support team](mailto:support@selerix.com) tooadd hello users in hello BenSelect account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e1d5c-206">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="e1d5c-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e1d5c-207">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBenSelect доступа.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenSelect.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e1d5c-209">**tooassign tooBenSelect Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e1d5c-209">**tooassign Britta Simon tooBenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1d5c-210">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e1d5c-212">В списке приложений hello выберите **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-212">In hello applications list, select **BenSelect**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="e1d5c-214">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e1d5c-216">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-216">Click **Add** button.</span></span> <span data-ttu-id="e1d5c-217">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e1d5c-219">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1d5c-220">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1d5c-221">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1d5c-222">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e1d5c-222">Testing single sign-on</span></span>

<span data-ttu-id="e1d5c-223">В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-223">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1d5c-224">При нажатии кнопки hello BenSelect плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour BenSelect приложения.</span><span class="sxs-lookup"><span data-stu-id="e1d5c-224">When you click hello BenSelect tile in hello Access Panel, you should get automatically signed-on tooyour BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1d5c-225">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e1d5c-225">Additional resources</span></span>

* [<span data-ttu-id="e1d5c-226">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1d5c-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1d5c-227">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1d5c-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

