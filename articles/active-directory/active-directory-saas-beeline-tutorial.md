---
title: "Руководство по интеграции Azure Active Directory с BeeLine | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="538b8-103">Руководство по интеграции Azure Active Directory с Beeline</span><span class="sxs-lookup"><span data-stu-id="538b8-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="538b8-104">В этом учебнике вы узнаете, как toointegrate BeeLine с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="538b8-104">In this tutorial, you learn how toointegrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="538b8-105">Интеграция с Azure AD BeeLine предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="538b8-105">Integrating BeeLine with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="538b8-106">Можно управлять в Azure AD, имеющего доступ tooBeeLine</span><span class="sxs-lookup"><span data-stu-id="538b8-106">You can control in Azure AD who has access tooBeeLine</span></span>
- <span data-ttu-id="538b8-107">Можно включить на пользователей tooautomatically get вошедшего tooBeeLine (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="538b8-107">You can enable your users tooautomatically get signed-on tooBeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="538b8-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="538b8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="538b8-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="538b8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="538b8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="538b8-110">Prerequisites</span></span>

<span data-ttu-id="538b8-111">tooconfigure интеграция Azure AD с BeeLine требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="538b8-111">tooconfigure Azure AD integration with BeeLine, you need hello following items:</span></span>

- <span data-ttu-id="538b8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="538b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="538b8-113">подписка BeeLine с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="538b8-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="538b8-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="538b8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="538b8-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="538b8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="538b8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="538b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="538b8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="538b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="538b8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="538b8-118">Scenario description</span></span>
<span data-ttu-id="538b8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="538b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="538b8-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="538b8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="538b8-121">Добавление BeeLine из галереи hello</span><span class="sxs-lookup"><span data-stu-id="538b8-121">Adding BeeLine from hello gallery</span></span>
2. <span data-ttu-id="538b8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="538b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-hello-gallery"></a><span data-ttu-id="538b8-123">Добавление BeeLine из галереи hello</span><span class="sxs-lookup"><span data-stu-id="538b8-123">Adding BeeLine from hello gallery</span></span>
<span data-ttu-id="538b8-124">tooconfigure hello интеграции BeeLine в Azure AD, вы должны tooadd BeeLine из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="538b8-124">tooconfigure hello integration of BeeLine into Azure AD, you need tooadd BeeLine from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="538b8-125">**tooadd BeeLine из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="538b8-125">**tooadd BeeLine from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="538b8-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="538b8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="538b8-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="538b8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="538b8-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="538b8-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="538b8-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="538b8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="538b8-133">Введите в поле поиска hello **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="538b8-133">In hello search box, type **BeeLine**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="538b8-135">В панели результатов hello выберите **BeeLine**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="538b8-135">In hello results panel, select **BeeLine**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="538b8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="538b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="538b8-138">В этом разделе описана настройка и проверка единого входа Azure AD в BeeLine с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="538b8-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="538b8-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BeeLine является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="538b8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BeeLine is tooa user in Azure AD.</span></span> <span data-ttu-id="538b8-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в BeeLine должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="538b8-140">In other words, a link relationship between an Azure AD user and hello related user in BeeLine needs toobe established.</span></span>

<span data-ttu-id="538b8-141">В BeeLine, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="538b8-141">In BeeLine, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="538b8-142">tooconfigure и теста Azure AD единого входа с BeeLine, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="538b8-142">tooconfigure and test Azure AD single sign-on with BeeLine, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="538b8-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="538b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="538b8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="538b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="538b8-145">**[Создание тестового пользователя BeeLine](#creating-a-beeline-test-user)**  -toohave аналог Саймон Britta в BeeLine, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="538b8-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - toohave a counterpart of Britta Simon in BeeLine that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="538b8-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="538b8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="538b8-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="538b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="538b8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="538b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="538b8-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении BeeLine.</span><span class="sxs-lookup"><span data-stu-id="538b8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="538b8-150">**tooconfigure Azure AD единого входа с BeeLine, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="538b8-150">**tooconfigure Azure AD single sign-on with BeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="538b8-151">В hello в hello портала Azure **BeeLine** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="538b8-151">In hello Azure portal, on hello **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="538b8-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="538b8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="538b8-155">На hello **URL-адреса и домена BeeLine** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="538b8-155">On hello **BeeLine Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="538b8-157">а.</span><span class="sxs-lookup"><span data-stu-id="538b8-157">a.</span></span> <span data-ttu-id="538b8-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="538b8-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="538b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="538b8-159">b.</span></span> <span data-ttu-id="538b8-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="538b8-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="538b8-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="538b8-161">These values are not real.</span></span> <span data-ttu-id="538b8-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="538b8-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="538b8-163">Обратитесь к [BeeLine поддержки](https://www.beeline.com/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="538b8-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) tooget these values.</span></span>
 
4. <span data-ttu-id="538b8-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="538b8-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="538b8-166">Приложение Beeline ожидает утверждения SAML hello в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="538b8-166">Your Beeline application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="538b8-167">Можно работать с [BeeLine поддержки](https://www.beeline.com/contact-us/) первый tooidentify hello идентификатор пользователя, который будет сопоставлена с приложение hello.</span><span class="sxs-lookup"><span data-stu-id="538b8-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first tooidentify hello correct user identifier which will be mapped into hello application.</span></span> <span data-ttu-id="538b8-168">Также выполните рекомендации hello из [BeeLine поддержки](https://www.beeline.com/contact-us/) о hello атрибут, который хочет toouse для данного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="538b8-168">Also please take hello guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about hello attribute which they want toouse for this mapping.</span></span> <span data-ttu-id="538b8-169">Вы можете управлять hello значение этого атрибута из hello **атрибуты пользователя** вкладку приложения hello.</span><span class="sxs-lookup"><span data-stu-id="538b8-169">You can manage hello value of this attribute from hello **User Attributes** tab of hello application.</span></span> <span data-ttu-id="538b8-170">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="538b8-170">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="538b8-171">Здесь мы сопоставленной hello **идентификатор пользователя** утверждение со hello **userprincipalname** атрибут, который предоставляет уникальный идентификатор, который будет отправлен toohello Beeline приложения в hello каждой успешной SAML Ответ.</span><span class="sxs-lookup"><span data-stu-id="538b8-171">Here we have mapped hello **User Identifier** claim with hello **userprincipalname** attribute, which provides unique user ID, which will be sent toohello Beeline application in hello every successful SAML Response.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="538b8-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="538b8-173">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="538b8-175">На hello **конфигурации BeeLine** щелкните **Настройка BeeLine** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="538b8-175">On hello **BeeLine Configuration** section, click **Configure BeeLine** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="538b8-176">Копировать hello **URL-адрес выхода** и **идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="538b8-176">Copy hello **Sign-Out URL** and **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="538b8-178">tooconfigure единого входа на **BeeLine** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **идентификатор сущности SAML**, **URL-адрес выхода**слишком[BeeLine поддержки](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="538b8-178">tooconfigure single sign-on on **BeeLine** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** too[BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="538b8-179">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="538b8-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="538b8-180">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="538b8-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="538b8-181">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="538b8-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="538b8-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="538b8-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="538b8-183">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="538b8-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="538b8-185">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="538b8-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="538b8-186">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="538b8-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="538b8-188">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="538b8-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="538b8-190">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="538b8-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="538b8-192">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="538b8-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="538b8-194">а.</span><span class="sxs-lookup"><span data-stu-id="538b8-194">a.</span></span> <span data-ttu-id="538b8-195">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="538b8-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="538b8-196">b.</span><span class="sxs-lookup"><span data-stu-id="538b8-196">b.</span></span> <span data-ttu-id="538b8-197">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="538b8-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="538b8-198">c.</span><span class="sxs-lookup"><span data-stu-id="538b8-198">c.</span></span> <span data-ttu-id="538b8-199">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="538b8-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="538b8-200">d.</span><span class="sxs-lookup"><span data-stu-id="538b8-200">d.</span></span> <span data-ttu-id="538b8-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="538b8-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="538b8-202">Создание тестового пользователя BeeLine</span><span class="sxs-lookup"><span data-stu-id="538b8-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="538b8-203">В этом разделе описано, как создать пользователя Britta Simon в приложении Beeline.</span><span class="sxs-lookup"><span data-stu-id="538b8-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="538b8-204">Beeline приложению все пользователи toobe hello, подготовить в приложении hello перед выполнением единого входа.</span><span class="sxs-lookup"><span data-stu-id="538b8-204">Beeline application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="538b8-205">Таким образом работают с hello [BeeLine поддержки](https://www.beeline.com/contact-us/) tooprovision этих пользователей в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="538b8-205">So work with hello [BeeLine support team](https://www.beeline.com/contact-us/) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="538b8-206">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="538b8-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="538b8-207">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBeeLine доступа.</span><span class="sxs-lookup"><span data-stu-id="538b8-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBeeLine.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="538b8-209">**tooassign tooBeeLine Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="538b8-209">**tooassign Britta Simon tooBeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="538b8-210">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="538b8-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="538b8-212">В списке приложений hello выберите **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="538b8-212">In hello applications list, select **BeeLine**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="538b8-214">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="538b8-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="538b8-216">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="538b8-216">Click **Add** button.</span></span> <span data-ttu-id="538b8-217">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="538b8-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="538b8-219">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="538b8-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="538b8-220">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="538b8-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="538b8-221">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="538b8-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="538b8-222">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="538b8-222">Testing single sign-on</span></span>

<span data-ttu-id="538b8-223">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="538b8-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="538b8-224">При нажатии кнопки hello Beeline плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Beeline приложения.</span><span class="sxs-lookup"><span data-stu-id="538b8-224">When you click hello Beeline tile in hello Access Panel, you should get automatically signed-on tooyour Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="538b8-225">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="538b8-225">Additional resources</span></span>

* [<span data-ttu-id="538b8-226">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="538b8-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="538b8-227">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="538b8-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

