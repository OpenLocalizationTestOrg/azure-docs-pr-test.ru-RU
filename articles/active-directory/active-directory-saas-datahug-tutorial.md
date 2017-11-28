---
title: "Руководство по интеграции Azure Active Directory с Datahug | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="0788d-103">Руководство. Интеграция Azure Active Directory с Datahug</span><span class="sxs-lookup"><span data-stu-id="0788d-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="0788d-104">В этом учебнике вы узнаете, как toointegrate Datahug с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0788d-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0788d-105">Интеграция с Azure AD Datahug предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0788d-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0788d-106">Можно управлять в Azure AD, имеющего доступ tooDatahug</span><span class="sxs-lookup"><span data-stu-id="0788d-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="0788d-107">Можно включить на пользователей tooautomatically get вошедшего tooDatahug (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0788d-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0788d-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0788d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0788d-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0788d-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="0788d-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0788d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0788d-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0788d-111">Prerequisites</span></span>

<span data-ttu-id="0788d-112">tooconfigure интеграция Azure AD с Datahug требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0788d-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="0788d-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0788d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0788d-114">подписка Datahug с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0788d-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0788d-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0788d-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0788d-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0788d-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0788d-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0788d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0788d-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0788d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0788d-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0788d-119">Scenario description</span></span>
<span data-ttu-id="0788d-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0788d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0788d-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0788d-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0788d-122">Добавление Datahug из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0788d-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="0788d-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0788d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="0788d-124">Добавление Datahug из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0788d-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="0788d-125">tooconfigure hello интеграции Datahug в Azure AD, вы должны tooadd Datahug из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0788d-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0788d-126">**tooadd Datahug из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0788d-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0788d-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0788d-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0788d-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0788d-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0788d-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0788d-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0788d-132">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0788d-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0788d-134">Введите в поле поиска hello **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="0788d-134">In hello search box, type **Datahug**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="0788d-136">В панели результатов hello выберите **Datahug**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0788d-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0788d-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0788d-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0788d-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Datahug с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0788d-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0788d-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Datahug является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0788d-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="0788d-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Datahug должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0788d-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="0788d-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Datahug.</span><span class="sxs-lookup"><span data-stu-id="0788d-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="0788d-143">tooconfigure и теста Azure AD единого входа с Datahug, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0788d-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0788d-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0788d-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0788d-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0788d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0788d-146">**[Создание тестового пользователя Datahug](#creating-a-datahug-test-user)**  -toohave аналог Саймон Britta в Datahug, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="0788d-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0788d-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0788d-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0788d-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0788d-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0788d-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0788d-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0788d-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Datahug.</span><span class="sxs-lookup"><span data-stu-id="0788d-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="0788d-151">**tooconfigure Azure AD единого входа с Datahug, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0788d-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="0788d-152">В hello в hello портала Azure **Datahug** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0788d-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0788d-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0788d-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="0788d-156">На hello **Datahug доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="0788d-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="0788d-158">а.</span><span class="sxs-lookup"><span data-stu-id="0788d-158">a.</span></span> <span data-ttu-id="0788d-159">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="0788d-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="0788d-160">b.</span><span class="sxs-lookup"><span data-stu-id="0788d-160">b.</span></span> <span data-ttu-id="0788d-161">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="0788d-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="0788d-162">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="0788d-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="0788d-163">При необходимости приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="0788d-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="0788d-165">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="0788d-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0788d-166">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="0788d-166">These values are not hello real.</span></span> <span data-ttu-id="0788d-167">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0788d-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0788d-168">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатора и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="0788d-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="0788d-169">Обратитесь к [группа поддержки клиента Datahug](http://datahug.com/about/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="0788d-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="0788d-170">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0788d-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="0788d-172">Проверьте **«Показывать дополнительные параметры подписи сертификата»** и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="0788d-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="0788d-174">А.</span><span class="sxs-lookup"><span data-stu-id="0788d-174">a.</span></span> <span data-ttu-id="0788d-175">В поле **Вариант подписывания** выберите **Утверждение знака SAML**.</span><span class="sxs-lookup"><span data-stu-id="0788d-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="0788d-176">b.</span><span class="sxs-lookup"><span data-stu-id="0788d-176">b.</span></span> <span data-ttu-id="0788d-177">В поле **Алгоритм подписывания** выберите **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="0788d-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="0788d-178">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0788d-178">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="0788d-180">На hello **конфигурации Datahug** щелкните **Настройка Datahug** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="0788d-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0788d-181">Копировать hello **идентификатор сущности SAML** и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="0788d-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="0788d-183">tooconfigure единого входа на **Datahug** стороны, необходимо загрузить hello toosend **метаданные в формате XML**, **идентификатор сущности SAML** и **SAML единого входа службы URL-адрес** слишком[Datahug поддержки](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="0788d-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="0788d-184">Они устанавливаются это приложение hello toohave правильно настроенной на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="0788d-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0788d-185">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="0788d-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0788d-186">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0788d-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0788d-187">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0788d-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0788d-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0788d-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="0788d-189">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0788d-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0788d-191">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0788d-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0788d-192">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0788d-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0788d-194">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0788d-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0788d-196">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="0788d-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0788d-198">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0788d-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0788d-200">а.</span><span class="sxs-lookup"><span data-stu-id="0788d-200">a.</span></span> <span data-ttu-id="0788d-201">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0788d-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0788d-202">b.</span><span class="sxs-lookup"><span data-stu-id="0788d-202">b.</span></span> <span data-ttu-id="0788d-203">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0788d-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0788d-204">c.</span><span class="sxs-lookup"><span data-stu-id="0788d-204">c.</span></span> <span data-ttu-id="0788d-205">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0788d-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0788d-206">d.</span><span class="sxs-lookup"><span data-stu-id="0788d-206">d.</span></span> <span data-ttu-id="0788d-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0788d-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="0788d-208">Создание тестового пользователя Datahug</span><span class="sxs-lookup"><span data-stu-id="0788d-208">Creating a Datahug test user</span></span>

<span data-ttu-id="0788d-209">Пользователи toolog tooenable Azure AD в tooDatahug, их необходимо подготовить в Datahug.</span><span class="sxs-lookup"><span data-stu-id="0788d-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="0788d-210">Эта подготовка для Datahug выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="0788d-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="0788d-211">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0788d-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0788d-212">Войдите в систему tooyour Datahug сайт компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="0788d-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="0788d-213">Наведите указатель мыши на hello **шестеренки** в правом верхнем углу приветствия и нажмите кнопку **параметры**</span><span class="sxs-lookup"><span data-stu-id="0788d-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Добавление сотрудника](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="0788d-215">Выберите **людей** и нажмите кнопку hello **Добавление пользователей** вкладка</span><span class="sxs-lookup"><span data-stu-id="0788d-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="0788d-217">Введите hello электронной почты лица hello хотелось бы toocreate учетную запись для и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="0788d-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="0788d-219">Можно отправить toouser почты регистрации, выбрав **отправки приветственного сообщения** флажок.</span><span class="sxs-lookup"><span data-stu-id="0788d-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="0788d-220">При создании учетной записи для Salesforce не передают hello приветственное сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="0788d-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0788d-221">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0788d-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0788d-222">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooDatahug доступа.</span><span class="sxs-lookup"><span data-stu-id="0788d-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0788d-224">**tooassign tooDatahug Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0788d-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="0788d-225">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0788d-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0788d-227">В списке приложений hello выберите **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="0788d-227">In hello applications list, select **Datahug**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="0788d-229">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0788d-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0788d-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0788d-231">Click **Add** button.</span></span> <span data-ttu-id="0788d-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0788d-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0788d-234">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0788d-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0788d-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0788d-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0788d-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0788d-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0788d-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0788d-237">Testing single sign-on</span></span>

<span data-ttu-id="0788d-238">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0788d-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="0788d-239">При нажатии кнопки hello Datahug плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Datahug приложения.</span><span class="sxs-lookup"><span data-stu-id="0788d-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="0788d-240">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0788d-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0788d-241">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0788d-241">Additional resources</span></span>

* [<span data-ttu-id="0788d-242">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0788d-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0788d-243">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0788d-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

