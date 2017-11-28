---
title: "Руководство по интеграции Azure Active Directory с Wizergos Productivity Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Wizergos производительном программном обеспечении."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="55a3b-103">Руководство. Интеграция Azure Active Directory с Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="55a3b-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="55a3b-104">Hello цель этого учебника — tooshow вы как toointegrate Wizergos офисного программного обеспечения в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55a3b-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55a3b-105">Интеграция программного обеспечения производительности Wizergos с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="55a3b-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="55a3b-106">Можно управлять в Azure AD, имеющего доступ tooWizergos производительном программном обеспечении</span><span class="sxs-lookup"><span data-stu-id="55a3b-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="55a3b-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooWizergos производительности программного обеспечения единого входа (SSO)</span><span class="sxs-lookup"><span data-stu-id="55a3b-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="55a3b-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="55a3b-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="55a3b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55a3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55a3b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="55a3b-110">Prerequisites</span></span>
<span data-ttu-id="55a3b-111">tooconfigure интеграция Azure AD с программным обеспечением для повышения производительности Wizergos требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="55a3b-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="55a3b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="55a3b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="55a3b-113">подписка на Wizergos Productivity Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="55a3b-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="55a3b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="55a3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="55a3b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="55a3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="55a3b-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="55a3b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="55a3b-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55a3b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55a3b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="55a3b-118">Scenario description</span></span>
<span data-ttu-id="55a3b-119">Hello цель этого учебника — tooenable вы tootest единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="55a3b-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="55a3b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="55a3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55a3b-121">Добавление программного обеспечения производительности Wizergos из галереи hello</span><span class="sxs-lookup"><span data-stu-id="55a3b-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="55a3b-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55a3b-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="55a3b-123">Добавление программного обеспечения производительности Wizergos из галереи hello</span><span class="sxs-lookup"><span data-stu-id="55a3b-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="55a3b-124">tooconfigure hello интеграция Wizergos производительности программного обеспечения в Azure AD, вы должны tooadd Wizergos производительном программном обеспечении из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="55a3b-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="55a3b-125">**tooadd Wizergos производительном программном обеспечении из библиотеки hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="55a3b-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="55a3b-126">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="55a3b-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="55a3b-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="55a3b-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="55a3b-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Приложения][2]
4. <span data-ttu-id="55a3b-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="55a3b-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Приложения][3]
5. <span data-ttu-id="55a3b-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Приложения][4]
6. <span data-ttu-id="55a3b-135">Введите в поле поиска hello **Wizergos производительном программном обеспечении**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="55a3b-137">В панели результатов hello выберите **Wizergos производительном программном обеспечении**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="55a3b-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![При выборе приложение hello в галерее hello](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="55a3b-139">Настройка и проверка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="55a3b-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="55a3b-140">Цель этого раздела Hello является tooshow как tooconfigure и тестирования единого входа Azure AD, с программным обеспечением Wizergos производительности на основе тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="55a3b-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55a3b-141">Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в Wizergos производительном программном обеспечении tooan пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55a3b-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="55a3b-142">Другими словами связи между пользователя Azure AD и связанных пользователей hello в программном обеспечении производительности Wizergos должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="55a3b-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="55a3b-143">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Wizergos производительном программном обеспечении.</span><span class="sxs-lookup"><span data-stu-id="55a3b-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="55a3b-144">tooconfigure и теста Azure AD единого входа с Softwareder BynWizergos производительность, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="55a3b-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="55a3b-145">**[Настройка Azure AD единого входа](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="55a3b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="55a3b-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="55a3b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55a3b-147">**[Создание тестового пользователя производительном программном обеспечении Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave аналог Саймон Britta в Wizergos производительном программном обеспечении, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="55a3b-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="55a3b-148">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="55a3b-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55a3b-149">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="55a3b-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="55a3b-150">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="55a3b-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="55a3b-151">В этом разделе включения Azure AD единого входа в классическом портале hello и настройки единого входа в приложении Wizergos производительном программном обеспечении.</span><span class="sxs-lookup"><span data-stu-id="55a3b-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="55a3b-152">**tooconfigure Azure AD единого входа с Wizergos производительном программном обеспечении, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="55a3b-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="55a3b-153">Классическом портале hello на hello **Wizergos производительном программном обеспечении** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="55a3b-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][6] 
2. <span data-ttu-id="55a3b-155">На hello **предпочитаемый как toosign пользователей на tooWizergos производительном программном обеспечении** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**:</span><span class="sxs-lookup"><span data-stu-id="55a3b-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="55a3b-157">На hello **Настройка параметров приложения** странице диалогового окна щелкните **Далее**:</span><span class="sxs-lookup"><span data-stu-id="55a3b-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="55a3b-159">На hello **настроить единый вход в Wizergos производительном программном обеспечении** щелкните **загрузки сертификата**, а затем сохраните файл hello на компьютере:</span><span class="sxs-lookup"><span data-stu-id="55a3b-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="55a3b-161">В другом окне браузера, клиент производительном программном обеспечении Wizergos tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="55a3b-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="55a3b-162">Меню "гамбургер" hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="55a3b-164">На странице администрирования в меню слева выберите **Проверка подлинности** и нажмите кнопку **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="55a3b-166">Выполнить hello, выполните действия **проверки ПОДЛИННОСТИ** раздела.</span><span class="sxs-lookup"><span data-stu-id="55a3b-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="55a3b-168">Нажмите кнопку **отправить** hello tooupload кнопку Загрузить сертификат из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55a3b-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="55a3b-169">В hello **URL-адрес издателя** textbox помещение значения hello **URL-адрес издателя** из мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55a3b-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="55a3b-170">В hello **-URL** textbox помещение значения hello **входа адрес службы единого** из мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55a3b-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="55a3b-171">В hello **URL-адрес единого выхода** textbox помещение значения hello **URL-адрес службы единого выхода** из мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55a3b-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="55a3b-172">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="55a3b-172">Click **Save** button.</span></span>
9. <span data-ttu-id="55a3b-173">Hello классического портала выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Единый вход в Azure AD][10]
10. <span data-ttu-id="55a3b-175">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Единый вход в Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="55a3b-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="55a3b-177">Create an Azure AD test user</span></span>
<span data-ttu-id="55a3b-178">Hello цель этого раздела — toocreate тестового пользователя вызывается Саймон Britta классическом портале hello.</span><span class="sxs-lookup"><span data-stu-id="55a3b-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][20]

