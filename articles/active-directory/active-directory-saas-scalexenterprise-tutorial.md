---
title: "Руководство по интеграции Azure Active Directory с ScaleX Enterprise | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="4d916-103">Руководство по интеграции Azure Active Directory с ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="4d916-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="4d916-104">В этом учебнике вы узнаете, как toointegrate ScaleX предприятия в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d916-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d916-105">Интеграция ScaleX предприятия с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4d916-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4d916-106">Можно управлять в Azure AD, имеющего доступ tooScaleX предприятия</span><span class="sxs-lookup"><span data-stu-id="4d916-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="4d916-107">Можно включить на пользователей tooautomatically get вошедшего tooScaleX предприятия (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d916-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d916-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4d916-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4d916-109">Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d916-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="4d916-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="4d916-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d916-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4d916-111">Prerequisites</span></span>

<span data-ttu-id="4d916-112">tooconfigure интеграция Azure AD с ScaleX Enterprise требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4d916-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="4d916-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4d916-113">An Azure AD subscription</span></span>
- <span data-ttu-id="4d916-114">подписка ScaleX Enterprise с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4d916-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d916-115">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4d916-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d916-116">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="4d916-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d916-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4d916-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4d916-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d916-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d916-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4d916-119">Scenario description</span></span>
<span data-ttu-id="4d916-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4d916-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d916-121">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="4d916-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d916-122">Добавление ScaleX Enterprise из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="4d916-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="4d916-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d916-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="4d916-124">Добавление ScaleX Enterprise из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="4d916-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="4d916-125">tooconfigure hello интеграции ScaleX Enterprise в tooAzure AD, вы должны tooadd ScaleX Enterprise из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4d916-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4d916-126">**tooadd ScaleX Enterprise из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="4d916-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d916-127">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4d916-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d916-129">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="4d916-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4d916-130">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4d916-130">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4d916-132">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="4d916-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4d916-134">Введите в поле поиска hello **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="4d916-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="4d916-136">В панели результатов hello, выберите **ScaleX Enterprise**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4d916-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d916-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d916-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d916-139">В этом разделе описана настройка и проверка единого входа Azure AD в ScaleX Enterprise с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d916-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4d916-140">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello ScaleX предприятии является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d916-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="4d916-141">Другими словами связи между пользователя Azure AD и связанных пользователей hello ScaleX предприятия должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="4d916-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="4d916-142">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** ScaleX предприятия.</span><span class="sxs-lookup"><span data-stu-id="4d916-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="4d916-143">tooconfigure и теста Azure AD единого входа с ScaleX Enterprise, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4d916-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4d916-144">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="4d916-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4d916-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="4d916-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d916-146">**[Создание тестового пользователя ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave аналог Саймон Britta ScaleX предприятии, которая является представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="4d916-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d916-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="4d916-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d916-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4d916-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d916-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d916-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d916-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ScaleX предприятия.</span><span class="sxs-lookup"><span data-stu-id="4d916-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="4d916-151">**tooconfigure Azure AD единого входа с помощью ScaleX Enterprise выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d916-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d916-152">В hello в hello портала Azure **ScaleX Enterprise** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4d916-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4d916-154">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="4d916-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="4d916-156">На hello **ScaleX домена предприятия и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="4d916-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="4d916-158">а.</span><span class="sxs-lookup"><span data-stu-id="4d916-158">a.</span></span> <span data-ttu-id="4d916-159">В hello **идентификатор** текстовое значение hello типа, используя следующий шаблон hello:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="4d916-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="4d916-160">b.</span><span class="sxs-lookup"><span data-stu-id="4d916-160">b.</span></span> <span data-ttu-id="4d916-161">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="4d916-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="4d916-162">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="4d916-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="4d916-164">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="4d916-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="4d916-165">Они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="4d916-165">These are not hello real values.</span></span> <span data-ttu-id="4d916-166">Обновите эти значения с hello фактический идентификатор, URL-адрес ответа или URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="4d916-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="4d916-167">Обратитесь к [группа поддержки ScaleX корпоративный клиент](http://info.rescale.com/contact_sales) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="4d916-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="4d916-168">Приложение ScaleX ожидает утверждения SAML hello в определенном формате, требующий вы toomodify настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="4d916-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="4d916-169">Нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** флажок tooopen hello пользовательские атрибуты параметров.</span><span class="sxs-lookup"><span data-stu-id="4d916-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="4d916-171">а.</span><span class="sxs-lookup"><span data-stu-id="4d916-171">a.</span></span> <span data-ttu-id="4d916-172">Щелкните правой кнопкой мыши атрибут hello **имя** и нажмите кнопку Удалить.</span><span class="sxs-lookup"><span data-stu-id="4d916-172">Right click hello attribute **name** and click delete.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="4d916-174">b.</span><span class="sxs-lookup"><span data-stu-id="4d916-174">b.</span></span> <span data-ttu-id="4d916-175">Нажмите кнопку **emailaddress** атрибута tooopen hello изменение атрибута окна.</span><span class="sxs-lookup"><span data-stu-id="4d916-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="4d916-176">Измените его значение с **user.mail** слишком**user.userprincipalname** и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="4d916-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="4d916-178">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4d916-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="4d916-180">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4d916-180">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="4d916-182">На hello **конфигурация предприятия ScaleX** щелкните **настроить корпоративный ScaleX** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="4d916-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4d916-183">Копировать hello **идентификатор сущности SAML** и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="4d916-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="4d916-185">tooconfigure единого входа на **ScaleX Enterprise** стороны, toohello веб-сайт корпоративного ScaleX компании от имени администратора имени входа.</span><span class="sxs-lookup"><span data-stu-id="4d916-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="4d916-186">Щелкните меню hello в верхнем hello справа и выберите **администрирования Contoso**.</span><span class="sxs-lookup"><span data-stu-id="4d916-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d916-187">Contoso является лишь примером.</span><span class="sxs-lookup"><span data-stu-id="4d916-187">Contoso is just an example.</span></span> <span data-ttu-id="4d916-188">Используйте фактическое название компании.</span><span class="sxs-lookup"><span data-stu-id="4d916-188">This should be your actual Company Name.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="4d916-190">Выберите **интеграции** из hello верхнем меню и выберите **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4d916-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="4d916-192">Заполните форму hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="4d916-192">Complete hello form as follows:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="4d916-194">а.</span><span class="sxs-lookup"><span data-stu-id="4d916-194">a.</span></span> <span data-ttu-id="4d916-195">Выберите **Create any user who can authenticate with SSO** (Создание любого пользователя, который может выполнить проверку подлинности с помощью единого входа).</span><span class="sxs-lookup"><span data-stu-id="4d916-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="4d916-196">b.</span><span class="sxs-lookup"><span data-stu-id="4d916-196">b.</span></span> <span data-ttu-id="4d916-197">**Поставщик услуг saml**: вставьте значение hello ***urn: oasis: имена: tc: SAML:2.0:nameid-формат: постоянное***</span><span class="sxs-lookup"><span data-stu-id="4d916-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="4d916-198">c.</span><span class="sxs-lookup"><span data-stu-id="4d916-198">c.</span></span> <span data-ttu-id="4d916-199">**Имя поля электронной почты поставщика удостоверений в ACS ответ**: вставьте значение hello`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="4d916-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="4d916-200">d.</span><span class="sxs-lookup"><span data-stu-id="4d916-200">d.</span></span> <span data-ttu-id="4d916-201">**Идентификатор сущности EntityDescriptor поставщика удостоверений:** hello вставить **идентификатор сущности SAML** значения, скопированные из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4d916-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="4d916-202">д.</span><span class="sxs-lookup"><span data-stu-id="4d916-202">e.</span></span> <span data-ttu-id="4d916-203">**Удостоверение поставщика SingleSignOnService URL-адрес:** hello вставить **SAML единого входа URL-адрес службы** из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4d916-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="4d916-204">f.</span><span class="sxs-lookup"><span data-stu-id="4d916-204">f.</span></span> <span data-ttu-id="4d916-205">**Сертификат открытого X509 поставщика удостоверений:** Привет открыть X509 сертификат будет загружен из hello Azure в Блокнот и вставьте содержимое hello в этом поле.</span><span class="sxs-lookup"><span data-stu-id="4d916-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="4d916-206">Убедитесь, что не разрывы строк в hello средней hello содержимого сертификата.</span><span class="sxs-lookup"><span data-stu-id="4d916-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="4d916-207">ж.</span><span class="sxs-lookup"><span data-stu-id="4d916-207">g.</span></span> <span data-ttu-id="4d916-208">Проверьте следующие флажки hello: **включено, шифрование NameID и AuthnRequests входа.**</span><span class="sxs-lookup"><span data-stu-id="4d916-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="4d916-209">h.</span><span class="sxs-lookup"><span data-stu-id="4d916-209">h.</span></span> <span data-ttu-id="4d916-210">Нажмите кнопку **параметры единого входа обновления** toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="4d916-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="4d916-211">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="4d916-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4d916-212">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="4d916-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4d916-213">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d916-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d916-214">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d916-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d916-215">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4d916-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4d916-217">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d916-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d916-218">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4d916-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d916-220">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="4d916-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d916-222">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4d916-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d916-224">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4d916-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d916-226">а.</span><span class="sxs-lookup"><span data-stu-id="4d916-226">a.</span></span> <span data-ttu-id="4d916-227">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d916-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d916-228">b.</span><span class="sxs-lookup"><span data-stu-id="4d916-228">b.</span></span> <span data-ttu-id="4d916-229">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4d916-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d916-230">c.</span><span class="sxs-lookup"><span data-stu-id="4d916-230">c.</span></span> <span data-ttu-id="4d916-231">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="4d916-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4d916-232">d.</span><span class="sxs-lookup"><span data-stu-id="4d916-232">d.</span></span> <span data-ttu-id="4d916-233">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4d916-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="4d916-234">Создание тестового пользователя ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="4d916-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="4d916-235">Пользователи toolog tooenable Azure AD в tooScaleX Enterprise, их необходимо подготовить в tooScaleX предприятия.</span><span class="sxs-lookup"><span data-stu-id="4d916-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="4d916-236">В случае hello ScaleX Enterprise Подготовка пользователей осуществляется автоматическое и вручную действия, не требуются.</span><span class="sxs-lookup"><span data-stu-id="4d916-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="4d916-237">На стороне ScaleX hello будет автоматически подготовлен любого пользователя, прошедшего проверку подлинности с использованием учетных данных единого входа.</span><span class="sxs-lookup"><span data-stu-id="4d916-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4d916-238">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="4d916-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4d916-239">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления Enterprise tooScaleX доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="4d916-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4d916-241">**tooassign Britta Simon tooScaleX Enterprise, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4d916-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d916-242">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4d916-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4d916-244">В списке приложений hello выберите **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="4d916-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="4d916-246">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="4d916-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4d916-248">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4d916-248">Click **Add** button.</span></span> <span data-ttu-id="4d916-249">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4d916-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4d916-251">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="4d916-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4d916-252">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4d916-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d916-253">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4d916-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="4d916-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4d916-254">Testing single sign-on</span></span>

<span data-ttu-id="4d916-255">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="4d916-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4d916-256">Щелкните hello ScaleX Enterprise плитку в hello панели доступа, вы получите автоматически вошедшего tooyour ScaleX корпоративного приложения.</span><span class="sxs-lookup"><span data-stu-id="4d916-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="4d916-257">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="4d916-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4d916-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4d916-258">Additional resources</span></span>

* [<span data-ttu-id="4d916-259">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d916-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d916-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d916-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

