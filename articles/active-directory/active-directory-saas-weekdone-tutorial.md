---
title: "Руководство по интеграции Azure Active Directory с Weekdone | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f997f1b49ff1aa0659a2409fdd945c6f96413b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="c0941-103">Руководство. Интеграция Azure Active Directory с Weekdone</span><span class="sxs-lookup"><span data-stu-id="c0941-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="c0941-104">В этом учебнике вы узнаете, как toointegrate Weekdone с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0941-104">In this tutorial, you learn how toointegrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0941-105">Интеграция с Azure AD Weekdone предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c0941-105">Integrating Weekdone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0941-106">Можно управлять в Azure AD, имеющего доступ tooWeekdone</span><span class="sxs-lookup"><span data-stu-id="c0941-106">You can control in Azure AD who has access tooWeekdone</span></span>
- <span data-ttu-id="c0941-107">Можно включить на пользователей tooautomatically get вошедшего tooWeekdone (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0941-107">You can enable your users tooautomatically get signed-on tooWeekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0941-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c0941-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0941-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0941-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0941-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c0941-110">Prerequisites</span></span>

<span data-ttu-id="c0941-111">tooconfigure интеграция Azure AD с Weekdone требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c0941-111">tooconfigure Azure AD integration with Weekdone, you need hello following items:</span></span>

- <span data-ttu-id="c0941-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c0941-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0941-113">подписка Weekdone с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c0941-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0941-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c0941-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0941-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c0941-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0941-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c0941-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0941-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0941-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0941-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c0941-118">Scenario description</span></span>
<span data-ttu-id="c0941-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c0941-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0941-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c0941-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0941-121">Добавление Weekdone из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c0941-121">Adding Weekdone from hello gallery</span></span>
2. <span data-ttu-id="c0941-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0941-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-hello-gallery"></a><span data-ttu-id="c0941-123">Добавление Weekdone из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c0941-123">Adding Weekdone from hello gallery</span></span>
<span data-ttu-id="c0941-124">tooconfigure hello интеграции Weekdone в Azure AD, вы должны tooadd Weekdone из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0941-124">tooconfigure hello integration of Weekdone into Azure AD, you need tooadd Weekdone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0941-125">**tooadd Weekdone из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0941-125">**tooadd Weekdone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0941-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c0941-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0941-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c0941-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0941-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0941-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c0941-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c0941-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c0941-133">Введите в поле поиска hello **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="c0941-133">In hello search box, type **Weekdone**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="c0941-135">В панели результатов hello выберите **Weekdone**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c0941-135">In hello results panel, select **Weekdone**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0941-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0941-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0941-138">В этом разделе описана настройка и проверка единого входа Azure AD в Weekdone с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0941-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0941-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Weekdone является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0941-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Weekdone is tooa user in Azure AD.</span></span> <span data-ttu-id="c0941-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Weekdone должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c0941-140">In other words, a link relationship between an Azure AD user and hello related user in Weekdone needs toobe established.</span></span>

<span data-ttu-id="c0941-141">В Weekdone, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c0941-141">In Weekdone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c0941-142">tooconfigure и теста Azure AD единого входа с Weekdone, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c0941-142">tooconfigure and test Azure AD single sign-on with Weekdone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0941-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c0941-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0941-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c0941-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0941-145">**[Создание тестового пользователя Weekdone](#creating-a-weekdone-test-user)**  -toohave аналог Саймон Britta в Weekdone, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0941-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - toohave a counterpart of Britta Simon in Weekdone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0941-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c0941-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0941-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c0941-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0941-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0941-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0941-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Weekdone.</span><span class="sxs-lookup"><span data-stu-id="c0941-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="c0941-150">**tooconfigure Azure AD единого входа с Weekdone, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0941-150">**tooconfigure Azure AD single sign-on with Weekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0941-151">В hello в hello портала Azure **Weekdone** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c0941-151">In hello Azure portal, on hello **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c0941-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c0941-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="c0941-155">На hello **Weekdone доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="c0941-155">On hello **Weekdone Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="c0941-157">а.</span><span class="sxs-lookup"><span data-stu-id="c0941-157">a.</span></span> <span data-ttu-id="c0941-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="c0941-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="c0941-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0941-159">b.</span></span> <span data-ttu-id="c0941-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="c0941-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="c0941-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="c0941-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="c0941-162">При необходимости приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="c0941-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="c0941-164">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="c0941-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c0941-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c0941-165">These values are not real.</span></span> <span data-ttu-id="c0941-166">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="c0941-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c0941-167">Обратитесь к [группа поддержки клиента Weekdone](mailto:hello@weekdone.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="c0941-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) tooget these values.</span></span> 

5. <span data-ttu-id="c0941-168">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c0941-168">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="c0941-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c0941-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c0941-172">На hello **конфигурации Weekdone** щелкните **Настройка Weekdone** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c0941-172">On hello **Weekdone Configuration** section, click **Configure Weekdone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c0941-173">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c0941-173">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="c0941-175">tooconfigure единого входа на **Weekdone** стороны, необходимо загрузить hello toosend **метаданные в формате XML, URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Weekdone поддержки команда](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="c0941-175">tooconfigure single sign-on on **Weekdone** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="c0941-176">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c0941-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0941-177">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c0941-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0941-178">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0941-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0941-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0941-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0941-180">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c0941-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c0941-182">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0941-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0941-183">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c0941-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0941-185">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c0941-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0941-187">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="c0941-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0941-189">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c0941-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0941-191">а.</span><span class="sxs-lookup"><span data-stu-id="c0941-191">a.</span></span> <span data-ttu-id="c0941-192">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0941-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0941-193">b.</span><span class="sxs-lookup"><span data-stu-id="c0941-193">b.</span></span> <span data-ttu-id="c0941-194">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0941-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0941-195">c.</span><span class="sxs-lookup"><span data-stu-id="c0941-195">c.</span></span> <span data-ttu-id="c0941-196">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c0941-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0941-197">d.</span><span class="sxs-lookup"><span data-stu-id="c0941-197">d.</span></span> <span data-ttu-id="c0941-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c0941-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="c0941-199">Создание тестового пользователя Weekdone</span><span class="sxs-lookup"><span data-stu-id="c0941-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="c0941-200">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Weekdone.</span><span class="sxs-lookup"><span data-stu-id="c0941-200">hello objective of this section is toocreate a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="c0941-201">Приложение Weekdone поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c0941-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c0941-202">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="c0941-202">There is no action item for you in this section.</span></span> <span data-ttu-id="c0941-203">Новый пользователь создается во время попытки tooaccess Weekdone, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="c0941-203">A new user is created during an attempt tooaccess Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="c0941-204">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Weekdone клиента поддержки](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="c0941-204">If you need toocreate a user manually, you need toocontact hello [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0941-205">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c0941-205">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0941-206">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWeekdone доступа.</span><span class="sxs-lookup"><span data-stu-id="c0941-206">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWeekdone.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c0941-208">**tooassign tooWeekdone Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c0941-208">**tooassign Britta Simon tooWeekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0941-209">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0941-209">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c0941-211">В списке приложений hello выберите **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="c0941-211">In hello applications list, select **Weekdone**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="c0941-213">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c0941-213">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c0941-215">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c0941-215">Click **Add** button.</span></span> <span data-ttu-id="c0941-216">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c0941-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c0941-218">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c0941-218">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0941-219">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c0941-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0941-220">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c0941-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0941-221">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c0941-221">Testing single sign-on</span></span>

<span data-ttu-id="c0941-222">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="c0941-222">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c0941-223">При нажатии кнопки hello Weekdone плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Weekdone приложения.</span><span class="sxs-lookup"><span data-stu-id="c0941-223">When you click hello Weekdone tile in hello Access Panel, you should get automatically signed-on tooyour Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0941-224">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c0941-224">Additional resources</span></span>

* [<span data-ttu-id="c0941-225">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0941-225">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0941-226">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0941-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