<span data-ttu-id="55a3b-180">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="55a3b-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="55a3b-181">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="55a3b-183">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="55a3b-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="55a3b-184">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="55a3b-186">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="55a3b-188">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="55a3b-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="55a3b-190">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="55a3b-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="55a3b-191">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="55a3b-192">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-192">Click **Next**.</span></span>
6. <span data-ttu-id="55a3b-193">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="55a3b-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="55a3b-195">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="55a3b-196">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="55a3b-197">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="55a3b-198">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="55a3b-199">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-199">Click **Next**.</span></span>
7. <span data-ttu-id="55a3b-200">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="55a3b-202">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="55a3b-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="55a3b-204">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="55a3b-205">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="55a3b-206">Создание тестового пользователя Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="55a3b-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="55a3b-207">В этом разделе описано, как создать пользователя Britta Simon в приложении Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="55a3b-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="55a3b-208">Следует работать с группой поддержки Wizergos производительном программном обеспечении через [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd hello пользователей на платформе Wizergos офисные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="55a3b-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="55a3b-209">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="55a3b-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="55a3b-210">Hello цель этого раздела — tooenabling toouse Britta Simon единого входа в Azure, предоставляя свой доступ tooWizergos производительности программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="55a3b-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![Назначение пользователя][200]

<span data-ttu-id="55a3b-212">**tooassign tooWizergos Britta Simon производительном программном обеспечении выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="55a3b-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="55a3b-213">Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="55a3b-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Назначение пользователя][201]
2. <span data-ttu-id="55a3b-215">В списке приложений hello выберите **Wizergos производительном программном обеспечении**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="55a3b-217">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![Назначение пользователя][203]
4. <span data-ttu-id="55a3b-219">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="55a3b-220">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="55a3b-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="55a3b-222">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="55a3b-222">Test single sign-on</span></span>
<span data-ttu-id="55a3b-223">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="55a3b-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="55a3b-224">Если щелкнуть плитку Wizergos офисные приложения hello в hello панели доступа, следует получать автоматически вошедшего tooyour Wizergos производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="55a3b-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55a3b-225">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="55a3b-225">Additional resources</span></span>
* [<span data-ttu-id="55a3b-226">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55a3b-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55a3b-227">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55a3b-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
