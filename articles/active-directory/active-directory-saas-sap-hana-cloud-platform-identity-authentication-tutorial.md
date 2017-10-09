---
title: "Руководство по интеграции Azure Active Directory с приложением SAP HANA Cloud Platform Identity Authentication | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SAP HANA облачной платформы удостоверений проверки подлинности."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="50f93-103">Руководство по интеграции Azure Active Directory с приложением SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="50f93-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="50f93-104">В этом учебнике вы узнаете, как toointegrate SAP HANA облачной платформы удостоверений проверки подлинности в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50f93-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="50f93-105">Проверка подлинности облачной платформы SAP HANA идентификатора используется в качестве прокси-сервера поставщика удостоверений tooaccess приложения SAP с помощью Azure AD как hello основного поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="50f93-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="50f93-106">Интеграция проверки подлинности облачной платформы SAP HANA удостоверений с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="50f93-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="50f93-107">Можно управлять в Azure AD, имеющего доступ tooSAP приложения</span><span class="sxs-lookup"><span data-stu-id="50f93-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="50f93-108">Можно включить на пользователей tooautomatically get tooSAP вошедшего приложения единого входа (SSO) с их учетными записями Azure AD</span><span class="sxs-lookup"><span data-stu-id="50f93-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="50f93-109">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="50f93-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="50f93-110">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50f93-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="50f93-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="50f93-111">Prerequisites</span></span>

<span data-ttu-id="50f93-112">tooconfigure интеграция Azure AD с помощью проверки подлинности облачной платформы SAP HANA удостоверений необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="50f93-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="50f93-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="50f93-113">An Azure AD subscription</span></span>
- <span data-ttu-id="50f93-114">Подписка на **SAP HANA Cloud Platform Identity Authentication** с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="50f93-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="50f93-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="50f93-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="50f93-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="50f93-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50f93-117">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="50f93-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="50f93-118">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50f93-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50f93-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="50f93-119">Scenario description</span></span>
<span data-ttu-id="50f93-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="50f93-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="50f93-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="50f93-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50f93-122">Добавление проверки подлинности облачной платформы SAP HANA удостоверений из галереи hello</span><span class="sxs-lookup"><span data-stu-id="50f93-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="50f93-123">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50f93-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="50f93-124">Прежде чем углубляться в технические подробности hello, это жизненно важных toounderstand hello концепции, с которыми вы будете toolook на.</span><span class="sxs-lookup"><span data-stu-id="50f93-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="50f93-125">Hello федерации проверки подлинности облачной платформы SAP HANA удостоверений и Azure Active Directory позволяет tooimplement единого входа для приложений или служб, защищенных AAD (в качестве поставщика удостоверений) с приложениями SAP и службах, защищенных облачной платформы SAP HANA удостоверение Проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="50f93-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="50f93-126">В настоящее время проверки подлинности облачной платформы SAP HANA удостоверение выступает в качестве поставщика удостоверений прокси tooSAP приложения.</span><span class="sxs-lookup"><span data-stu-id="50f93-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="50f93-127">В свою очередь, Azure Active Directory выступает в качестве hello начальные поставщика удостоверений в этой программе установки.</span><span class="sxs-lookup"><span data-stu-id="50f93-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="50f93-128">Привет, следующая схема иллюстрирует это:</span><span class="sxs-lookup"><span data-stu-id="50f93-128">hello following diagram illustrates this:</span></span>    

