---
title: "Руководство по интеграции Azure Active Directory с порталом управления облачными службами для Microsoft Azure | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и портал управления облако Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="356e1-103">Учебник. Интеграция Azure Active Directory с порталом управления облачными службами для Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="356e1-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="356e1-104">В этом учебнике вы узнаете, как toointegrate облака портал управления для Microsoft Azure в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="356e1-104">In this tutorial, you learn how toointegrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="356e1-105">Интеграция с Azure AD портал управления облако Microsoft Azure предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="356e1-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="356e1-106">Можно управлять в Azure AD, имеющего доступ tooCloud портал управления для Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="356e1-106">You can control in Azure AD who has access tooCloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="356e1-107">Ваш пользователей tooautomatically get вошедшего tooCloud портал управления для Microsoft Azure (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="356e1-107">You can enable your users tooautomatically get signed-on tooCloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="356e1-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="356e1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="356e1-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="356e1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="356e1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="356e1-110">Prerequisites</span></span>

<span data-ttu-id="356e1-111">tooconfigure интеграция Azure AD с портала управления облака для Microsoft Azure требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="356e1-111">tooconfigure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need hello following items:</span></span>

- <span data-ttu-id="356e1-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="356e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="356e1-113">подписка портала управления облачными службами для Microsoft Azure с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="356e1-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="356e1-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="356e1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="356e1-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="356e1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="356e1-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="356e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="356e1-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="356e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="356e1-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="356e1-118">Scenario description</span></span>
<span data-ttu-id="356e1-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="356e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="356e1-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="356e1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="356e1-121">Добавление облака портал управления для Microsoft Azure из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="356e1-121">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
2. <span data-ttu-id="356e1-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="356e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a><span data-ttu-id="356e1-123">Добавление облака портал управления для Microsoft Azure из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="356e1-123">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
<span data-ttu-id="356e1-124">tooconfigure hello интеграции облака портал управления для Microsoft Azure в Azure AD, необходимо tooadd облака портал управления для Microsoft Azure из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="356e1-124">tooconfigure hello integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need tooadd Cloud Management Portal for Microsoft Azure from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="356e1-125">**tooadd облака портал управления для Microsoft Azure из коллекции hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="356e1-125">**tooadd Cloud Management Portal for Microsoft Azure from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="356e1-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="356e1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="356e1-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="356e1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="356e1-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="356e1-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="356e1-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="356e1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="356e1-133">Введите в поле поиска hello **облака портал управления для Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="356e1-133">In hello search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="356e1-135">В панели результатов hello выберите **облака портал управления для Microsoft Azure**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="356e1-135">In hello results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="356e1-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="356e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="356e1-138">В этом разделе описывается настройка и проверка единого входа Azure AD на портале управления облачными службами в Microsoft Azure с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="356e1-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="356e1-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в облаке портал управления для Microsoft Azure является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="356e1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cloud Management Portal for Microsoft Azure is tooa user in Azure AD.</span></span> <span data-ttu-id="356e1-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей на портале управления облака для Microsoft Azure должна установить toobe.</span><span class="sxs-lookup"><span data-stu-id="356e1-140">In other words, a link relationship between an Azure AD user and hello related user in Cloud Management Portal for Microsoft Azure needs toobe established.</span></span>

