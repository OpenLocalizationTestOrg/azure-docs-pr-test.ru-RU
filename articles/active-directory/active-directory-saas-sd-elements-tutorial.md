---
title: "Руководство по интеграции Azure Active Directory с SD Elements | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SD элементы."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="919c2-103">Учебник. Интеграция Azure Active Directory с SD Elements</span><span class="sxs-lookup"><span data-stu-id="919c2-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="919c2-104">В этом учебнике вы узнаете, как toointegrate SD элементы с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="919c2-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="919c2-105">Интеграция SD элементы с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="919c2-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="919c2-106">Можно управлять в Azure AD, имеющего доступ tooSD элементов</span><span class="sxs-lookup"><span data-stu-id="919c2-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="919c2-107">Можно включить на пользователей tooautomatically get вошедшего tooSD элементы (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="919c2-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="919c2-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="919c2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="919c2-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="919c2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="919c2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="919c2-110">Prerequisites</span></span>

<span data-ttu-id="919c2-111">tooconfigure интеграция Azure AD с элементами SD необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="919c2-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="919c2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="919c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="919c2-113">подписка SD Elements с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="919c2-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="919c2-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="919c2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="919c2-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="919c2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="919c2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="919c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="919c2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="919c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="919c2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="919c2-118">Scenario description</span></span>
<span data-ttu-id="919c2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="919c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="919c2-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="919c2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="919c2-121">Добавление SD элементы из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="919c2-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="919c2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="919c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="919c2-123">Добавление SD элементы из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="919c2-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="919c2-124">tooconfigure hello интеграция SD элементов в Azure AD, вы должны tooadd SD элементы из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="919c2-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="919c2-125">**tooadd SD элементы из коллекции hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="919c2-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="919c2-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="919c2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="919c2-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="919c2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="919c2-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="919c2-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="919c2-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="919c2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="919c2-133">Введите в поле поиска hello **SD элементы**.</span><span class="sxs-lookup"><span data-stu-id="919c2-133">In hello search box, type **SD Elements**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="919c2-135">В панели результатов hello выберите **SD элементы**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="919c2-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="919c2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="919c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="919c2-138">В этом разделе описана настройка и проверка единого входа Azure AD в SD Elements с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="919c2-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="919c2-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в элементах SD является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919c2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="919c2-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в элементах SD должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="919c2-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="919c2-141">В элементах SD присвоить значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="919c2-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="919c2-142">tooconfigure и тестирования Azure AD единого входа с элементами SD, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="919c2-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="919c2-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="919c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="919c2-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="919c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="919c2-145">**[Создание тестового пользователя SD элементы](#creating-a-sd-elements-test-user)**  -toohave аналог Саймон Britta в элементах SD, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="919c2-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="919c2-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="919c2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="919c2-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="919c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="919c2-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="919c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="919c2-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SD элементов.</span><span class="sxs-lookup"><span data-stu-id="919c2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="919c2-150">**tooconfigure Azure AD единого входа с элементами SD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="919c2-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="919c2-151">В hello в hello портала Azure **SD элементы** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="919c2-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="919c2-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="919c2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="919c2-155">На hello **URL-адреса и домена элементы SD** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="919c2-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="919c2-157">а.</span><span class="sxs-lookup"><span data-stu-id="919c2-157">a.</span></span> <span data-ttu-id="919c2-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="919c2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="919c2-159">b.</span><span class="sxs-lookup"><span data-stu-id="919c2-159">b.</span></span> <span data-ttu-id="919c2-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="919c2-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="919c2-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="919c2-161">These values are not real.</span></span> <span data-ttu-id="919c2-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="919c2-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="919c2-163">Обратитесь к [SD элементы поддерживают команды](mailto:support@sdelements.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="919c2-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="919c2-164">Элементы SD приложение ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="919c2-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="919c2-165">Настройка следующих утверждений для этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="919c2-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="919c2-166">Вы можете управлять hello значения этих атрибутов из hello **«Пользователя атрибут»** вкладку приложения hello.</span><span class="sxs-lookup"><span data-stu-id="919c2-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="919c2-167">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="919c2-167">hello following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="919c2-169">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="919c2-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="919c2-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="919c2-170">Attribute Name</span></span> | <span data-ttu-id="919c2-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="919c2-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="919c2-172">email</span><span class="sxs-lookup"><span data-stu-id="919c2-172">email</span></span> |<span data-ttu-id="919c2-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="919c2-173">user.mail</span></span> |
    | <span data-ttu-id="919c2-174">firstname</span><span class="sxs-lookup"><span data-stu-id="919c2-174">firstname</span></span> |<span data-ttu-id="919c2-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="919c2-175">user.givenname</span></span> |
    | <span data-ttu-id="919c2-176">lastname</span><span class="sxs-lookup"><span data-stu-id="919c2-176">lastname</span></span> |<span data-ttu-id="919c2-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="919c2-177">user.surname</span></span> |

    <span data-ttu-id="919c2-178">а.</span><span class="sxs-lookup"><span data-stu-id="919c2-178">a.</span></span> <span data-ttu-id="919c2-179">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="919c2-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="919c2-182">b.</span><span class="sxs-lookup"><span data-stu-id="919c2-182">b.</span></span> <span data-ttu-id="919c2-183">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="919c2-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="919c2-184">c.</span><span class="sxs-lookup"><span data-stu-id="919c2-184">c.</span></span> <span data-ttu-id="919c2-185">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="919c2-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="919c2-186">d.</span><span class="sxs-lookup"><span data-stu-id="919c2-186">d.</span></span> <span data-ttu-id="919c2-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="919c2-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="919c2-188">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="919c2-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="919c2-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="919c2-190">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="919c2-192">На hello **SD элементы конфигурации** щелкните **настроить элементы SD** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="919c2-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="919c2-193">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="919c2-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="919c2-195">tooget единый вход включен, обратитесь к вашей [SD элементы поддержки](mailto:support@sdelements.com) и предоставить им файл hello загруженного сертификата.</span><span class="sxs-lookup"><span data-stu-id="919c2-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="919c2-196">В другом окне браузера клиента SD элементы tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="919c2-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="919c2-197">В меню в верхней части hello hello выберите **системы**, а затем **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="919c2-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="919c2-199">На hello **параметры единого входа** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="919c2-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="919c2-201">а.</span><span class="sxs-lookup"><span data-stu-id="919c2-201">a.</span></span> <span data-ttu-id="919c2-202">Для параметра **SSO Type** (Тип SSO) выберите значение **SAML**.</span><span class="sxs-lookup"><span data-stu-id="919c2-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="919c2-203">b.</span><span class="sxs-lookup"><span data-stu-id="919c2-203">b.</span></span> <span data-ttu-id="919c2-204">В hello **идентификатор сущности поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="919c2-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="919c2-205">c.</span><span class="sxs-lookup"><span data-stu-id="919c2-205">c.</span></span> <span data-ttu-id="919c2-206">В hello **поставщика единого входа службы удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="919c2-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="919c2-207">d.</span><span class="sxs-lookup"><span data-stu-id="919c2-207">d.</span></span> <span data-ttu-id="919c2-208">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="919c2-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="919c2-209">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="919c2-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="919c2-210">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="919c2-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="919c2-211">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="919c2-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="919c2-212">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="919c2-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="919c2-213">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="919c2-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="919c2-215">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="919c2-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="919c2-216">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="919c2-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="919c2-218">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="919c2-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="919c2-220">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="919c2-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="919c2-222">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="919c2-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="919c2-224">а.</span><span class="sxs-lookup"><span data-stu-id="919c2-224">a.</span></span> <span data-ttu-id="919c2-225">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="919c2-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="919c2-226">b.</span><span class="sxs-lookup"><span data-stu-id="919c2-226">b.</span></span> <span data-ttu-id="919c2-227">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="919c2-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="919c2-228">c.</span><span class="sxs-lookup"><span data-stu-id="919c2-228">c.</span></span> <span data-ttu-id="919c2-229">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="919c2-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="919c2-230">d.</span><span class="sxs-lookup"><span data-stu-id="919c2-230">d.</span></span> <span data-ttu-id="919c2-231">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="919c2-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="919c2-232">Создание тестового пользователя SD Elements</span><span class="sxs-lookup"><span data-stu-id="919c2-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="919c2-233">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon SD элементов.</span><span class="sxs-lookup"><span data-stu-id="919c2-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="919c2-234">В случае hello элементов SD создание элементов SD пользователей осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="919c2-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="919c2-235">**toocreate Britta Simon SD элементов, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="919c2-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="919c2-236">В окне браузера, сайт компании SD элементы tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="919c2-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="919c2-237">В меню в верхней части hello hello выберите **Управление пользователями**, а затем **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="919c2-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![Создание тестового пользователя SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="919c2-239">Нажмите кнопку **Add New User**(Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="919c2-239">Click **Add New User**.</span></span>
   
    ![Создание тестового пользователя SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="919c2-241">На hello **добавить пользователя** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="919c2-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="919c2-243">а.</span><span class="sxs-lookup"><span data-stu-id="919c2-243">a.</span></span> <span data-ttu-id="919c2-244">В hello **электронной почты** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="919c2-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="919c2-245">b.</span><span class="sxs-lookup"><span data-stu-id="919c2-245">b.</span></span> <span data-ttu-id="919c2-246">В hello **имя** текстовом поле введите имя пользователя, такие как hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="919c2-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="919c2-247">c.</span><span class="sxs-lookup"><span data-stu-id="919c2-247">c.</span></span> <span data-ttu-id="919c2-248">В hello **Фамилия** текстовом поле введите фамилию пользователя как hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="919c2-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="919c2-249">d.</span><span class="sxs-lookup"><span data-stu-id="919c2-249">d.</span></span> <span data-ttu-id="919c2-250">Для параметра **Role** (Роль) выберите значение **User** (Пользователь).</span><span class="sxs-lookup"><span data-stu-id="919c2-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="919c2-251">д.</span><span class="sxs-lookup"><span data-stu-id="919c2-251">e.</span></span> <span data-ttu-id="919c2-252">Нажмите кнопку **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="919c2-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="919c2-253">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="919c2-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="919c2-254">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSD элементов.</span><span class="sxs-lookup"><span data-stu-id="919c2-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="919c2-256">**tooassign Britta Simon tooSD элементов, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="919c2-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="919c2-257">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="919c2-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="919c2-259">В списке приложений hello выберите **SD элементы**.</span><span class="sxs-lookup"><span data-stu-id="919c2-259">In hello applications list, select **SD Elements**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="919c2-261">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="919c2-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="919c2-263">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="919c2-263">Click **Add** button.</span></span> <span data-ttu-id="919c2-264">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="919c2-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="919c2-266">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="919c2-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="919c2-267">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="919c2-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="919c2-268">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="919c2-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="919c2-269">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="919c2-269">Testing single sign-on</span></span>

<span data-ttu-id="919c2-270">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="919c2-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="919c2-271">При нажатии кнопки приветствия SD элементы мозаики в hello панели доступа, следует получать автоматически вошедшего tooyour SD элементов приложения.</span><span class="sxs-lookup"><span data-stu-id="919c2-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="919c2-272">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="919c2-272">Additional resources</span></span>

* [<span data-ttu-id="919c2-273">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="919c2-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="919c2-274">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="919c2-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

