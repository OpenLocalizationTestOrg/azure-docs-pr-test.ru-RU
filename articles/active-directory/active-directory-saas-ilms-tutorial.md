---
title: "Руководство. Интеграция Azure Active Directory с iLMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="96c1a-103">Руководство. Интеграция Azure Active Directory с iLMS</span><span class="sxs-lookup"><span data-stu-id="96c1a-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="96c1a-104">В этом учебнике вы узнаете, как iLMS toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96c1a-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96c1a-105">Интеграция с Azure AD iLMS предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="96c1a-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96c1a-106">Можно управлять в Azure AD, имеющего доступ tooiLMS</span><span class="sxs-lookup"><span data-stu-id="96c1a-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="96c1a-107">Можно включить на пользователей tooautomatically get вошедшего tooiLMS (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="96c1a-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96c1a-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="96c1a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="96c1a-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96c1a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96c1a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="96c1a-110">Prerequisites</span></span>

<span data-ttu-id="96c1a-111">tooconfigure интеграция Azure AD с iLMS требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="96c1a-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="96c1a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="96c1a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96c1a-113">подписка iLMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="96c1a-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96c1a-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="96c1a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96c1a-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="96c1a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96c1a-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="96c1a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="96c1a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96c1a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96c1a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="96c1a-118">Scenario description</span></span>
<span data-ttu-id="96c1a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="96c1a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96c1a-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="96c1a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96c1a-121">Добавление iLMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="96c1a-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="96c1a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="96c1a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="96c1a-123">Добавление iLMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="96c1a-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="96c1a-124">tooconfigure hello интеграции iLMS в Azure AD, вы должны iLMS tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="96c1a-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96c1a-125">**iLMS tooadd из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96c1a-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96c1a-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="96c1a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96c1a-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96c1a-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="96c1a-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="96c1a-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="96c1a-133">Введите в поле поиска hello **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-133">In hello search box, type **iLMS**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="96c1a-135">В панели результатов hello выберите **iLMS**, нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96c1a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="96c1a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96c1a-138">В этом разделе описана настройка и проверка единого входа Azure AD в iLMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96c1a-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96c1a-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в iLMS является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96c1a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="96c1a-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в iLMS должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="96c1a-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="96c1a-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в iLMS.</span><span class="sxs-lookup"><span data-stu-id="96c1a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="96c1a-142">tooconfigure и теста Azure AD единого входа с iLMS, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="96c1a-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96c1a-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="96c1a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96c1a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="96c1a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96c1a-145">**[Создание тестового пользователя, прошедшего iLMS](#creating-an-ilms-test-user)**  -toohave аналог Саймон Britta в iLMS, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="96c1a-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="96c1a-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="96c1a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96c1a-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="96c1a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96c1a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="96c1a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96c1a-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении iLMS.</span><span class="sxs-lookup"><span data-stu-id="96c1a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="96c1a-150">**tooconfigure Azure AD единого входа с iLMS, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96c1a-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="96c1a-151">В hello в hello портала Azure **iLMS** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="96c1a-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="96c1a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="96c1a-155">На hello **iLMS URL-адреса и домена** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="96c1a-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="96c1a-157">а.</span><span class="sxs-lookup"><span data-stu-id="96c1a-157">a.</span></span> <span data-ttu-id="96c1a-158">В hello **идентификатор** текстовое поле, вставить hello **идентификатор** значение Копировать из **поставщика услуг** раздел параметров SAML в портал администрирования iLMS.</span><span class="sxs-lookup"><span data-stu-id="96c1a-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="96c1a-159">b.</span><span class="sxs-lookup"><span data-stu-id="96c1a-159">b.</span></span> <span data-ttu-id="96c1a-160">В hello **URL-адрес ответа** текстовое поле, вставить hello **конечной точки (URL)** значение Копировать из **поставщика услуг** раздел параметров SAML в портал администрирования iLMS наличие следующих hello шаблон`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="96c1a-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="96c1a-161">Значение "123456" указано в качестве примера идентификатора.</span><span class="sxs-lookup"><span data-stu-id="96c1a-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="96c1a-162">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="96c1a-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="96c1a-164">В hello **URL-адрес входа** текстовое поле, вставить hello **конечной точки (URL)** значение Копировать из **поставщика услуг** раздел параметров SAML в портал администрирования iLMS как`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="96c1a-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="96c1a-165">tooenable JIT-компилятора подготовки iLMS приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="96c1a-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="96c1a-166">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="96c1a-167">Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** раздел на странице интеграции приложений.</span><span class="sxs-lookup"><span data-stu-id="96c1a-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="96c1a-168">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="96c1a-168">hello following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="96c1a-170">Создание **подразделение, регион** и **деления** атрибуты и добавьте имя hello этих атрибутов в iLMS.</span><span class="sxs-lookup"><span data-stu-id="96c1a-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="96c1a-171">Все указанные выше атрибуты являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="96c1a-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="96c1a-172">У вас есть tooenable **Создание учетной записи пользователя Un-recognized** в iLMS toomap этих атрибутов.</span><span class="sxs-lookup"><span data-stu-id="96c1a-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="96c1a-173">Следуйте инструкциям hello [здесь](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget представление hello атрибуты конфигурации.</span><span class="sxs-lookup"><span data-stu-id="96c1a-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="96c1a-174">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="96c1a-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="96c1a-175">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="96c1a-175">Attribute Name</span></span> | <span data-ttu-id="96c1a-176">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="96c1a-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="96c1a-177">division</span><span class="sxs-lookup"><span data-stu-id="96c1a-177">division</span></span> | <span data-ttu-id="96c1a-178">user.department</span><span class="sxs-lookup"><span data-stu-id="96c1a-178">user.department</span></span> |
    | <span data-ttu-id="96c1a-179">region</span><span class="sxs-lookup"><span data-stu-id="96c1a-179">region</span></span> | <span data-ttu-id="96c1a-180">user.state</span><span class="sxs-lookup"><span data-stu-id="96c1a-180">user.state</span></span> |
    | <span data-ttu-id="96c1a-181">department</span><span class="sxs-lookup"><span data-stu-id="96c1a-181">department</span></span> | <span data-ttu-id="96c1a-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="96c1a-182">user.jobtitle</span></span> |

    <span data-ttu-id="96c1a-183">а.</span><span class="sxs-lookup"><span data-stu-id="96c1a-183">a.</span></span> <span data-ttu-id="96c1a-184">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="96c1a-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="96c1a-187">b.</span><span class="sxs-lookup"><span data-stu-id="96c1a-187">b.</span></span> <span data-ttu-id="96c1a-188">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="96c1a-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="96c1a-189">c.</span><span class="sxs-lookup"><span data-stu-id="96c1a-189">c.</span></span> <span data-ttu-id="96c1a-190">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="96c1a-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="96c1a-191">d.</span><span class="sxs-lookup"><span data-stu-id="96c1a-191">d.</span></span> <span data-ttu-id="96c1a-192">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-192">Click **Ok**</span></span>

7. <span data-ttu-id="96c1a-193">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="96c1a-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="96c1a-195">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="96c1a-195">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="96c1a-197">В другом окне браузера, войдите в tooyour **портал администрирования iLMS** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="96c1a-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="96c1a-198">Нажмите кнопку **SSO:SAML** под **параметры** tooopen SAML параметров вкладки и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="96c1a-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="96c1a-200">а.</span><span class="sxs-lookup"><span data-stu-id="96c1a-200">a.</span></span> <span data-ttu-id="96c1a-201">Разверните hello **поставщика услуг** раздела и скопируйте hello **идентификатор** и **конечной точки (URL)** значение.</span><span class="sxs-lookup"><span data-stu-id="96c1a-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="96c1a-203">b.</span><span class="sxs-lookup"><span data-stu-id="96c1a-203">b.</span></span> <span data-ttu-id="96c1a-204">В разделе **Identity Provider** (Поставщик удостоверений) установите переключатель **Import Metadata** (Импорт метаданных).</span><span class="sxs-lookup"><span data-stu-id="96c1a-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="96c1a-205">c.</span><span class="sxs-lookup"><span data-stu-id="96c1a-205">c.</span></span> <span data-ttu-id="96c1a-206">Выберите hello **метаданные** файла, загруженного с портала Azure из **сертификат подписи SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="96c1a-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="96c1a-208">d.</span><span class="sxs-lookup"><span data-stu-id="96c1a-208">d.</span></span> <span data-ttu-id="96c1a-209">Если требуется, чтобы tooenable JIT Подготовка toocreate iLMS учетных записей для отмены-распознавать пользователей, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="96c1a-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="96c1a-210">Установите флажок **Create Un-recognized User Account** (Создать учетную запись неопознанного пользователя) для сопоставления этих атрибутов.</span><span class="sxs-lookup"><span data-stu-id="96c1a-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="96c1a-212">Сопоставление атрибутов hello в Azure AD с атрибутами hello в iLMS.</span><span class="sxs-lookup"><span data-stu-id="96c1a-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="96c1a-213">В столбце атрибутов hello укажите hello атрибуты имени или hello значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="96c1a-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="96c1a-214">д.</span><span class="sxs-lookup"><span data-stu-id="96c1a-214">e.</span></span> <span data-ttu-id="96c1a-215">Go слишком**бизнес-правила** вкладку и выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="96c1a-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="96c1a-217">Проверьте **создания Un-recognized областей, подразделения и отделы** toocreate регионы, подразделения и отделы, которые еще не существуют во время hello единым входом.</span><span class="sxs-lookup"><span data-stu-id="96c1a-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="96c1a-218">Проверьте **обновление пользовательского профиля во время входа в** toospecify ли профиль пользователя hello обновляется каждый единого входа.</span><span class="sxs-lookup"><span data-stu-id="96c1a-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="96c1a-219">Если hello **«Обновление пустые значения для не обязательные поля в профиль пользователя»** флажок, поля необязательно профиля, в которых не указаны при входе будет возникать hello iLMS профиля пользователя toocontain пустые значения для этих полей.</span><span class="sxs-lookup"><span data-stu-id="96c1a-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="96c1a-220">Проверьте **отправлять ошибки уведомления по электронной почте** и введите hello электронной почты пользователя hello, в котором требуется tooreceive hello Ошибка уведомления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="96c1a-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="96c1a-221">Нажмите кнопку **Сохранить** кнопку Параметры toosave hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-221">Click **Save** button toosave hello settings.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="96c1a-223">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="96c1a-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96c1a-224">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96c1a-225">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96c1a-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96c1a-226">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="96c1a-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="96c1a-227">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="96c1a-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="96c1a-229">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96c1a-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96c1a-230">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="96c1a-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96c1a-232">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="96c1a-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96c1a-234">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="96c1a-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96c1a-236">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="96c1a-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96c1a-238">а.</span><span class="sxs-lookup"><span data-stu-id="96c1a-238">a.</span></span> <span data-ttu-id="96c1a-239">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96c1a-240">b.</span><span class="sxs-lookup"><span data-stu-id="96c1a-240">b.</span></span> <span data-ttu-id="96c1a-241">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96c1a-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96c1a-242">c.</span><span class="sxs-lookup"><span data-stu-id="96c1a-242">c.</span></span> <span data-ttu-id="96c1a-243">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="96c1a-244">d.</span><span class="sxs-lookup"><span data-stu-id="96c1a-244">d.</span></span> <span data-ttu-id="96c1a-245">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="96c1a-246">Создание тестового пользователя iLMS</span><span class="sxs-lookup"><span data-stu-id="96c1a-246">Creating an iLMS test user</span></span>

<span data-ttu-id="96c1a-247">Приложение поддерживает только в подготовки пользователей время и после проверки подлинности пользователей автоматически создаются в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="96c1a-248">JIT-компилятора будет работать, если щелкнуть hello **Создание учетной записи пользователя Un-recognized** флажок во время параметр конфигурации SAML на портале администрирования iLMS.</span><span class="sxs-lookup"><span data-stu-id="96c1a-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="96c1a-249">Toocreate пользователя вручную, затем выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="96c1a-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="96c1a-250">Войдите на сайте компании iLMS tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="96c1a-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="96c1a-251">Нажмите кнопку **«Регистрация пользователя»** под **пользователей** вкладке tooopen **Регистрация пользователя** страницы.</span><span class="sxs-lookup"><span data-stu-id="96c1a-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![Добавление сотрудника](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="96c1a-253">На hello **«Регистрация пользователя»** выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="96c1a-255">а.</span><span class="sxs-lookup"><span data-stu-id="96c1a-255">a.</span></span> <span data-ttu-id="96c1a-256">В hello **имя** в текстовое поле имя Britta типа hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="96c1a-257">b.</span><span class="sxs-lookup"><span data-stu-id="96c1a-257">b.</span></span> <span data-ttu-id="96c1a-258">В hello **Фамилия** текстового поля, типа hello фамилии Simon.</span><span class="sxs-lookup"><span data-stu-id="96c1a-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="96c1a-259">c.</span><span class="sxs-lookup"><span data-stu-id="96c1a-259">c.</span></span> <span data-ttu-id="96c1a-260">В hello **адрес электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.</span><span class="sxs-lookup"><span data-stu-id="96c1a-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="96c1a-261">d.</span><span class="sxs-lookup"><span data-stu-id="96c1a-261">d.</span></span> <span data-ttu-id="96c1a-262">В hello **область** раскрывающийся список, выберите hello значение для области.</span><span class="sxs-lookup"><span data-stu-id="96c1a-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="96c1a-263">д.</span><span class="sxs-lookup"><span data-stu-id="96c1a-263">e.</span></span> <span data-ttu-id="96c1a-264">В hello **деления** раскрывающийся список, выберите hello значение для раздела.</span><span class="sxs-lookup"><span data-stu-id="96c1a-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="96c1a-265">f.</span><span class="sxs-lookup"><span data-stu-id="96c1a-265">f.</span></span> <span data-ttu-id="96c1a-266">В hello **отдел** раскрывающийся список, выберите hello значение для отдела.</span><span class="sxs-lookup"><span data-stu-id="96c1a-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="96c1a-267">ж.</span><span class="sxs-lookup"><span data-stu-id="96c1a-267">g.</span></span> <span data-ttu-id="96c1a-268">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96c1a-269">Можно отправить toouser почты регистрации, выбрав **Отправка почты регистрации** флажок.</span><span class="sxs-lookup"><span data-stu-id="96c1a-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96c1a-270">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="96c1a-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="96c1a-271">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooiLMS доступа.</span><span class="sxs-lookup"><span data-stu-id="96c1a-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="96c1a-273">**tooassign tooiLMS Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="96c1a-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="96c1a-274">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="96c1a-276">В списке приложений hello выберите **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-276">In hello applications list, select **iLMS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="96c1a-278">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="96c1a-280">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-280">Click **Add** button.</span></span> <span data-ttu-id="96c1a-281">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="96c1a-283">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96c1a-284">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96c1a-285">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="96c1a-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96c1a-286">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="96c1a-286">Testing single sign-on</span></span>

<span data-ttu-id="96c1a-287">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="96c1a-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96c1a-288">При нажатии кнопки iLMS плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour iLMS приложения.</span><span class="sxs-lookup"><span data-stu-id="96c1a-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96c1a-289">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="96c1a-289">Additional resources</span></span>

* [<span data-ttu-id="96c1a-290">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96c1a-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96c1a-291">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96c1a-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

