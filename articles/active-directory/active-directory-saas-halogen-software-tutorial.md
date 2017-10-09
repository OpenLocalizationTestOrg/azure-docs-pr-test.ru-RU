---
title: "Руководство по интеграции Azure Active Directory с Halogen Software | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и имеющий программного обеспечения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="0ef80-103">Учебник. Интеграция Azure Active Directory с Halogen Software</span><span class="sxs-lookup"><span data-stu-id="0ef80-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="0ef80-104">В этом учебнике вы узнаете, как toointegrate имеющий программного обеспечения в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ef80-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ef80-105">Интеграция имеющий программного обеспечения в Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0ef80-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0ef80-106">Можно управлять в Azure AD, имеющего доступ tooHalogen программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="0ef80-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="0ef80-107">Можно включить на пользователей tooautomatically get вошедшего tooHalogen программного обеспечения (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ef80-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ef80-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0ef80-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0ef80-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ef80-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ef80-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ef80-110">Prerequisites</span></span>

<span data-ttu-id="0ef80-111">tooconfigure интеграция Azure AD с программным обеспечением имеющий требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0ef80-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="0ef80-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0ef80-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ef80-113">подписка Halogen Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0ef80-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ef80-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0ef80-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ef80-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0ef80-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ef80-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0ef80-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ef80-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ef80-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ef80-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0ef80-118">Scenario description</span></span>

<span data-ttu-id="0ef80-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0ef80-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ef80-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0ef80-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ef80-121">Добавление программного обеспечения имеющий из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0ef80-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="0ef80-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ef80-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="0ef80-123">Добавление программного обеспечения имеющий из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0ef80-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="0ef80-124">tooconfigure hello интеграции имеющий программного обеспечения в Azure AD, вы должны tooadd имеющий программного обеспечения из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0ef80-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0ef80-125">**tooadd имеющий программного обеспечения из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0ef80-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ef80-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0ef80-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0ef80-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0ef80-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0ef80-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0ef80-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0ef80-133">Введите в поле поиска hello **программного обеспечения имеющий**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-133">In hello search box, type **Halogen Software**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="0ef80-135">В панели результатов hello, выберите **программного обеспечения имеющий**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0ef80-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0ef80-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ef80-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0ef80-138">В этом разделе описана настройка и проверка единого входа Azure AD в Halogen Software для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ef80-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ef80-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в программном обеспечении имеющий является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ef80-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="0ef80-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в программном обеспечении имеющий должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0ef80-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="0ef80-141">В программном обеспечении имеющий, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="0ef80-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0ef80-142">tooconfigure и теста Azure AD единого входа с имеющий программного обеспечения, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0ef80-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0ef80-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0ef80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0ef80-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0ef80-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ef80-145">**[Создание тестового пользователя программного обеспечения имеющий](#creating-a-halogen-software-test-user)**  -toohave аналог Саймон Britta имеющий программного обеспечения, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="0ef80-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0ef80-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0ef80-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ef80-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0ef80-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0ef80-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ef80-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0ef80-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении имеющий программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="0ef80-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="0ef80-150">**tooconfigure Azure AD единого входа с программным обеспечением имеющий выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0ef80-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ef80-151">В hello в hello портала Azure **программного обеспечения имеющий** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0ef80-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0ef80-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="0ef80-155">На hello **URL-адреса и имеющий программного обеспечения домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0ef80-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="0ef80-157">а.</span><span class="sxs-lookup"><span data-stu-id="0ef80-157">a.</span></span> <span data-ttu-id="0ef80-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="0ef80-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="0ef80-159">b.</span><span class="sxs-lookup"><span data-stu-id="0ef80-159">b.</span></span> <span data-ttu-id="0ef80-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="0ef80-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ef80-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0ef80-161">These values are not real.</span></span> <span data-ttu-id="0ef80-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="0ef80-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0ef80-163">Обратитесь к [имеющий клиентское программное обеспечение поддержки](https://support.halogensoftware.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="0ef80-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="0ef80-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0ef80-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="0ef80-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0ef80-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ef80-168">В другом окне браузера, tooyour входа **программного обеспечения имеющий** приложение от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="0ef80-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="0ef80-169">Нажмите кнопку hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0ef80-169">Click hello **Options** tab.</span></span> 
   
    ![Что такое Azure AD Connect?][12]

8. <span data-ttu-id="0ef80-171">Hello панели навигации слева щелкните **конфигурация SAML**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Что такое Azure AD Connect?][13]

