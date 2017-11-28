---
title: "Руководство по интеграции Azure Active Directory с Zscaler Private Access (ZPA) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zscaler закрытый доступ (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="9aee7-103">Руководство по интеграции Azure Active Directory с Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="9aee7-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="9aee7-104">В этом учебнике вы узнаете, как toointegrate Zscaler закрытый доступ (ZPA) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9aee7-104">In this tutorial, you learn how toointegrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9aee7-105">Интеграция с Azure AD Zscaler закрытый доступ (ZPA) предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9aee7-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9aee7-106">Можно управлять в Azure AD, имеющего доступ tooZscaler закрытый доступ (ZPA)</span><span class="sxs-lookup"><span data-stu-id="9aee7-106">You can control in Azure AD who has access tooZscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="9aee7-107">Ваш пользователей tooautomatically get вошедшего tooZscaler закрытый доступ (ZPA) (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="9aee7-107">You can enable your users tooautomatically get signed-on tooZscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9aee7-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="9aee7-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9aee7-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9aee7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9aee7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9aee7-110">Prerequisites</span></span>

<span data-ttu-id="9aee7-111">tooconfigure интеграция Azure AD с Zscaler закрытый доступ (ZPA) требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9aee7-111">tooconfigure Azure AD integration with Zscaler Private Access (ZPA), you need hello following items:</span></span>

- <span data-ttu-id="9aee7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9aee7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9aee7-113">подписка Zscaler Private Access (ZPA) с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9aee7-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="9aee7-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9aee7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="9aee7-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="9aee7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9aee7-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="9aee7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9aee7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9aee7-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="9aee7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9aee7-118">Scenario description</span></span>
<span data-ttu-id="9aee7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9aee7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9aee7-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="9aee7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9aee7-121">Добавление Zscaler закрытый доступ (ZPA) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="9aee7-121">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
2. <span data-ttu-id="9aee7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9aee7-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a><span data-ttu-id="9aee7-123">Добавление Zscaler закрытый доступ (ZPA) из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="9aee7-123">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
<span data-ttu-id="9aee7-124">tooconfigure hello интеграция из Zscaler закрытый доступ (ZPA) в Azure AD, вы должны tooadd Zscaler закрытый доступ (ZPA) из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9aee7-124">tooconfigure hello integration of Zscaler Private Access (ZPA) into Azure AD, you need tooadd Zscaler Private Access (ZPA) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9aee7-125">**tooadd Zscaler закрытый доступ (ZPA) из коллекции hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9aee7-125">**tooadd Zscaler Private Access (ZPA) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9aee7-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9aee7-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9aee7-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9aee7-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9aee7-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="9aee7-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9aee7-133">Введите в поле поиска hello **Zscaler закрытый доступ (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-133">In hello search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="9aee7-135">В панели результатов hello выберите **Zscaler закрытый доступ (ZPA)**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9aee7-135">In hello results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9aee7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9aee7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9aee7-138">В этом разделе описана настройка и проверка единого входа Azure AD в Zscaler Private Access (ZPA) с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9aee7-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9aee7-139">Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello в Zscaler закрытый доступ (ZPA) является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9aee7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Private Access (ZPA) is tooa user in Azure AD.</span></span> <span data-ttu-id="9aee7-140">Иными словами связи между пользователя Azure AD и связанных пользователей hello в Zscaler закрытый доступ (ZPA) необходимо установить toobe.</span><span class="sxs-lookup"><span data-stu-id="9aee7-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Private Access (ZPA) needs toobe established.</span></span>