<span data-ttu-id="356e1-141">На портале управления облака для Microsoft Azure, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="356e1-141">In Cloud Management Portal for Microsoft Azure, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="356e1-142">tooconfigure и выполнить проверку Azure AD единого входа с помощью портала управления облако Microsoft Azure, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="356e1-142">tooconfigure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="356e1-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="356e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="356e1-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="356e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="356e1-145">**[Создание облака портал управления для тестового пользователя Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  -toohave аналог Саймон Britta на портале управления облака для Microsoft Azure, которая является представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="356e1-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - toohave a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="356e1-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="356e1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="356e1-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="356e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="356e1-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="356e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="356e1-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в портал управления облачные приложения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="356e1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="356e1-150">**tooconfigure Azure AD единого входа с помощью портала управления облака для Microsoft Azure выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="356e1-150">**tooconfigure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="356e1-151">В hello в hello портала Azure **облака портал управления для Microsoft Azure** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="356e1-151">In hello Azure portal, on hello **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="356e1-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="356e1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="356e1-155">На hello **портала управления Cloud домена Microsoft Azure и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="356e1-155">On hello **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="356e1-157">а.</span><span class="sxs-lookup"><span data-stu-id="356e1-157">a.</span></span> <span data-ttu-id="356e1-158">В hello **URL-адрес входа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="356e1-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="356e1-159">b.</span><span class="sxs-lookup"><span data-stu-id="356e1-159">b.</span></span> <span data-ttu-id="356e1-160">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="356e1-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="356e1-161">c.</span><span class="sxs-lookup"><span data-stu-id="356e1-161">c.</span></span> <span data-ttu-id="356e1-162">В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="356e1-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="356e1-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="356e1-163">These values are not real.</span></span> <span data-ttu-id="356e1-164">Обновите эти значения с hello фактический URL-адрес входа, идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="356e1-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="356e1-165">Обратитесь к [облака портал управления для поддержки клиент Microsoft Azure](mailto:jczernuszka@newsignature.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="356e1-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="356e1-166">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="356e1-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="356e1-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="356e1-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="356e1-170">На hello **облака портал управления для Microsoft Azure конфигурации** щелкните **Настройка облака портал управления Microsoft Azure** tooopen **Настройкавхода**окна.</span><span class="sxs-lookup"><span data-stu-id="356e1-170">On hello **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="356e1-171">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="356e1-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="356e1-173">tooconfigure единого входа на **облака портал управления для Microsoft Azure** стороны, необходимо загрузить hello toosend **сертификат**, **URL-адрес выхода**, **SAML единого входа URL-адрес службы** и **идентификатор сущности SAML** слишком[облака портал управления для поддержки Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="356e1-173">tooconfigure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="356e1-174">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="356e1-174">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="356e1-175">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="356e1-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="356e1-176">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="356e1-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="356e1-177">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="356e1-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="356e1-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="356e1-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="356e1-179">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="356e1-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="356e1-181">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="356e1-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="356e1-182">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="356e1-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="356e1-184">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="356e1-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="356e1-186">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="356e1-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="356e1-188">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="356e1-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="356e1-190">а.</span><span class="sxs-lookup"><span data-stu-id="356e1-190">a.</span></span> <span data-ttu-id="356e1-191">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="356e1-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="356e1-192">b.</span><span class="sxs-lookup"><span data-stu-id="356e1-192">b.</span></span> <span data-ttu-id="356e1-193">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="356e1-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="356e1-194">c.</span><span class="sxs-lookup"><span data-stu-id="356e1-194">c.</span></span> <span data-ttu-id="356e1-195">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="356e1-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="356e1-196">d.</span><span class="sxs-lookup"><span data-stu-id="356e1-196">d.</span></span> <span data-ttu-id="356e1-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="356e1-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="356e1-198">Создание тестового пользователя портала управления облачными службами для Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="356e1-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="356e1-199">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon на портале управления облака для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="356e1-199">hello objective of this section is toocreate a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="356e1-200">Можно работать с [облака портал управления для поддержки Microsoft Azure](mailto:jczernuszka@newsignature.com) tooadd пользователей hello в hello портала управления Cloud для учетной записи Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="356e1-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) tooadd hello users in hello Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="356e1-201">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="356e1-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="356e1-202">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCloud портал управления для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="356e1-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloud Management Portal for Microsoft Azure.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="356e1-204">**tooassign tooCloud Britta Simon портал управления для Microsoft Azure, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="356e1-204">**tooassign Britta Simon tooCloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="356e1-205">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="356e1-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="356e1-207">В списке приложений hello выберите **облака портал управления для Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="356e1-207">In hello applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="356e1-209">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="356e1-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="356e1-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="356e1-211">Click **Add** button.</span></span> <span data-ttu-id="356e1-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="356e1-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="356e1-214">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="356e1-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="356e1-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="356e1-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="356e1-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="356e1-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="356e1-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="356e1-217">Testing single sign-on</span></span>

<span data-ttu-id="356e1-218">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="356e1-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="356e1-219">При нажатии кнопки hello облака портал управления для Microsoft Azure плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на портал управления облака для приложения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="356e1-219">When you click hello Cloud Management Portal for Microsoft Azure tile in hello Access Panel, you should get automatically signed-on tooyour Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="356e1-220">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="356e1-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="356e1-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="356e1-221">Additional resources</span></span>

* [<span data-ttu-id="356e1-222">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="356e1-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="356e1-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="356e1-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

