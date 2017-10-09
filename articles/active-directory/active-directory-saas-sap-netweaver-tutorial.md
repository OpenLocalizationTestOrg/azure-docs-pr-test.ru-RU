---
title: "Руководство по интеграции Azure Active Directory с SAP NetWeaver | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SAP NetWeaver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 69008734864e1e258a0c2ec872e51aa331491fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="cb87f-103">Руководство. Интеграция Azure Active Directory с SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="cb87f-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="cb87f-104">В этом учебнике вы узнаете, как toointegrate SAP NetWeaver в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb87f-104">In this tutorial, you learn how toointegrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb87f-105">Интеграция SAP NetWeaver в Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="cb87f-105">Integrating SAP NetWeaver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb87f-106">Можно управлять в Azure AD, имеющего доступ tooSAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="cb87f-106">You can control in Azure AD who has access tooSAP NetWeaver</span></span>
- <span data-ttu-id="cb87f-107">Можно включить на пользователей tooautomatically get вошедшего tooSAP NetWeaver (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb87f-107">You can enable your users tooautomatically get signed-on tooSAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb87f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="cb87f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb87f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb87f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cb87f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cb87f-110">Prerequisites</span></span>

<span data-ttu-id="cb87f-111">tooconfigure интеграция Azure AD с SAP NetWeaver необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="cb87f-111">tooconfigure Azure AD integration with SAP NetWeaver, you need hello following items:</span></span>

- <span data-ttu-id="cb87f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="cb87f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb87f-113">подписка SAP NetWeaver с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="cb87f-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb87f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="cb87f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb87f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="cb87f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb87f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="cb87f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb87f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb87f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb87f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="cb87f-118">Scenario description</span></span>
<span data-ttu-id="cb87f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="cb87f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb87f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="cb87f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb87f-121">Добавление SAP NetWeaver из галереи hello</span><span class="sxs-lookup"><span data-stu-id="cb87f-121">Adding SAP NetWeaver from hello gallery</span></span>
2. <span data-ttu-id="cb87f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb87f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-hello-gallery"></a><span data-ttu-id="cb87f-123">Добавление SAP NetWeaver из галереи hello</span><span class="sxs-lookup"><span data-stu-id="cb87f-123">Adding SAP NetWeaver from hello gallery</span></span>
<span data-ttu-id="cb87f-124">tooconfigure hello интеграции SAP NetWeaver в Azure AD, вы должны tooadd SAP NetWeaver из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="cb87f-124">tooconfigure hello integration of SAP NetWeaver into Azure AD, you need tooadd SAP NetWeaver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb87f-125">**tooadd SAP NetWeaver из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cb87f-125">**tooadd SAP NetWeaver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb87f-126">В hello  **[портала Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="cb87f-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb87f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb87f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="cb87f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="cb87f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="cb87f-133">Введите в поле поиска hello **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-133">In hello search box, type **SAP NetWeaver**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="cb87f-135">В панели результатов hello выберите **SAP NetWeaver**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cb87f-135">In hello results panel, select **SAP NetWeaver**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb87f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb87f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb87f-138">В этом разделе описана настройка и проверка единого входа Azure AD в SAP NetWeaver с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb87f-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb87f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SAP NetWeaver является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb87f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP NetWeaver is tooa user in Azure AD.</span></span> <span data-ttu-id="cb87f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в SAP NetWeaver должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="cb87f-140">In other words, a link relationship between an Azure AD user and hello related user in SAP NetWeaver needs toobe established.</span></span>

<span data-ttu-id="cb87f-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="cb87f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="cb87f-142">tooconfigure и теста Azure AD единого входа с SAP NetWeaver, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="cb87f-142">tooconfigure and test Azure AD single sign-on with SAP NetWeaver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb87f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="cb87f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb87f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="cb87f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb87f-145">**[Создание тестового пользователя, прошедшего SAP NetWeaver](#creating-an-sap-netweaver-test-user)**  -toohave аналог Саймон Britta в SAP NetWeaver, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="cb87f-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - toohave a counterpart of Britta Simon in SAP NetWeaver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb87f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="cb87f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb87f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cb87f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb87f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb87f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb87f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="cb87f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="cb87f-150">**tooconfigure Azure AD единого входа с SAP NetWeaver, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cb87f-150">**tooconfigure Azure AD single sign-on with SAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb87f-151">В hello в hello портала Azure **SAP NetWeaver** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-151">In hello Azure portal, on hello **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="cb87f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="cb87f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="cb87f-155">На hello **URL-адреса и домена SAP NetWeaver** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="cb87f-155">On hello **SAP NetWeaver Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="cb87f-157">а.</span><span class="sxs-lookup"><span data-stu-id="cb87f-157">a.</span></span> <span data-ttu-id="cb87f-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="cb87f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="cb87f-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb87f-159">b.</span></span> <span data-ttu-id="cb87f-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="cb87f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="cb87f-161">c.</span><span class="sxs-lookup"><span data-stu-id="cb87f-161">c.</span></span> <span data-ttu-id="cb87f-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="cb87f-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="cb87f-163">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="cb87f-163">These values are not hello real.</span></span> <span data-ttu-id="cb87f-164">Обновить значения hello фактический идентификатор и URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="cb87f-164">Update these values with hello actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="cb87f-165">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="cb87f-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="cb87f-166">Обратитесь к [группа поддержки SAP NetWeaver клиента](https://www.sap.com/support.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="cb87f-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) tooget these values.</span></span> 

4. <span data-ttu-id="cb87f-167">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="cb87f-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="cb87f-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="cb87f-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="cb87f-171">На hello **конфигурации SAP NetWeaver** щелкните **настроить SAP NetWeaver** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="cb87f-171">On hello **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cb87f-172">Копировать hello **идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="cb87f-172">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="cb87f-174">tooconfigure единого входа на **SAP NetWeaver** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **идентификатор сущности SAML** слишком[поддержки SAP NetWeaver ](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="cb87f-174">tooconfigure single sign-on on **SAP NetWeaver** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="cb87f-175">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="cb87f-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb87f-176">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="cb87f-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb87f-177">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb87f-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb87f-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb87f-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb87f-179">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cb87f-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="cb87f-181">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cb87f-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb87f-182">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="cb87f-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb87f-184">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb87f-186">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="cb87f-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb87f-188">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="cb87f-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb87f-190">а.</span><span class="sxs-lookup"><span data-stu-id="cb87f-190">a.</span></span> <span data-ttu-id="cb87f-191">В hello **имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-191">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="cb87f-192">b.</span><span class="sxs-lookup"><span data-stu-id="cb87f-192">b.</span></span> <span data-ttu-id="cb87f-193">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="cb87f-193">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="cb87f-194">c.</span><span class="sxs-lookup"><span data-stu-id="cb87f-194">c.</span></span> <span data-ttu-id="cb87f-195">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb87f-196">d.</span><span class="sxs-lookup"><span data-stu-id="cb87f-196">d.</span></span> <span data-ttu-id="cb87f-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="cb87f-198">Создание тестового пользователя SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="cb87f-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="cb87f-199">В этом разделе описано, как создать пользователя Britta Simon в приложении SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="cb87f-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="cb87f-200">Работа с вашей [поддержки SAP NetWeaver](https://www.sap.com/support.html) tooadd hello пользователей на платформе SAP NetWeaver hello.</span><span class="sxs-lookup"><span data-stu-id="cb87f-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) tooadd hello users in hello SAP NetWeaver platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb87f-201">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="cb87f-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb87f-202">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="cb87f-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP NetWeaver.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="cb87f-204">**tooassign tooSAP Britta Simon NetWeaver, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="cb87f-204">**tooassign Britta Simon tooSAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb87f-205">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="cb87f-207">В списке приложений hello выберите **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-207">In hello applications list, select **SAP NetWeaver**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="cb87f-209">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="cb87f-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-211">Click **Add** button.</span></span> <span data-ttu-id="cb87f-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="cb87f-214">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="cb87f-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb87f-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb87f-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="cb87f-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb87f-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="cb87f-217">Testing single sign-on</span></span>

<span data-ttu-id="cb87f-218">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="cb87f-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cb87f-219">При выборе плитки SAP NetWeaver hello в hello панели доступа, следует получать автоматически вошедшего tooyour приложения SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="cb87f-219">When you click hello SAP NetWeaver tile in hello Access Panel, you should get automatically signed-on tooyour SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb87f-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cb87f-220">Additional resources</span></span>

* [<span data-ttu-id="cb87f-221">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb87f-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb87f-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb87f-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