<span data-ttu-id="9aee7-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Zscaler закрытый доступ (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9aee7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="9aee7-142">tooconfigure и тестирования Azure AD единого входа с Zscaler закрытый доступ (ZPA), необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9aee7-142">tooconfigure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9aee7-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="9aee7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9aee7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9aee7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9aee7-145">**[Создание тестового пользователя Zscaler закрытый доступ (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave аналог Саймон Britta в Zscaler закрытый доступ (ZPA), являющийся представлением ей связанного toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9aee7-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - toohave a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9aee7-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="9aee7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9aee7-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9aee7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9aee7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9aee7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9aee7-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложение Zscaler закрытый доступ (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9aee7-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="9aee7-150">**tooconfigure Azure AD единого входа с Zscaler закрытый доступ (ZPA), выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9aee7-150">**tooconfigure Azure AD single sign-on with Zscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="9aee7-151">На портале управления Azure hello на hello **Zscaler закрытый доступ (ZPA)** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-151">In hello Azure Management portal, on hello **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9aee7-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="9aee7-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="9aee7-155">На hello **Zscaler закрытый доступ (ZPA) доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9aee7-155">On hello **Zscaler Private Access (ZPA) Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="9aee7-157">а.</span><span class="sxs-lookup"><span data-stu-id="9aee7-157">a.</span></span> <span data-ttu-id="9aee7-158">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="9aee7-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="9aee7-159">b.</span><span class="sxs-lookup"><span data-stu-id="9aee7-159">b.</span></span> <span data-ttu-id="9aee7-160">В hello **идентификатор** введите:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="9aee7-160">In hello **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9aee7-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="9aee7-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="9aee7-162">У вас есть tooupdate входа эти значения с hello фактический URL-адрес и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9aee7-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="9aee7-163">Здесь мы предлагаем вам toouse hello уникальное значение URL-адреса в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9aee7-163">Here we suggest you toouse hello unique value of URL in hello Identifier.</span></span> <span data-ttu-id="9aee7-164">Обратитесь к [группы поддержки Zscaler закрытый доступ (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="9aee7-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooget these values.</span></span>

4. <span data-ttu-id="9aee7-165">На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-165">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="9aee7-167">На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-167">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="9aee7-168">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-168">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="9aee7-170">На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9aee7-170">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="9aee7-172">На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-172">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="9aee7-174">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="9aee7-174">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="9aee7-176">В другом окне веб-браузера войдите на свой корпоративный сайт Zscaler Private Access (ZPA) в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="9aee7-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="9aee7-177">Перейдите в слишком**администратора** и нажмите кнопку **конфигурации поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-177">Navigate too**Administrator** and then click **Idp Configuration**.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="9aee7-179">В hello **конфигурации поставщика удостоверений** щелкните **Добавление новой конфигурации поставщика Удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-179">In hello **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="9aee7-181">В hello **новая конфигурация поставщика Удостоверений** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9aee7-181">In hello **New IDP Configuration** section, perform hello following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="9aee7-183">а.</span><span class="sxs-lookup"><span data-stu-id="9aee7-183">a.</span></span> <span data-ttu-id="9aee7-184">Чтобы отправить скачанный файл метаданных, щелкните **Select File** (Выбрать файл).</span><span class="sxs-lookup"><span data-stu-id="9aee7-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="9aee7-185">b.</span><span class="sxs-lookup"><span data-stu-id="9aee7-185">b.</span></span> <span data-ttu-id="9aee7-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9aee7-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9aee7-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9aee7-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9aee7-188">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="9aee7-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9aee7-190">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9aee7-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9aee7-191">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="9aee7-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9aee7-193">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="9aee7-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9aee7-195">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9aee7-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9aee7-197">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9aee7-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9aee7-199">а.</span><span class="sxs-lookup"><span data-stu-id="9aee7-199">a.</span></span> <span data-ttu-id="9aee7-200">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9aee7-201">b.</span><span class="sxs-lookup"><span data-stu-id="9aee7-201">b.</span></span> <span data-ttu-id="9aee7-202">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9aee7-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9aee7-203">c.</span><span class="sxs-lookup"><span data-stu-id="9aee7-203">c.</span></span> <span data-ttu-id="9aee7-204">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9aee7-205">d.</span><span class="sxs-lookup"><span data-stu-id="9aee7-205">d.</span></span> <span data-ttu-id="9aee7-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="9aee7-207">Создание тестового пользователя Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="9aee7-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="9aee7-208">В этом разделе описано, как создать пользователя Britta Simon в приложении Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9aee7-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="9aee7-209">Можно работать с [группы поддержки Zscaler закрытый доступ (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooadd hello пользователей на платформе hello Zscaler закрытый доступ (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9aee7-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooadd hello users in hello Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9aee7-210">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="9aee7-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9aee7-211">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooZscaler закрытый доступ (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9aee7-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooZscaler Private Access (ZPA).</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9aee7-213">**tooassign tooZscaler Britta Simon закрытый доступ (ZPA), выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9aee7-213">**tooassign Britta Simon tooZscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="9aee7-214">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-214">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9aee7-216">В списке приложений hello выберите **Zscaler закрытый доступ (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-216">In hello applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="9aee7-218">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9aee7-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-220">Click **Add** button.</span></span> <span data-ttu-id="9aee7-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9aee7-223">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="9aee7-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9aee7-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9aee7-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9aee7-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="9aee7-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9aee7-226">Testing single sign-on</span></span>

<span data-ttu-id="9aee7-227">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="9aee7-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9aee7-228">При нажатии кнопки hello Zscaler закрытый доступ (ZPA) плитки в панели доступа hello, вы должны получить приложения автоматически вошедшего tooyour Zscaler закрытый доступ (ZPA).</span><span class="sxs-lookup"><span data-stu-id="9aee7-228">When you click hello Zscaler Private Access (ZPA) tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9aee7-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9aee7-229">Additional resources</span></span>

* [<span data-ttu-id="9aee7-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9aee7-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9aee7-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9aee7-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png