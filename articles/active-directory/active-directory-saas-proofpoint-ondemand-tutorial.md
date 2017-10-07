---
title: "Руководство по интеграции Azure Active Directory с Proofpoint on Demand | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Proofpoint по требованию."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="1f23f-103">Руководство. Интеграция Azure Active Directory с Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="1f23f-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="1f23f-104">В этом учебнике вы узнаете, как toointegrate Proofpoint по запросу в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f23f-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f23f-105">Интеграция Proofpoint по запросу с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1f23f-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1f23f-106">Можно управлять в Azure AD, имеющего tooProofpoint доступ по требованию</span><span class="sxs-lookup"><span data-stu-id="1f23f-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="1f23f-107">Можно включить на пользователей tooautomatically get вошедшего tooProofpoint по требованию (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f23f-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f23f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1f23f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1f23f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f23f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f23f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1f23f-110">Prerequisites</span></span>

<span data-ttu-id="1f23f-111">Интеграция Azure AD tooconfigure Proofpoint по требованию необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1f23f-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="1f23f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1f23f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f23f-113">подписка с поддержкой единого входа Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="1f23f-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f23f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1f23f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f23f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1f23f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f23f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1f23f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f23f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f23f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f23f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1f23f-118">Scenario description</span></span>
<span data-ttu-id="1f23f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1f23f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f23f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1f23f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f23f-121">Добавление Proofpoint по запросу из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1f23f-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="1f23f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f23f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="1f23f-123">Добавление Proofpoint по запросу из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1f23f-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="1f23f-124">tooconfigure hello интеграции Proofpoint по запросу в Azure AD, вы должны tooadd Proofpoint по запросу из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1f23f-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1f23f-125">**tooadd Proofpoint по запросу из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1f23f-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f23f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1f23f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f23f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1f23f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1f23f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1f23f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1f23f-133">Введите в поле поиска hello **Proofpoint по требованию**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="1f23f-135">В панели результатов hello выберите **Proofpoint по требованию**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1f23f-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f23f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f23f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f23f-138">Этот раздел описывает, как настроить и проверить единый вход Azure AD в Proofpoint on Demand с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f23f-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f23f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Proofpoint по требованию является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f23f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="1f23f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Proofpoint по запросу должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="1f23f-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="1f23f-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Proofpoint по требованию.</span><span class="sxs-lookup"><span data-stu-id="1f23f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="1f23f-142">tooconfigure и Azure AD тестирования единого входа Proofpoint по требованию необходимо hello toocomplete следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="1f23f-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1f23f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1f23f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1f23f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1f23f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f23f-145">**[Создание тестового пользователя запросу Proofpoint](#creating-a-proofpoint-on-demand-test-user)**  -toohave аналог Саймон Britta в Proofpoint по запросу, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="1f23f-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f23f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1f23f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f23f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1f23f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f23f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f23f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f23f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей Proofpoint по запросу приложения.</span><span class="sxs-lookup"><span data-stu-id="1f23f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="1f23f-150">**tooconfigure Azure AD единого входа с Proofpoint по запросу, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1f23f-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f23f-151">В hello в hello портала Azure **Proofpoint по требованию** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1f23f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1f23f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="1f23f-155">На hello **Proofpoint на URL-адреса и домена запросу** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1f23f-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="1f23f-157">a.In hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="1f23f-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="1f23f-158">b.</span><span class="sxs-lookup"><span data-stu-id="1f23f-158">b.</span></span> <span data-ttu-id="1f23f-159">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="1f23f-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="1f23f-160">c.</span><span class="sxs-lookup"><span data-stu-id="1f23f-160">c.</span></span>  <span data-ttu-id="1f23f-161">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="1f23f-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1f23f-162">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="1f23f-162">These values are not hello real.</span></span> <span data-ttu-id="1f23f-163">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="1f23f-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="1f23f-164">Обратитесь к [Proofpoint в службу поддержки по запросу клиента](https://www.proofpoint.com/us/support-services) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="1f23f-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="1f23f-165">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="1f23f-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="1f23f-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1f23f-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="1f23f-169">На hello **Proofpoint конфигурации запросу** щелкните **Настройка Proofpoint по требованию** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="1f23f-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1f23f-170">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="1f23f-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="1f23f-172">tooconfigure единого входа на **Proofpoint по требованию** стороны, необходимо загрузить hello toosend **Certificate(Base64)**,**идентификатор сущности SAML**, и **SAML Single Sign On URL-адрес службы** слишком[Proofpoint в службу поддержки по запросу клиента](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="1f23f-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="1f23f-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1f23f-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1f23f-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1f23f-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1f23f-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f23f-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f23f-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f23f-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f23f-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1f23f-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1f23f-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1f23f-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f23f-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1f23f-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f23f-182">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="1f23f-182">These values are not hello real.</span></span> <span data-ttu-id="1f23f-183">Обновить эти значения с фактическое hello</span><span class="sxs-lookup"><span data-stu-id="1f23f-183">Update these values with hello actual</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f23f-185">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="1f23f-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f23f-187">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1f23f-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f23f-189">а.</span><span class="sxs-lookup"><span data-stu-id="1f23f-189">a.</span></span> <span data-ttu-id="1f23f-190">В hello **имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="1f23f-191">b.</span><span class="sxs-lookup"><span data-stu-id="1f23f-191">b.</span></span> <span data-ttu-id="1f23f-192">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1f23f-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="1f23f-193">c.</span><span class="sxs-lookup"><span data-stu-id="1f23f-193">c.</span></span> <span data-ttu-id="1f23f-194">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1f23f-195">d.</span><span class="sxs-lookup"><span data-stu-id="1f23f-195">d.</span></span> <span data-ttu-id="1f23f-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="1f23f-197">Создание тестового пользователя Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="1f23f-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="1f23f-198">В этом разделе описано, как создать пользователя Britta Simon в Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="1f23f-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="1f23f-199">Работать с [Proofpoint в службу поддержки по запросу клиента](https://www.proofpoint.com/us/support-services) tooadd пользователей в hello Proofpoint на платформе запросу.</span><span class="sxs-lookup"><span data-stu-id="1f23f-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1f23f-200">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1f23f-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1f23f-201">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooProofpoint по требованию.</span><span class="sxs-lookup"><span data-stu-id="1f23f-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1f23f-203">**tooassign tooProofpoint Britta Simon по запросу, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="1f23f-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f23f-204">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1f23f-206">В списке приложений hello выберите **Proofpoint по требованию**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="1f23f-208">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1f23f-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-210">Click **Add** button.</span></span> <span data-ttu-id="1f23f-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1f23f-213">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1f23f-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1f23f-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f23f-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1f23f-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f23f-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1f23f-216">Testing single sign-on</span></span>

<span data-ttu-id="1f23f-217">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="1f23f-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1f23f-218">При нажатии кнопки hello **Proofpoint по требованию** плитки на панели доступа hello, пользователь должен быть автоматически вход tooyour Proofpoint по запросу приложения.</span><span class="sxs-lookup"><span data-stu-id="1f23f-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="1f23f-219">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f23f-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="1f23f-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1f23f-220">Additional resources</span></span>

* [<span data-ttu-id="1f23f-221">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f23f-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f23f-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f23f-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

