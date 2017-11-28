---
title: "Руководство по интеграции Azure Active Directory с BetterWorks | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BetterWorks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="f34c5-103">Учебник. Интеграция Azure Active Directory с BetterWorks</span><span class="sxs-lookup"><span data-stu-id="f34c5-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="f34c5-104">В этом учебнике вы узнаете, как toointegrate BetterWorks с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f34c5-104">In this tutorial, you learn how toointegrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f34c5-105">Интеграция с Azure AD BetterWorks предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f34c5-105">Integrating BetterWorks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f34c5-106">Можно управлять в Azure AD, имеющего доступ tooBetterWorks</span><span class="sxs-lookup"><span data-stu-id="f34c5-106">You can control in Azure AD who has access tooBetterWorks</span></span>
- <span data-ttu-id="f34c5-107">Можно включить на пользователей tooautomatically get вошедшего tooBetterWorks (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f34c5-107">You can enable your users tooautomatically get signed-on tooBetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f34c5-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f34c5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f34c5-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f34c5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f34c5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f34c5-110">Prerequisites</span></span>

<span data-ttu-id="f34c5-111">tooconfigure интеграция Azure AD с BetterWorks требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f34c5-111">tooconfigure Azure AD integration with BetterWorks, you need hello following items:</span></span>

- <span data-ttu-id="f34c5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f34c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f34c5-113">подписка BetterWorks с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f34c5-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f34c5-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f34c5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f34c5-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f34c5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f34c5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f34c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f34c5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f34c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f34c5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f34c5-118">Scenario description</span></span>
<span data-ttu-id="f34c5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f34c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f34c5-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f34c5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f34c5-121">Добавление BetterWorks из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f34c5-121">Adding BetterWorks from hello gallery</span></span>
2. <span data-ttu-id="f34c5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f34c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-hello-gallery"></a><span data-ttu-id="f34c5-123">Добавление BetterWorks из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f34c5-123">Adding BetterWorks from hello gallery</span></span>
<span data-ttu-id="f34c5-124">tooconfigure hello интеграции BetterWorks в Azure AD, вы должны tooadd BetterWorks из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f34c5-124">tooconfigure hello integration of BetterWorks into Azure AD, you need tooadd BetterWorks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f34c5-125">**tooadd BetterWorks из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f34c5-125">**tooadd BetterWorks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f34c5-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f34c5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f34c5-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f34c5-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f34c5-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f34c5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f34c5-133">Введите в поле поиска hello **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-133">In hello search box, type **BetterWorks**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="f34c5-135">В панели результатов hello выберите **BetterWorks**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f34c5-135">In hello results panel, select **BetterWorks**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f34c5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f34c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f34c5-138">В этом разделе описана настройка и проверка единого входа Azure AD в BetterWorks с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f34c5-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f34c5-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BetterWorks является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f34c5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BetterWorks is tooa user in Azure AD.</span></span> <span data-ttu-id="f34c5-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в BetterWorks должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f34c5-140">In other words, a link relationship between an Azure AD user and hello related user in BetterWorks needs toobe established.</span></span>

<span data-ttu-id="f34c5-141">В BetterWorks, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f34c5-141">In BetterWorks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f34c5-142">tooconfigure и теста Azure AD единого входа с BetterWorks, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f34c5-142">tooconfigure and test Azure AD single sign-on with BetterWorks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f34c5-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f34c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f34c5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f34c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f34c5-145">**[Создание тестового пользователя BetterWorks](#creating-a-betterworks-test-user)**  -toohave аналог Саймон Britta в BetterWorks, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f34c5-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - toohave a counterpart of Britta Simon in BetterWorks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f34c5-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f34c5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f34c5-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f34c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f34c5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f34c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f34c5-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="f34c5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="f34c5-150">**tooconfigure Azure AD единого входа с BetterWorks, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f34c5-150">**tooconfigure Azure AD single sign-on with BetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="f34c5-151">В hello в hello портала Azure **BetterWorks** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-151">In hello Azure portal, on hello **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f34c5-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f34c5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="f34c5-155">На hello **URL-адреса и домена BetterWorks** статьи, при желании tooconfigure приложения hello в **режиме, инициированный IDP**:</span><span class="sxs-lookup"><span data-stu-id="f34c5-155">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="f34c5-157">а.</span><span class="sxs-lookup"><span data-stu-id="f34c5-157">a.</span></span> <span data-ttu-id="f34c5-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="f34c5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="f34c5-159">b.</span><span class="sxs-lookup"><span data-stu-id="f34c5-159">b.</span></span> <span data-ttu-id="f34c5-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="f34c5-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="f34c5-161">На hello **URL-адреса и домена BetterWorks** статьи, при желании tooconfigure приложения hello в **режиме, инициируемая SP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f34c5-161">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="f34c5-163">а.</span><span class="sxs-lookup"><span data-stu-id="f34c5-163">a.</span></span> <span data-ttu-id="f34c5-164">Щелкните hello **Показывать дополнительные параметры URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-164">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="f34c5-165">b.</span><span class="sxs-lookup"><span data-stu-id="f34c5-165">b.</span></span> <span data-ttu-id="f34c5-166">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="f34c5-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f34c5-167">Значения, указанные выше, приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f34c5-167">These are not real values.</span></span> <span data-ttu-id="f34c5-168">Обновите эти значения с hello URL-адрес ответа, идентификатор и фактический на URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="f34c5-168">Update these values with hello Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="f34c5-169">Обратитесь к [BetterWorks поддержки](mailto:support@betterworks.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f34c5-169">Contact [BetterWorks support team](mailto:support@betterworks.com) tooget these values.</span></span>
 
4. <span data-ttu-id="f34c5-170">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f34c5-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="f34c5-172">BetterWorks приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="f34c5-172">BetterWorks application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f34c5-173">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f34c5-173">Configure hello following claims for this application.</span></span> <span data-ttu-id="f34c5-174">Вы можете управлять hello значения этих атрибутов из hello»**атрибута**» вкладку приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f34c5-174">You can manage hello values of these attributes from hello "**Attribute**" tab of hello application.</span></span> <span data-ttu-id="f34c5-175">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="f34c5-175">hello following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="f34c5-177">На hello **атрибутов токена SAML** диалоговое окно, для каждой строки, показано в следующей таблице hello выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f34c5-177">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
   | <span data-ttu-id="f34c5-178">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="f34c5-178">Attribute Name</span></span> | <span data-ttu-id="f34c5-179">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="f34c5-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="f34c5-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="f34c5-180">saml_token</span></span>     | <span data-ttu-id="f34c5-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="f34c5-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="f34c5-182">а.</span><span class="sxs-lookup"><span data-stu-id="f34c5-182">a.</span></span> <span data-ttu-id="f34c5-183">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f34c5-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="f34c5-186">b.</span><span class="sxs-lookup"><span data-stu-id="f34c5-186">b.</span></span> <span data-ttu-id="f34c5-187">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f34c5-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

   <span data-ttu-id="f34c5-188">c.</span><span class="sxs-lookup"><span data-stu-id="f34c5-188">c.</span></span> <span data-ttu-id="f34c5-189">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f34c5-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
   <span data-ttu-id="f34c5-190">d.</span><span class="sxs-lookup"><span data-stu-id="f34c5-190">d.</span></span> <span data-ttu-id="f34c5-191">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-191">Click **Ok**.</span></span>

7. <span data-ttu-id="f34c5-192">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f34c5-192">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f34c5-194">tooconfigure единого входа на **BetterWorks** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[BetterWorks поддержки](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="f34c5-194">tooconfigure single sign-on on **BetterWorks** side, you need toosend hello downloaded **Metadata XML** too[BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="f34c5-195">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f34c5-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f34c5-196">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f34c5-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f34c5-197">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f34c5-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f34c5-198">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f34c5-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="f34c5-199">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f34c5-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f34c5-201">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f34c5-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f34c5-202">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f34c5-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f34c5-204">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f34c5-206">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f34c5-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f34c5-208">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f34c5-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f34c5-210">а.</span><span class="sxs-lookup"><span data-stu-id="f34c5-210">a.</span></span> <span data-ttu-id="f34c5-211">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f34c5-212">b.</span><span class="sxs-lookup"><span data-stu-id="f34c5-212">b.</span></span> <span data-ttu-id="f34c5-213">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f34c5-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f34c5-214">c.</span><span class="sxs-lookup"><span data-stu-id="f34c5-214">c.</span></span> <span data-ttu-id="f34c5-215">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f34c5-216">d.</span><span class="sxs-lookup"><span data-stu-id="f34c5-216">d.</span></span> <span data-ttu-id="f34c5-217">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="f34c5-218">Создание тестового пользователя BetterWorks</span><span class="sxs-lookup"><span data-stu-id="f34c5-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="f34c5-219">В этом разделе описано, как создать пользователя Britta Simon в приложении BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="f34c5-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="f34c5-220">Работать с [BetterWorks поддержки](mailto:support@betterworks.com) tooadd hello пользователей на платформе BetterWorks hello.</span><span class="sxs-lookup"><span data-stu-id="f34c5-220">Work with [BetterWorks support team](mailto:support@betterworks.com) tooadd hello users in hello BetterWorks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f34c5-221">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f34c5-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f34c5-222">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBetterWorks доступа.</span><span class="sxs-lookup"><span data-stu-id="f34c5-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBetterWorks.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f34c5-224">**tooassign tooBetterWorks Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f34c5-224">**tooassign Britta Simon tooBetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="f34c5-225">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f34c5-227">В списке приложений hello выберите **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-227">In hello applications list, select **BetterWorks**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="f34c5-229">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f34c5-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-231">Click **Add** button.</span></span> <span data-ttu-id="f34c5-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f34c5-234">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f34c5-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f34c5-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f34c5-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f34c5-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f34c5-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f34c5-237">Testing single sign-on</span></span>

<span data-ttu-id="f34c5-238">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="f34c5-238">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f34c5-239">При нажатии кнопки BetterWorks плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour BetterWorks приложения.</span><span class="sxs-lookup"><span data-stu-id="f34c5-239">When you click hello BetterWorks tile in hello Access Panel, you should get automatically signed-on tooyour BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f34c5-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f34c5-240">Additional resources</span></span>

* [<span data-ttu-id="f34c5-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f34c5-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f34c5-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f34c5-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

