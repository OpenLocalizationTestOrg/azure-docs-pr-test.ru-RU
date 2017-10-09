---
title: "Руководство по интеграции Azure Active Directory с Printix | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="8c2a9-103">Руководство. Интеграция Azure Active Directory с Printix</span><span class="sxs-lookup"><span data-stu-id="8c2a9-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="8c2a9-104">В этом учебнике вы узнаете, как toointegrate Printix с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c2a9-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c2a9-105">Интеграция с Azure AD Printix предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8c2a9-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8c2a9-106">Можно управлять в Azure AD, имеющего доступ tooPrintix</span><span class="sxs-lookup"><span data-stu-id="8c2a9-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="8c2a9-107">Можно включить на пользователей tooautomatically get вошедшего tooPrintix (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c2a9-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c2a9-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8c2a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8c2a9-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c2a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c2a9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8c2a9-110">Prerequisites</span></span>

<span data-ttu-id="8c2a9-111">tooconfigure интеграция Azure AD с Printix требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8c2a9-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="8c2a9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8c2a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c2a9-113">подписка Printix с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c2a9-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c2a9-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8c2a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c2a9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c2a9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c2a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c2a9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8c2a9-118">Scenario description</span></span>
<span data-ttu-id="8c2a9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c2a9-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8c2a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c2a9-121">Добавление Printix из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8c2a9-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="8c2a9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c2a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="8c2a9-123">Добавление Printix из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8c2a9-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="8c2a9-124">tooconfigure hello интеграции Printix в Azure AD, вы должны tooadd Printix из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8c2a9-125">**tooadd Printix из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8c2a9-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c2a9-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8c2a9-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8c2a9-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8c2a9-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8c2a9-133">Введите в поле поиска hello **Printix**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-133">In hello search box, type **Printix**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="8c2a9-135">В панели результатов hello выберите **Printix**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8c2a9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c2a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8c2a9-138">В этом разделе описана настройка и проверка единого входа Azure AD в Printix с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8c2a9-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Printix является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="8c2a9-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Printix должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="8c2a9-141">В Printix, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8c2a9-142">tooconfigure и теста Azure AD единого входа с Printix, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8c2a9-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8c2a9-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c2a9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c2a9-145">**[Создание тестового пользователя Printix](#creating-a-printix-test-user)**  -toohave аналог Саймон Britta в Printix, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8c2a9-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c2a9-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8c2a9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c2a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8c2a9-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Printix.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="8c2a9-150">**tooconfigure Azure AD единого входа с Printix, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8c2a9-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c2a9-151">В hello в hello портала Azure **Printix** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8c2a9-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="8c2a9-155">На hello **URL-адреса и домена Printix** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8c2a9-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="8c2a9-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="8c2a9-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8c2a9-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-158">hello value is not real.</span></span> <span data-ttu-id="8c2a9-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8c2a9-160">Обратитесь к [группа поддержки клиента Printix](mailto:support@printix.net) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="8c2a9-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="8c2a9-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8c2a9-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8c2a9-165">Клиент Printix tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="8c2a9-166">В меню hello hello верхней части страницы, нажмите значок hello в правом верхнем углу hello и выберите пункт «**проверки подлинности**».</span><span class="sxs-lookup"><span data-stu-id="8c2a9-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="8c2a9-168">На hello **установки** выберите **Azure и Office 365, включение проверки подлинности**</span><span class="sxs-lookup"><span data-stu-id="8c2a9-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="8c2a9-170">На hello **Azure** текстовое toohello URL-адрес метаданных федерации ввода из вкладки «**документа метаданных федерации**».</span><span class="sxs-lookup"><span data-stu-id="8c2a9-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="8c2a9-171">Присоединение hello метаданных XML-файл, который был загружен из Azure AD, слишком[Printix поддержки](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="8c2a9-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="8c2a9-172">Затем они загрузить hello XML-файла и укажите URL-адрес метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="8c2a9-174">Нажмите кнопку hello»**тестирования**«и нажмите кнопку»**ОК**» кнопку при успешном выполнении теста hello.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="8c2a9-175">Страница Azure active directory будет отображаться после нажатия кнопки hello **тестирования** кнопки.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="8c2a9-176">«hello проверка выполнена успешно» здесь означает после ввода учетных данных Azure тестовая учетная запись, он отобразит hello отображению сообщения «параметры прошла проверку». Нажмите кнопку hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="8c2a9-178">Щелкните hello **Сохранить** кнопку «**проверки подлинности**» страницы.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="8c2a9-179">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8c2a9-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8c2a9-180">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8c2a9-181">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c2a9-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8c2a9-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c2a9-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="8c2a9-183">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8c2a9-185">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8c2a9-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c2a9-186">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c2a9-188">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c2a9-190">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8c2a9-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c2a9-192">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8c2a9-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c2a9-194">а.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-194">a.</span></span> <span data-ttu-id="8c2a9-195">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c2a9-196">b.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-196">b.</span></span> <span data-ttu-id="8c2a9-197">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c2a9-198">c.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-198">c.</span></span> <span data-ttu-id="8c2a9-199">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8c2a9-200">d.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-200">d.</span></span> <span data-ttu-id="8c2a9-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="8c2a9-202">Создание тестового пользователя Printix</span><span class="sxs-lookup"><span data-stu-id="8c2a9-202">Creating a Printix test user</span></span>

<span data-ttu-id="8c2a9-203">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Printix.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="8c2a9-204">Приложение Printix поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8c2a9-205">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-205">There is no action item for you in this section.</span></span> <span data-ttu-id="8c2a9-206">Новый пользователь создается во время попытки tooaccess Printix, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="8c2a9-207">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Printix поддержки](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="8c2a9-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8c2a9-208">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8c2a9-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8c2a9-209">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPrintix доступа.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8c2a9-211">**tooassign tooPrintix Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8c2a9-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c2a9-212">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8c2a9-214">В списке приложений hello выберите **Printix**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-214">In hello applications list, select **Printix**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="8c2a9-216">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8c2a9-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-218">Click **Add** button.</span></span> <span data-ttu-id="8c2a9-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8c2a9-221">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8c2a9-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c2a9-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8c2a9-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8c2a9-224">Testing single sign-on</span></span>

<span data-ttu-id="8c2a9-225">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8c2a9-226">При нажатии кнопки hello Printix плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Printix приложения.</span><span class="sxs-lookup"><span data-stu-id="8c2a9-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c2a9-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8c2a9-227">Additional resources</span></span>

* [<span data-ttu-id="8c2a9-228">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c2a9-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c2a9-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8c2a9-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

