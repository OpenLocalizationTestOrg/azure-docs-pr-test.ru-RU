---
title: "Руководство по интеграции Azure Active Directory с Sansan | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Sansan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: f58cc613a2e3a240e555b61a34db4155eb9dff71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="264aa-103">Руководство по интеграции Azure Active Directory с Sansan</span><span class="sxs-lookup"><span data-stu-id="264aa-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="264aa-104">В этом учебнике вы узнаете, как toointegrate Sansan с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="264aa-104">In this tutorial, you learn how toointegrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="264aa-105">Интеграция с Azure AD Sansan предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="264aa-105">Integrating Sansan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="264aa-106">Можно управлять в Azure AD, имеющего доступ tooSansan</span><span class="sxs-lookup"><span data-stu-id="264aa-106">You can control in Azure AD who has access tooSansan</span></span>
- <span data-ttu-id="264aa-107">Можно включить на пользователей tooautomatically get вошедшего tooSansan (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="264aa-107">You can enable your users tooautomatically get signed-on tooSansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="264aa-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="264aa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="264aa-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="264aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="264aa-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="264aa-110">Prerequisites</span></span>

<span data-ttu-id="264aa-111">tooconfigure интеграция Azure AD с Sansan требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="264aa-111">tooconfigure Azure AD integration with Sansan, you need hello following items:</span></span>

- <span data-ttu-id="264aa-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="264aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="264aa-113">подписка Sansan с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="264aa-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="264aa-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="264aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="264aa-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="264aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="264aa-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="264aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="264aa-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="264aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="264aa-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="264aa-118">Scenario description</span></span>
<span data-ttu-id="264aa-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="264aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="264aa-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="264aa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="264aa-121">Добавление Sansan из галереи hello</span><span class="sxs-lookup"><span data-stu-id="264aa-121">Adding Sansan from hello gallery</span></span>
2. <span data-ttu-id="264aa-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="264aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-hello-gallery"></a><span data-ttu-id="264aa-123">Добавление Sansan из галереи hello</span><span class="sxs-lookup"><span data-stu-id="264aa-123">Adding Sansan from hello gallery</span></span>
<span data-ttu-id="264aa-124">tooconfigure hello интеграции Sansan в Azure AD, вы должны tooadd Sansan из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="264aa-124">tooconfigure hello integration of Sansan into Azure AD, you need tooadd Sansan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="264aa-125">**tooadd Sansan из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="264aa-125">**tooadd Sansan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="264aa-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="264aa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="264aa-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="264aa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="264aa-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="264aa-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="264aa-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="264aa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="264aa-133">Введите в поле поиска hello **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="264aa-133">In hello search box, type **Sansan**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="264aa-135">В панели результатов hello выберите **Sansan**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="264aa-135">In hello results panel, select **Sansan**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="264aa-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="264aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="264aa-138">В этом разделе описана настройка и проверка единого входа Azure AD в Sansan с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="264aa-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="264aa-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Sansan является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="264aa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sansan is tooa user in Azure AD.</span></span> <span data-ttu-id="264aa-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Sansan должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="264aa-140">In other words, a link relationship between an Azure AD user and hello related user in Sansan needs toobe established.</span></span>

<span data-ttu-id="264aa-141">В Sansan, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="264aa-141">In Sansan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="264aa-142">tooconfigure и теста Azure AD единого входа с Sansan, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="264aa-142">tooconfigure and test Azure AD single sign-on with Sansan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="264aa-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="264aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="264aa-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="264aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="264aa-145">**[Создание тестового пользователя Sansan](#creating-a-sansan-test-user)**  -toohave аналог Саймон Britta в Sansan, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="264aa-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - toohave a counterpart of Britta Simon in Sansan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="264aa-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="264aa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="264aa-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="264aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="264aa-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="264aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="264aa-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Sansan.</span><span class="sxs-lookup"><span data-stu-id="264aa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="264aa-150">**tooconfigure Azure AD единого входа с Sansan, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="264aa-150">**tooconfigure Azure AD single sign-on with Sansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="264aa-151">В hello в hello портала Azure **Sansan** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="264aa-151">In hello Azure portal, on hello **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="264aa-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="264aa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="264aa-155">На hello **URL-адреса и домена Sansan** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="264aa-155">On hello **Sansan Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="264aa-157">а.</span><span class="sxs-lookup"><span data-stu-id="264aa-157">a.</span></span> <span data-ttu-id="264aa-158">В hello **URL-адрес входа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="264aa-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | <span data-ttu-id="264aa-159">Среда</span><span class="sxs-lookup"><span data-stu-id="264aa-159">Environment</span></span> | <span data-ttu-id="264aa-160">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="264aa-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="264aa-161">Компьютерная сеть</span><span class="sxs-lookup"><span data-stu-id="264aa-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="264aa-162">Собственное мобильное приложение</span><span class="sxs-lookup"><span data-stu-id="264aa-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="264aa-163">Параметры браузера для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="264aa-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="264aa-164">b.</span><span class="sxs-lookup"><span data-stu-id="264aa-164">b.</span></span> <span data-ttu-id="264aa-165">В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="264aa-165">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="264aa-166">Среда</span><span class="sxs-lookup"><span data-stu-id="264aa-166">Environment</span></span>             | <span data-ttu-id="264aa-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="264aa-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="264aa-168">Компьютерная сеть</span><span class="sxs-lookup"><span data-stu-id="264aa-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="264aa-169">Собственное мобильное приложение</span><span class="sxs-lookup"><span data-stu-id="264aa-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="264aa-170">Параметры браузера для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="264aa-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="264aa-171">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="264aa-171">These values are not real.</span></span> <span data-ttu-id="264aa-172">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="264aa-172">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="264aa-173">Обратитесь к [группа поддержки клиента Sansan](https://www.sansan.com/form/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="264aa-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) tooget these values.</span></span> 

4. <span data-ttu-id="264aa-174">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="264aa-174">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="264aa-176">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="264aa-176">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="264aa-178">На hello **конфигурации Sansan** щелкните **Настройка Sansan** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="264aa-178">On hello **Sansan Configuration** section, click **Configure Sansan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="264aa-179">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="264aa-179">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="264aa-181">tooconfigure единого входа на **Sansan** стороны, необходимо загрузить hello toosend **сертификат**, **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** слишком[Sansan поддержки](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="264aa-181">tooconfigure single sign-on on **Sansan** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="264aa-182">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="264aa-182">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="264aa-183">Настройка браузера ПК подходит как для мобильного приложения и браузера для мобильных устройств, так и для компьютерной сети.</span><span class="sxs-lookup"><span data-stu-id="264aa-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="264aa-184">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="264aa-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="264aa-185">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="264aa-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="264aa-186">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="264aa-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="264aa-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="264aa-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="264aa-188">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="264aa-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="264aa-190">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="264aa-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="264aa-191">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="264aa-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="264aa-193">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="264aa-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="264aa-195">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="264aa-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="264aa-197">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="264aa-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="264aa-199">а.</span><span class="sxs-lookup"><span data-stu-id="264aa-199">a.</span></span> <span data-ttu-id="264aa-200">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="264aa-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="264aa-201">b.</span><span class="sxs-lookup"><span data-stu-id="264aa-201">b.</span></span> <span data-ttu-id="264aa-202">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="264aa-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="264aa-203">c.</span><span class="sxs-lookup"><span data-stu-id="264aa-203">c.</span></span> <span data-ttu-id="264aa-204">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="264aa-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="264aa-205">d.</span><span class="sxs-lookup"><span data-stu-id="264aa-205">d.</span></span> <span data-ttu-id="264aa-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="264aa-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="264aa-207">Создание тестового пользователя Sansan</span><span class="sxs-lookup"><span data-stu-id="264aa-207">Creating a Sansan test user</span></span>

<span data-ttu-id="264aa-208">В этом разделе описано, как создать пользователя Britta Simon в приложении SanSan.</span><span class="sxs-lookup"><span data-stu-id="264aa-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="264aa-209">SanSan приложению toobe пользователя hello подготовить в приложении hello перед выполнением единого входа.</span><span class="sxs-lookup"><span data-stu-id="264aa-209">SanSan application needs hello user toobe provisioned in hello application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="264aa-210">Если требуется toocreate пользователь вручную или пакета пользователей, вы должны toocontact hello [Sansan поддержки](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="264aa-210">If you need toocreate a user manually or batch of users, you need toocontact hello [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="264aa-211">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="264aa-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="264aa-212">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSansan доступа.</span><span class="sxs-lookup"><span data-stu-id="264aa-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSansan.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="264aa-214">**tooassign tooSansan Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="264aa-214">**tooassign Britta Simon tooSansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="264aa-215">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="264aa-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="264aa-217">В списке приложений hello выберите **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="264aa-217">In hello applications list, select **Sansan**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="264aa-219">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="264aa-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="264aa-221">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="264aa-221">Click **Add** button.</span></span> <span data-ttu-id="264aa-222">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="264aa-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="264aa-224">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="264aa-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="264aa-225">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="264aa-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="264aa-226">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="264aa-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="264aa-227">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="264aa-227">Testing single sign-on</span></span>

<span data-ttu-id="264aa-228">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="264aa-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="264aa-229">При нажатии кнопки hello Sansan плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Sansan приложения.</span><span class="sxs-lookup"><span data-stu-id="264aa-229">When you click hello Sansan tile in hello Access Panel, you should get automatically signed-on tooyour Sansan application.</span></span>
<span data-ttu-id="264aa-230">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="264aa-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="264aa-231">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="264aa-231">Additional resources</span></span>

* [<span data-ttu-id="264aa-232">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="264aa-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="264aa-233">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="264aa-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