![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="50f93-130">При такой конфигурации клиент SAP HANA Cloud Platform Identity Authentication будет настроен как надежное приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="50f93-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="50f93-131">Все приложения SAP и службы будут tooprotect через таким образом впоследствии настраиваются в консоли управления для проверки подлинности облачной платформы SAP HANA удостоверение hello!</span><span class="sxs-lookup"><span data-stu-id="50f93-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="50f93-132">Это означает, что авторизации для предоставления доступа tooSAP приложений и служб месте tootake потребности в проверке подлинности облачной платформы SAP HANA удостоверение для установки (как противоположность tooconfiguring авторизации в Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="50f93-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="50f93-133">Путем настройки проверки подлинности облачной платформы SAP HANA удостоверения как приложение через hello Azure Active Directory Marketplace, нет необходимости tootake заботиться о настройке необходимых утверждений отдельных / утверждений SAML и преобразования необходимости tooproduce действительный токен проверки подлинности для приложений SAP.</span><span class="sxs-lookup"><span data-stu-id="50f93-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="50f93-134">В настоящее время единый вход для интернет-решений был проверен только обеими сторонами.</span><span class="sxs-lookup"><span data-stu-id="50f93-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="50f93-135">Потоки, необходимые для связи "приложение — API" и "API — API", работают, но они еще не проверялись.</span><span class="sxs-lookup"><span data-stu-id="50f93-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="50f93-136">Они будут проверены в ходе последующих действий.</span><span class="sxs-lookup"><span data-stu-id="50f93-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="50f93-137">Добавление проверки подлинности облачной платформы SAP HANA удостоверений из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="50f93-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="50f93-138">tooconfigure hello интеграции проверки подлинности облачной платформы SAP HANA удостоверений в Azure AD, вы должны tooadd проверки подлинности облачной платформы SAP HANA удостоверений из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="50f93-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="50f93-139">**tooadd аутентификации SAP HANA облачной платформы удостоверений из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="50f93-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="50f93-140">В hello [ **портал управления Azure**](https://portal.azure.com)на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="50f93-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="50f93-142">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="50f93-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="50f93-143">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="50f93-143">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="50f93-145">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="50f93-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="50f93-147">Введите в поле поиска hello **проверки подлинности облачной платформы SAP HANA удостоверение**.</span><span class="sxs-lookup"><span data-stu-id="50f93-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="50f93-149">В панели результатов hello выберите **проверки подлинности облачной платформы SAP HANA удостоверение**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="50f93-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="50f93-151">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="50f93-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="50f93-152">В этом разделе описана настройка и проверка единого входа Azure AD в SAP HANA Cloud Platform Identity Authentication с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50f93-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50f93-153">Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в проверке подлинности облачной платформы SAP HANA удостоверение является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50f93-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="50f93-154">Другими словами связи между пользователя Azure AD и связанных пользователей hello в SAP HANA облачной платформы удостоверений проверки подлинности должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="50f93-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="50f93-155">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в проверке подлинности облачной платформы SAP HANA удостоверение.</span><span class="sxs-lookup"><span data-stu-id="50f93-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="50f93-156">tooconfigure и тестирования единого входа Azure AD, с проверкой подлинности облачной платформы SAP HANA удостоверение, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="50f93-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="50f93-157">**[Настройка Azure AD единого входа](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="50f93-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="50f93-158">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="50f93-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50f93-159">**[Создание тестового пользователя проверки подлинности облачной платформы SAP HANA удостоверение](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave аналог Саймон Britta в SAP HANA облачной платформы удостоверений проверки подлинности, который является представлением ей связанного toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50f93-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="50f93-160">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="50f93-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50f93-161">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="50f93-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="50f93-162">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="50f93-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="50f93-163">В этом разделе Включить единый вход Azure AD на портале управления Azure hello и настроить единый вход в приложение проверки подлинности облачной платформы SAP HANA удостоверений.</span><span class="sxs-lookup"><span data-stu-id="50f93-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="50f93-164">Проверка подлинности облачной платформы SAP HANA удостоверения приложения ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="50f93-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="50f93-165">Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="50f93-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="50f93-166">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="50f93-166">hello following screenshot shows an example for this.</span></span>

![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="50f93-168">**tooconfigure SSO Azure AD с SAP HANA облачной платформы удостоверений проверки подлинности, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="50f93-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="50f93-169">На портале управления Azure hello на hello **проверки подлинности облачной платформы SAP HANA удостоверение** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="50f93-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="50f93-171">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="50f93-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа][5]

3. <span data-ttu-id="50f93-173">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалоговое окно, если для приложения SAP требуется атрибут, например «firstName».</span><span class="sxs-lookup"><span data-stu-id="50f93-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="50f93-174">В диалоговом окне атрибутов токена SAML hello добавьте атрибут «firstName» hello.</span><span class="sxs-lookup"><span data-stu-id="50f93-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="50f93-175">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="50f93-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Настройка единого входа][6]

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="50f93-178">В hello **имя атрибута** в текстовое поле имя атрибута типа hello «firstName».</span><span class="sxs-lookup"><span data-stu-id="50f93-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="50f93-179">Из hello **значение атрибута** список, выберите hello значение атрибута «user.givenname».</span><span class="sxs-lookup"><span data-stu-id="50f93-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="50f93-180">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="50f93-180">Click **Ok**.</span></span>

4. <span data-ttu-id="50f93-181">На hello **URL-адреса и SAP HANA облачной платформы удостоверений проверки подлинности домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="50f93-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="50f93-183">В hello **на URL-адрес входа** текстовом поле введите знак hello на URL-адрес для приложения hello SAP.</span><span class="sxs-lookup"><span data-stu-id="50f93-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="50f93-184">В hello **идентификатор** текстовое поле, значение типа hello следующий шаблон:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="50f93-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="50f93-185">Если вы не знаете это значение, следуйте документации проверки подлинности облачной платформы SAP HANA удостоверение hello в [конфигурации SAML 2.0 клиента](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="50f93-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="50f93-186">На hello **настройки проверки подлинности для облачной платформы SAP HANA удостоверение** щелкните **Настройка SAP HANA облачной платформы удостоверений проверки подлинности** tooopen **Настройкавхода** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="50f93-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="50f93-187">Щелкните на **метаданных XML SAML** и сохраните файл hello на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="50f93-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="50f93-190">tooget единого входа, настроенному для вашего приложения перейдите tooSAP HANA облачной платформы удостоверений проверки подлинности консоли администрирования.</span><span class="sxs-lookup"><span data-stu-id="50f93-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="50f93-191">URL-адрес Hello имеет hello следующий шаблон:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="50f93-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="50f93-192">Следуйте hello документации для проверки подлинности облачной платформы SAP HANA удостоверение слишком[Настройка Microsoft Azure AD в качестве организации поставщика удостоверений в SAP HANA облачной платформы удостоверений проверки подлинности](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="50f93-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="50f93-193">На портале управления Azure hello щелкните **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="50f93-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="50f93-194">По-прежнему hello, выполнив действия, только в том случае, если нужно tooadd и Включение единого входа для другого приложения SAP.</span><span class="sxs-lookup"><span data-stu-id="50f93-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="50f93-195">Повторите шаги в разделе hello раздел «Добавление SAP HANA облачной платформы удостоверений проверки подлинности из галереи hello» tooadd другой экземпляр SAP HANA облачной платформы удостоверений проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="50f93-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="50f93-196">На портале управления Azure hello на hello **проверки подлинности облачной платформы SAP HANA удостоверение** странице интеграции приложения щелкните **входа на связанный**.</span><span class="sxs-lookup"><span data-stu-id="50f93-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Настройка связанного единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="50f93-198">Сохраните конфигурацию hello.</span><span class="sxs-lookup"><span data-stu-id="50f93-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="50f93-199">новое приложение Hello будет использовать hello настройку единого входа для предыдущего SAP приложения hello.</span><span class="sxs-lookup"><span data-stu-id="50f93-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="50f93-200">Убедитесь, что вы используйте hello же корпоративной поставщиков удостоверений в hello проверки подлинности консоли администрирования облачной платформы SAP HANA удостоверений.</span><span class="sxs-lookup"><span data-stu-id="50f93-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="50f93-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="50f93-201">Create an Azure AD test user</span></span>
<span data-ttu-id="50f93-202">Hello цель этого раздела — toocreate тестового пользователя на новом портале hello вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="50f93-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="50f93-204">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="50f93-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="50f93-205">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="50f93-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="50f93-207">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="50f93-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="50f93-209">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="50f93-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="50f93-211">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="50f93-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="50f93-213">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50f93-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="50f93-214">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="50f93-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="50f93-215">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="50f93-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="50f93-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="50f93-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="50f93-217">Создание тестового пользователя SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="50f93-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="50f93-218">Toocreate проверки подлинности облачной платформы SAP HANA удостоверение пользователя не требуется.</span><span class="sxs-lookup"><span data-stu-id="50f93-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="50f93-219">Пользователи находятся в хранилище пользователя hello Azure AD могут использовать функциональные возможности Единого hello.</span><span class="sxs-lookup"><span data-stu-id="50f93-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="50f93-220">Проверка подлинности облачной платформы SAP HANA идентификатора поддерживает параметр hello федерации удостоверений.</span><span class="sxs-lookup"><span data-stu-id="50f93-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="50f93-221">Этот параметр позволяет toocheck приложения hello, если проверку подлинности поставщиком hello корпоративными удостоверениями пользователей hello существует в hello хранилища из SAP HANA облачной платформы удостоверений проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="50f93-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="50f93-222">При параметрах по умолчанию hello hello федерации удостоверений параметр отключен.</span><span class="sxs-lookup"><span data-stu-id="50f93-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="50f93-223">При включении федерации удостоверений hello только тех пользователей, импортируемые в SAP HANA облачной платформы удостоверений проверки подлинности, приложение может tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="50f93-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="50f93-224">Дополнительные сведения о том, как tooenable или отключите федерации удостоверений с SAP HANA облачной платформы удостоверений проверки подлинности, отображается включить федерацию удостоверений с аутентификацией SAP HANA облачной платформы удостоверений в [Настройка федерации удостоверений с hello хранилища из SAP HANA облачной платформы удостоверений проверки подлинности пользователя. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="50f93-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="50f93-225">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="50f93-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="50f93-226">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooSAP HANA облачной платформы удостоверений проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="50f93-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="50f93-228">**tooassign tooSAP Britta Simon HANA облачной платформы удостоверений проверки подлинности, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="50f93-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="50f93-229">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="50f93-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="50f93-231">В списке приложений hello выберите **проверки подлинности облачной платформы SAP HANA удостоверение**.</span><span class="sxs-lookup"><span data-stu-id="50f93-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="50f93-233">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="50f93-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="50f93-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="50f93-235">Click **Add** button.</span></span> <span data-ttu-id="50f93-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="50f93-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="50f93-238">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="50f93-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="50f93-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="50f93-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50f93-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="50f93-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="50f93-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="50f93-241">Test single sign-on</span></span>

<span data-ttu-id="50f93-242">В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="50f93-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="50f93-243">Если щелкнуть плитку проверки подлинности облачной платформы SAP HANA удостоверение hello в hello панели доступа, следует получать автоматически вошедшего tooyour проверки подлинности облачной платформы SAP HANA удостоверение приложения.</span><span class="sxs-lookup"><span data-stu-id="50f93-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="50f93-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="50f93-244">Additional resources</span></span>

* [<span data-ttu-id="50f93-245">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50f93-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50f93-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50f93-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png