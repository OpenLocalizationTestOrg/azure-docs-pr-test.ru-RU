---
title: "Руководство по интеграции Azure Active Directory с Autotask Workplace | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Autotask рабочей области."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="8b281-103">Руководство по интеграции Azure Active Directory с Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="8b281-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="8b281-104">В этом учебнике вы узнаете, как toointegrate Autotask рабочему месту с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b281-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b281-105">Интеграция с Azure AD Autotask рабочему месту предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8b281-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8b281-106">Можно управлять в Azure AD, имеющего tooAutotask доступа к рабочему месту</span><span class="sxs-lookup"><span data-stu-id="8b281-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="8b281-107">Можно включить на пользователей tooautomatically get вошедшего tooAutotask рабочему месту (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b281-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b281-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8b281-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8b281-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b281-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b281-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8b281-110">Prerequisites</span></span>

<span data-ttu-id="8b281-111">tooconfigure интеграция Azure AD в рабочей области Autotask требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8b281-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="8b281-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8b281-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b281-113">подписка Autotask Workplace с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8b281-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="8b281-114">права администратора или суперадминистратора в рабочей области;</span><span class="sxs-lookup"><span data-stu-id="8b281-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="8b281-115">Необходимо иметь учетную запись администратора в hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b281-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="8b281-116">Hello пользователей, которые будут использоваться этой функции должны иметь учетные записи в рабочей области и hello Azure AD, и их адреса электронной почты для обоих должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="8b281-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="8b281-117">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8b281-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b281-118">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8b281-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b281-119">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8b281-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b281-120">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b281-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b281-121">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8b281-121">Scenario description</span></span>
<span data-ttu-id="8b281-122">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8b281-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b281-123">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8b281-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b281-124">Добавление рабочей области Autotask из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8b281-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="8b281-125">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b281-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="8b281-126">Добавление рабочей области Autotask из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8b281-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="8b281-127">tooconfigure hello интеграции Autotask рабочая область в Azure AD, вы должны tooadd Autotask рабочей области из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8b281-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b281-128">**tooadd Autotask рабочей области из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8b281-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b281-129">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8b281-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="8b281-131">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8b281-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8b281-132">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b281-132">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="8b281-134">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8b281-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="8b281-136">Введите в поле поиска hello **рабочему месту Autotask**выберите **Autotask рабочему месту** из панели «результат» нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8b281-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Список результатов в рабочей области Autotask в hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8b281-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b281-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8b281-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Autotask Workplace с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b281-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8b281-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочей области Autotask является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b281-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="8b281-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочей области Autotask должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8b281-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="8b281-142">В рабочей области Autotask, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8b281-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8b281-143">tooconfigure и тестирования Azure AD единого входа в рабочей области Autotask, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8b281-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8b281-144">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8b281-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8b281-145">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8b281-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b281-146">**[Создание тестового пользователя, прошедшего рабочему месту Autotask](#create-an-autotask-workplace-test-user)**  -toohave аналог Саймон Britta в рабочей области Autotask, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8b281-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b281-147">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8b281-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b281-148">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8b281-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8b281-149">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b281-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8b281-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Autotask рабочей области.</span><span class="sxs-lookup"><span data-stu-id="8b281-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="8b281-151">**tooconfigure Azure AD единого входа в рабочей области Autotask, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8b281-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b281-152">В hello в hello портала Azure **рабочему месту Autotask** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8b281-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="8b281-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8b281-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="8b281-156">При необходимости приложение hello tooconfigure в **поставщика Удостоверений** инициировал режим, выполните следующие действия на hello hello **Autotask рабочей области домена и URL-адреса** раздела:</span><span class="sxs-lookup"><span data-stu-id="8b281-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![Сведения о домене и URL-адресах единого входа для IDP приложения Autotask Workplace](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="8b281-158">а.</span><span class="sxs-lookup"><span data-stu-id="8b281-158">a.</span></span> <span data-ttu-id="8b281-159">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="8b281-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="8b281-160">b.</span><span class="sxs-lookup"><span data-stu-id="8b281-160">b.</span></span> <span data-ttu-id="8b281-161">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="8b281-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="8b281-162">При необходимости приложение hello tooconfigure в **SP** инициируемых режим, проверка **Показывать дополнительные параметры URL-адреса** и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8b281-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для IDP приложения Autotask Workplace](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="8b281-164">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="8b281-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="8b281-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8b281-165">These values are not real.</span></span> <span data-ttu-id="8b281-166">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8b281-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="8b281-167">Обратитесь к [Autotask клиента рабочей группы поддержки](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="8b281-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="8b281-168">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8b281-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="8b281-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8b281-170">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8b281-172">В другом окне браузера вход с использованием сети tooWorkplace hello учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="8b281-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="8b281-173">При настройке поставщика удостоверений hello, дочерний домен потребуется toobe указано.</span><span class="sxs-lookup"><span data-stu-id="8b281-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="8b281-174">tooconfirm hello правильный поддомен, tooWorkplace входа через Интернет.</span><span class="sxs-lookup"><span data-stu-id="8b281-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="8b281-175">После входа в систему в делают поддомен toohello Примечание в URL-АДРЕСЕ hello.</span><span class="sxs-lookup"><span data-stu-id="8b281-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="8b281-176">Hello поддомен входит в состав hello между hello «https://» и «.awp.autotask.net/» и должен быть нам, Европа, ЦС или Австралия.</span><span class="sxs-lookup"><span data-stu-id="8b281-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="8b281-177">Go слишком**конфигурации** > **Single Sign-On** и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="8b281-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Конфигурация единого входа в Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="8b281-179">а.</span><span class="sxs-lookup"><span data-stu-id="8b281-179">a.</span></span> <span data-ttu-id="8b281-180">Выберите hello **файлом метаданных XML** параметр, а затем отправьте hello **метаданные в формате XML** загружен с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8b281-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="8b281-181">b.</span><span class="sxs-lookup"><span data-stu-id="8b281-181">b.</span></span> <span data-ttu-id="8b281-182">Нажмите кнопку **Enable SSO** (Включить единый вход).</span><span class="sxs-lookup"><span data-stu-id="8b281-182">Click **Enable SSO**.</span></span>
    
    ![Подтверждение конфигурации единого входа в Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="8b281-184">c.</span><span class="sxs-lookup"><span data-stu-id="8b281-184">c.</span></span> <span data-ttu-id="8b281-185">Выберите hello **я подтвердить правильность этих сведений, и я доверяю этого поставщика удостоверений** флажок.</span><span class="sxs-lookup"><span data-stu-id="8b281-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="8b281-186">d.</span><span class="sxs-lookup"><span data-stu-id="8b281-186">d.</span></span> <span data-ttu-id="8b281-187">Нажмите кнопку **Утвердить**.</span><span class="sxs-lookup"><span data-stu-id="8b281-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="8b281-188">Если вам требуется помощь по настройке Autotask рабочему месту, см. в разделе [эту страницу](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget помощь с рабочей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8b281-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="8b281-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8b281-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8b281-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8b281-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8b281-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b281-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8b281-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b281-192">Create an Azure AD test user</span></span>

<span data-ttu-id="8b281-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8b281-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="8b281-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8b281-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b281-196">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="8b281-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8b281-198">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8b281-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8b281-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="8b281-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8b281-202">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8b281-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8b281-204">а.</span><span class="sxs-lookup"><span data-stu-id="8b281-204">a.</span></span> <span data-ttu-id="8b281-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b281-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b281-206">b.</span><span class="sxs-lookup"><span data-stu-id="8b281-206">b.</span></span> <span data-ttu-id="8b281-207">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8b281-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8b281-208">c.</span><span class="sxs-lookup"><span data-stu-id="8b281-208">c.</span></span> <span data-ttu-id="8b281-209">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="8b281-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8b281-210">d.</span><span class="sxs-lookup"><span data-stu-id="8b281-210">d.</span></span> <span data-ttu-id="8b281-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8b281-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="8b281-212">Создание тестового пользователя Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="8b281-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="8b281-213">В этом разделе описано, как создать пользователя Britta Simon в приложении Autotask.</span><span class="sxs-lookup"><span data-stu-id="8b281-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="8b281-214">Обратитесь [Autotask рабочей группой поддержки](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd пользователей hello в hello платформы Autotask рабочей области.</span><span class="sxs-lookup"><span data-stu-id="8b281-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8b281-215">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8b281-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8b281-216">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAutotask доступа к рабочему месту.</span><span class="sxs-lookup"><span data-stu-id="8b281-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="8b281-218">**tooassign tooAutotask Britta Simon рабочему месту, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="8b281-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b281-219">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b281-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8b281-221">В списке приложений hello выберите **рабочему месту Autotask**.</span><span class="sxs-lookup"><span data-stu-id="8b281-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![Hello ссылку Autotask рабочей области в списке приложений hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="8b281-223">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8b281-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="8b281-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8b281-225">Click **Add** button.</span></span> <span data-ttu-id="8b281-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8b281-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="8b281-228">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8b281-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8b281-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8b281-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b281-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8b281-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8b281-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8b281-231">Test single sign-on</span></span>

<span data-ttu-id="8b281-232">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8b281-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8b281-233">При нажатии кнопки hello рабочему месту Autotask плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Autotask рабочей области приложения.</span><span class="sxs-lookup"><span data-stu-id="8b281-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="8b281-234">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8b281-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b281-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8b281-235">Additional resources</span></span>

* [<span data-ttu-id="8b281-236">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b281-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b281-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b281-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

