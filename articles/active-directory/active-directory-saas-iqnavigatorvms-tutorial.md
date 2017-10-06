---
title: "Руководство по интеграции Azure Active Directory c IQNavigator VMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и IQNavigator виртуальных МАШИН."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="891fb-103">Руководство по интеграции Azure Active Directory c IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="891fb-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="891fb-104">В этом учебнике вы узнаете, как toointegrate IQNavigator виртуальные МАШИНЫ в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="891fb-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="891fb-105">Интеграция IQNavigator ВМ с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="891fb-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="891fb-106">Можно управлять в Azure AD, имеющего доступ tooIQNavigator виртуальные МАШИНЫ</span><span class="sxs-lookup"><span data-stu-id="891fb-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="891fb-107">Можно включить на пользователей tooautomatically get вошедшего tooIQNavigator виртуальных МАШИН (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="891fb-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="891fb-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="891fb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="891fb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="891fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="891fb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="891fb-110">Prerequisites</span></span>

<span data-ttu-id="891fb-111">tooconfigure интеграция Azure AD с виртуальными Машинами IQNavigator требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="891fb-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="891fb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="891fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="891fb-113">подписка IQNavigator VMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="891fb-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="891fb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="891fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="891fb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="891fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="891fb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="891fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="891fb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="891fb-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="891fb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="891fb-118">Scenario description</span></span>
<span data-ttu-id="891fb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="891fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="891fb-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="891fb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="891fb-121">Добавление виртуальных МАШИН IQNavigator из галереи hello</span><span class="sxs-lookup"><span data-stu-id="891fb-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="891fb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="891fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="891fb-123">Добавление виртуальных МАШИН IQNavigator из галереи hello</span><span class="sxs-lookup"><span data-stu-id="891fb-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="891fb-124">tooconfigure hello интеграция IQNavigator виртуальных машин в Azure AD, вы должны tooadd IQNavigator виртуальных МАШИН из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="891fb-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="891fb-125">**tooadd IQNavigator ВМ из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="891fb-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="891fb-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="891fb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="891fb-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="891fb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="891fb-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="891fb-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="891fb-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="891fb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="891fb-133">Введите в поле поиска hello **IQNavigator ВМ**.</span><span class="sxs-lookup"><span data-stu-id="891fb-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="891fb-135">В панели результатов hello, выберите **виртуальные МАШИНЫ IQNavigator**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="891fb-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="891fb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="891fb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="891fb-138">В этом разделе описана настройка и проверка единого входа Azure AD в IQNavigator VMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="891fb-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="891fb-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в виртуальных Машинах IQNavigator является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="891fb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="891fb-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей на виртуальных Машинах IQNavigator должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="891fb-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="891fb-141">На виртуальных Машинах IQNavigator, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="891fb-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="891fb-142">tooconfigure и тестирования Azure AD единого входа с виртуальными Машинами IQNavigator, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="891fb-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="891fb-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="891fb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="891fb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="891fb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="891fb-145">**[Создание тестового пользователя ВМ IQNavigator](#creating-a-iqnavigator-vms-test-user)**  -toohave аналог Саймон Britta в виртуальных Машинах IQNavigator, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="891fb-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="891fb-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="891fb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="891fb-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="891fb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="891fb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="891fb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="891fb-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении IQNavigator виртуальных МАШИН.</span><span class="sxs-lookup"><span data-stu-id="891fb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="891fb-150">**tooconfigure Azure AD единый вход с виртуальной Машиной IQNavigator, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="891fb-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="891fb-151">В hello в hello портала Azure **виртуальные МАШИНЫ IQNavigator** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="891fb-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="891fb-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="891fb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="891fb-155">На hello **URL-адреса и виртуальными Машинами домена IQNavigator** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="891fb-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="891fb-157">а.</span><span class="sxs-lookup"><span data-stu-id="891fb-157">a.</span></span> <span data-ttu-id="891fb-158">В hello **идентификатор** текстовом поле введите URL-адрес hello:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="891fb-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="891fb-159">b.</span><span class="sxs-lookup"><span data-stu-id="891fb-159">b.</span></span> <span data-ttu-id="891fb-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="891fb-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="891fb-161">Проверьте **Показывать дополнительные параметры URL-адреса**, выполните следующий шаг hello:</span><span class="sxs-lookup"><span data-stu-id="891fb-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="891fb-163">В hello **ретрансляции состояние** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="891fb-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="891fb-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="891fb-164">These values are not real.</span></span> <span data-ttu-id="891fb-165">Обновите эти значения с фактическим URL-адрес ответа и ретрансляции состоянием hello.</span><span class="sxs-lookup"><span data-stu-id="891fb-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="891fb-166">Обратитесь к [IQNavigator виртуальные МАШИНЫ клиента поддержки](https://www.beeline.com/iqn-product-support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="891fb-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="891fb-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="891fb-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="891fb-169">toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="891fb-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="891fb-170">а.</span><span class="sxs-lookup"><span data-stu-id="891fb-170">a.</span></span> <span data-ttu-id="891fb-171">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="891fb-171">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="891fb-173">b.</span><span class="sxs-lookup"><span data-stu-id="891fb-173">b.</span></span> <span data-ttu-id="891fb-174">Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="891fb-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="891fb-176">c.</span><span class="sxs-lookup"><span data-stu-id="891fb-176">c.</span></span> <span data-ttu-id="891fb-177">Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="891fb-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="891fb-179">d.</span><span class="sxs-lookup"><span data-stu-id="891fb-179">d.</span></span> <span data-ttu-id="891fb-180">Теперь перейдите на странице свойств toohello **IQNavigator ВМ** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="891fb-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="891fb-182">д.</span><span class="sxs-lookup"><span data-stu-id="891fb-182">e.</span></span> <span data-ttu-id="891fb-183">Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="891fb-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="891fb-184">Значение идентификатора уникального пользователя hello ожидать приложению IQNavigator в утверждение идентификатора имени hello.</span><span class="sxs-lookup"><span data-stu-id="891fb-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="891fb-185">Клиента можно сопоставить hello правильное значение для утверждения идентификатора имени hello.</span><span class="sxs-lookup"><span data-stu-id="891fb-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="891fb-186">В этом случае мы сопоставленной hello пользователя. UserPrincipalName в целях демонстрации hello.</span><span class="sxs-lookup"><span data-stu-id="891fb-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="891fb-187">Однако в соответствии с tooyour параметры организации следует сопоставить hello правильное значение для него.</span><span class="sxs-lookup"><span data-stu-id="891fb-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="891fb-189">На hello **конфигурации виртуальных МАШИН IQNavigator** щелкните **настроить виртуальные МАШИНЫ IQNavigator** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="891fb-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="891fb-190">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="891fb-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="891fb-192">tooconfigure единого входа на **виртуальные МАШИНЫ IQNavigator** параллельно, необходимо toosend hello **URL-адрес метаданных**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком [Группа поддержки виртуальных МАШИН IQNavigator](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="891fb-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="891fb-193">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="891fb-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="891fb-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="891fb-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="891fb-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="891fb-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="891fb-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="891fb-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="891fb-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="891fb-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="891fb-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="891fb-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="891fb-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="891fb-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="891fb-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="891fb-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="891fb-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="891fb-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="891fb-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="891fb-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="891fb-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="891fb-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="891fb-209">а.</span><span class="sxs-lookup"><span data-stu-id="891fb-209">a.</span></span> <span data-ttu-id="891fb-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="891fb-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="891fb-211">b.</span><span class="sxs-lookup"><span data-stu-id="891fb-211">b.</span></span> <span data-ttu-id="891fb-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="891fb-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="891fb-213">c.</span><span class="sxs-lookup"><span data-stu-id="891fb-213">c.</span></span> <span data-ttu-id="891fb-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="891fb-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="891fb-215">d.</span><span class="sxs-lookup"><span data-stu-id="891fb-215">d.</span></span> <span data-ttu-id="891fb-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="891fb-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="891fb-217">Создание тестового пользователя IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="891fb-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="891fb-218">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в виртуальных Машинах IQNavigator.</span><span class="sxs-lookup"><span data-stu-id="891fb-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="891fb-219">Работать с [группа поддержки виртуальных МАШИН IQNavigator](https://www.beeline.com/iqn-product-support/) tooadd пользователей hello в hello виртуальные МАШИНЫ IQNavigator учетной записи.</span><span class="sxs-lookup"><span data-stu-id="891fb-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="891fb-220">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="891fb-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="891fb-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooIQNavigator виртуальных МАШИН.</span><span class="sxs-lookup"><span data-stu-id="891fb-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="891fb-223">**tooassign tooIQNavigator Britta Simon виртуальных МАШИН, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="891fb-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="891fb-224">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="891fb-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="891fb-226">В списке приложений hello выберите **IQNavigator ВМ**.</span><span class="sxs-lookup"><span data-stu-id="891fb-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="891fb-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="891fb-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="891fb-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="891fb-230">Click **Add** button.</span></span> <span data-ttu-id="891fb-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="891fb-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="891fb-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="891fb-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="891fb-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="891fb-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="891fb-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="891fb-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="891fb-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="891fb-236">Testing single sign-on</span></span>

<span data-ttu-id="891fb-237">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="891fb-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="891fb-238">При нажатии кнопки hello виртуальные МАШИНЫ IQNavigator плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на виртуальные МАШИНЫ IQNavigator приложения.</span><span class="sxs-lookup"><span data-stu-id="891fb-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="891fb-239">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="891fb-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="891fb-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="891fb-240">Additional resources</span></span>

* [<span data-ttu-id="891fb-241">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="891fb-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="891fb-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="891fb-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

