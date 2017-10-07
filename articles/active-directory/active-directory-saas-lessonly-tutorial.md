---
title: "Руководство по интеграции Azure Active Directory с Lesson.ly | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Lesson.ly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="f1e98-103">Руководство по интеграции Azure Active Directory с Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="f1e98-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="f1e98-104">В этом учебнике вы узнаете, как toointegrate Lesson.ly с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1e98-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1e98-105">Интеграция с Azure AD Lesson.ly предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f1e98-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1e98-106">Можно управлять в Azure AD, имеющего доступ tooLesson.ly</span><span class="sxs-lookup"><span data-stu-id="f1e98-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="f1e98-107">Можно включить на пользователей tooautomatically get вошедшего tooLesson.ly (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1e98-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1e98-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f1e98-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1e98-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1e98-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1e98-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f1e98-110">Prerequisites</span></span>

<span data-ttu-id="f1e98-111">tooconfigure интеграция Azure AD с Lesson.ly требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f1e98-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="f1e98-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f1e98-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1e98-113">подписка Lesson.ly с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f1e98-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1e98-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f1e98-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1e98-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f1e98-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1e98-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f1e98-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1e98-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1e98-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1e98-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f1e98-118">Scenario description</span></span>
<span data-ttu-id="f1e98-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f1e98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1e98-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f1e98-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1e98-121">Добавление Lesson.ly из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f1e98-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="f1e98-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1e98-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="f1e98-123">Добавление Lesson.ly из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f1e98-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="f1e98-124">tooconfigure hello интеграции Lesson.ly в Azure AD, вы должны tooadd Lesson.ly из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f1e98-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1e98-125">**tooadd Lesson.ly из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1e98-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1e98-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f1e98-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1e98-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1e98-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f1e98-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f1e98-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f1e98-133">Введите в поле поиска hello **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-133">In hello search box, type **Lesson.ly**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="f1e98-135">В панели результатов hello выберите **Lesson.ly**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f1e98-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1e98-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1e98-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1e98-138">В этом разделе описана настройка и проверка единого входа Azure AD в Lesson.ly с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1e98-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1e98-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Lesson.ly является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1e98-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="f1e98-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Lesson.ly должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f1e98-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="f1e98-141">В Lesson.ly, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f1e98-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f1e98-142">tooconfigure и теста Azure AD единого входа с Lesson.ly, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f1e98-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1e98-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f1e98-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1e98-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f1e98-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1e98-145">**[Создание тестового пользователя Lesson.ly](#creating-a-lessonly-test-user)**  -toohave аналог Саймон Britta в Lesson.ly, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f1e98-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1e98-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f1e98-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1e98-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f1e98-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1e98-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1e98-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1e98-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="f1e98-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="f1e98-150">**tooconfigure Azure AD единого входа с Lesson.ly, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1e98-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1e98-151">В hello в hello портала Azure **Lesson.ly** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f1e98-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f1e98-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="f1e98-155">На hello **URL-адреса и домена Lesson.ly** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f1e98-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="f1e98-157">а.</span><span class="sxs-lookup"><span data-stu-id="f1e98-157">a.</span></span> <span data-ttu-id="f1e98-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="f1e98-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="f1e98-159">Если ссылка на универсальный имя, которое **companyname** должен toobe заменяется фактическое имя.</span><span class="sxs-lookup"><span data-stu-id="f1e98-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="f1e98-160">b.</span><span class="sxs-lookup"><span data-stu-id="f1e98-160">b.</span></span> <span data-ttu-id="f1e98-161">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="f1e98-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="f1e98-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f1e98-162">These values are not real.</span></span> <span data-ttu-id="f1e98-163">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f1e98-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f1e98-164">Обратитесь к [группа поддержки клиента Lesson.ly](mailto:dev@lessonly.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f1e98-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="f1e98-165">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f1e98-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="f1e98-167">Hello Lesson.ly приложения ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена SAML** configuration.hello следующий снимок экрана показан пример для Это.</span><span class="sxs-lookup"><span data-stu-id="f1e98-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="f1e98-169">В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна настройки атрибутов токена SAML, как показано в hello предшествующий образ и выполнить следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f1e98-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="f1e98-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="f1e98-170">Attribute Name</span></span>   | <span data-ttu-id="f1e98-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="f1e98-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="f1e98-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="f1e98-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="f1e98-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f1e98-173">user.givenname</span></span> |
    | <span data-ttu-id="f1e98-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="f1e98-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="f1e98-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="f1e98-175">user.surname</span></span> |
    | <span data-ttu-id="f1e98-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="f1e98-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="f1e98-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="f1e98-177">user.mail</span></span> |

    <span data-ttu-id="f1e98-178">а.</span><span class="sxs-lookup"><span data-stu-id="f1e98-178">a.</span></span> <span data-ttu-id="f1e98-179">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f1e98-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f1e98-182">b.</span><span class="sxs-lookup"><span data-stu-id="f1e98-182">b.</span></span> <span data-ttu-id="f1e98-183">В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f1e98-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="f1e98-184">c.</span><span class="sxs-lookup"><span data-stu-id="f1e98-184">c.</span></span> <span data-ttu-id="f1e98-185">Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="f1e98-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f1e98-186">d.</span><span class="sxs-lookup"><span data-stu-id="f1e98-186">d.</span></span> <span data-ttu-id="f1e98-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="f1e98-188">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f1e98-188">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f1e98-190">На hello **конфигурации Lesson.ly** щелкните **Настройка Lesson.ly** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="f1e98-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f1e98-191">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="f1e98-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="f1e98-193">tooconfigure единого входа на **Lesson.ly** стороны, необходимо загрузить hello toosend **Certificate(Base64)** и **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Lesson.ly поддержки](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="f1e98-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="f1e98-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f1e98-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1e98-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f1e98-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1e98-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1e98-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1e98-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1e98-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1e98-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e98-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f1e98-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1e98-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1e98-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f1e98-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1e98-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1e98-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f1e98-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1e98-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f1e98-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1e98-209">а.</span><span class="sxs-lookup"><span data-stu-id="f1e98-209">a.</span></span> <span data-ttu-id="f1e98-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1e98-211">b.</span><span class="sxs-lookup"><span data-stu-id="f1e98-211">b.</span></span> <span data-ttu-id="f1e98-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1e98-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1e98-213">c.</span><span class="sxs-lookup"><span data-stu-id="f1e98-213">c.</span></span> <span data-ttu-id="f1e98-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1e98-215">d.</span><span class="sxs-lookup"><span data-stu-id="f1e98-215">d.</span></span> <span data-ttu-id="f1e98-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="f1e98-217">Создание тестового пользователя Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="f1e98-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="f1e98-218">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="f1e98-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="f1e98-219">Приложение Lesson.ly поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f1e98-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f1e98-220">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="f1e98-220">There is no action item for you in this section.</span></span> <span data-ttu-id="f1e98-221">Если он еще не существует во время попытки tooaccess Lesson.ly создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="f1e98-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="f1e98-222">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Lesson.ly поддержки](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="f1e98-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1e98-223">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f1e98-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1e98-224">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLesson.ly доступа.</span><span class="sxs-lookup"><span data-stu-id="f1e98-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f1e98-226">**tooassign tooLesson.ly Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f1e98-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1e98-227">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f1e98-229">В списке приложений hello выберите **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="f1e98-231">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f1e98-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-233">Click **Add** button.</span></span> <span data-ttu-id="f1e98-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f1e98-236">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f1e98-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1e98-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1e98-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f1e98-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1e98-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f1e98-239">Testing single sign-on</span></span>

<span data-ttu-id="f1e98-240">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="f1e98-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1e98-241">При нажатии кнопки hello Lesson.ly плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Lesson.ly приложения.</span><span class="sxs-lookup"><span data-stu-id="f1e98-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1e98-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f1e98-242">Additional resources</span></span>

* [<span data-ttu-id="f1e98-243">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1e98-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1e98-244">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1e98-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