9. <span data-ttu-id="0ef80-173">На hello **конфигурация SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0ef80-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![Что такое Azure AD Connect?][14]

     <span data-ttu-id="0ef80-175">а.</span><span class="sxs-lookup"><span data-stu-id="0ef80-175">a.</span></span> <span data-ttu-id="0ef80-176">В качестве значения поля **Уникальный идентификатор** выберите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="0ef80-177">b.</span><span class="sxs-lookup"><span data-stu-id="0ef80-177">b.</span></span> <span data-ttu-id="0ef80-178">В качестве значения поля **Unique Identifier Maps To** (Уникальный идентификатор сопоставляется с) выберите **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="0ef80-179">c.</span><span class="sxs-lookup"><span data-stu-id="0ef80-179">c.</span></span> <span data-ttu-id="0ef80-180">tooupload скачанный файл метаданных, щелкните **Обзор** tooselect hello файла, а затем **передать файл**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="0ef80-181">d.</span><span class="sxs-lookup"><span data-stu-id="0ef80-181">d.</span></span> <span data-ttu-id="0ef80-182">Конфигурация tootest hello, нажмите кнопку **запустить тест**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="0ef80-183">Требуется toowait приветственное сообщение «*hello SAML проверка завершена. Закройте это окно*".</span><span class="sxs-lookup"><span data-stu-id="0ef80-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="0ef80-184">Закройте окно браузера открытый hello.</span><span class="sxs-lookup"><span data-stu-id="0ef80-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="0ef80-185">Hello **включить SAML** флажок доступна только в том случае, если проверка hello завершена.</span><span class="sxs-lookup"><span data-stu-id="0ef80-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="0ef80-186">д.</span><span class="sxs-lookup"><span data-stu-id="0ef80-186">e.</span></span> <span data-ttu-id="0ef80-187">Выберите **Включить SAML**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="0ef80-188">Е.</span><span class="sxs-lookup"><span data-stu-id="0ef80-188">f.</span></span> <span data-ttu-id="0ef80-189">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="0ef80-190">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="0ef80-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0ef80-191">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0ef80-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0ef80-192">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0ef80-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0ef80-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ef80-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="0ef80-194">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef80-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0ef80-196">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0ef80-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ef80-197">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0ef80-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ef80-199">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ef80-201">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="0ef80-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ef80-203">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0ef80-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ef80-205">а.</span><span class="sxs-lookup"><span data-stu-id="0ef80-205">a.</span></span> <span data-ttu-id="0ef80-206">В hello **имя** в текстовое поле имя типа как **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="0ef80-207">b.</span><span class="sxs-lookup"><span data-stu-id="0ef80-207">b.</span></span> <span data-ttu-id="0ef80-208">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0ef80-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0ef80-209">c.</span><span class="sxs-lookup"><span data-stu-id="0ef80-209">c.</span></span> <span data-ttu-id="0ef80-210">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0ef80-211">d.</span><span class="sxs-lookup"><span data-stu-id="0ef80-211">d.</span></span> <span data-ttu-id="0ef80-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="0ef80-213">Создание тестового пользователя Halogen Software</span><span class="sxs-lookup"><span data-stu-id="0ef80-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="0ef80-214">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon имеющий программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="0ef80-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="0ef80-215">**toocreate пользователя с именем Britta Simon имеющий программного обеспечения, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0ef80-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ef80-216">Войдите на tooyour **программного обеспечения имеющий** приложение от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="0ef80-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="0ef80-217">Нажмите кнопку hello **центра пользователей** , а затем щелкните **Create User**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![Что такое Azure AD Connect?][300]  

3. <span data-ttu-id="0ef80-219">На hello **нового пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0ef80-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![Что такое Azure AD Connect?][301]

    <span data-ttu-id="0ef80-221">а.</span><span class="sxs-lookup"><span data-stu-id="0ef80-221">a.</span></span> <span data-ttu-id="0ef80-222">В hello **имя** в текстовое поле имя первого типа hello пользователя как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="0ef80-223">b.</span><span class="sxs-lookup"><span data-stu-id="0ef80-223">b.</span></span> <span data-ttu-id="0ef80-224">В hello **Фамилия** текстовое поле, тип фамилию пользователя hello как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="0ef80-225">c.</span><span class="sxs-lookup"><span data-stu-id="0ef80-225">c.</span></span> <span data-ttu-id="0ef80-226">В hello **Username** введите **Britta Simon**, hello имя пользователя как hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef80-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="0ef80-227">d.</span><span class="sxs-lookup"><span data-stu-id="0ef80-227">d.</span></span> <span data-ttu-id="0ef80-228">В hello **пароль** введите пароль для Britta.</span><span class="sxs-lookup"><span data-stu-id="0ef80-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="0ef80-229">д.</span><span class="sxs-lookup"><span data-stu-id="0ef80-229">e.</span></span> <span data-ttu-id="0ef80-230">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0ef80-231">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0ef80-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0ef80-232">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooHalogen программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="0ef80-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0ef80-234">**tooassign tooHalogen Britta Simon программное обеспечение, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="0ef80-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ef80-235">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0ef80-237">В списке приложений hello выберите **программного обеспечения имеющий**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="0ef80-239">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0ef80-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-241">Click **Add** button.</span></span> <span data-ttu-id="0ef80-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0ef80-244">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0ef80-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0ef80-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ef80-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0ef80-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0ef80-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0ef80-247">Testing single sign-on</span></span>

<span data-ttu-id="0ef80-248">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="0ef80-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0ef80-249">Если щелкнуть плитку программного обеспечения имеющий hello в hello панели доступа, следует получать автоматически вошедшего tooyour имеющий программного приложения.</span><span class="sxs-lookup"><span data-stu-id="0ef80-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ef80-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0ef80-250">Additional resources</span></span>

* [<span data-ttu-id="0ef80-251">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ef80-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ef80-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ef80-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
