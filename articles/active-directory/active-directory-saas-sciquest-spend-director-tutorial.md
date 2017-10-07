---
title: "Руководство по интеграции Azure Active Directory с SciQuest Spend Director | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SciQuest директор расходов."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="39f96-103">Учебник. Интеграция Azure Active Directory с SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="39f96-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="39f96-104">Hello цель этого учебника — tooshow вы как toointegrate директор расходов SciQuest с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39f96-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="39f96-105">Интеграция с Azure AD директор расходов SciQuest предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="39f96-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="39f96-106">Можно управлять в Azure AD, имеющего доступ tooSciQuest директор расходов</span><span class="sxs-lookup"><span data-stu-id="39f96-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="39f96-107">Можно включить на пользователей tooautomatically get вошедшего tooSciQuest директор расходов (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="39f96-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="39f96-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="39f96-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="39f96-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39f96-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39f96-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="39f96-110">Prerequisites</span></span>
<span data-ttu-id="39f96-111">tooconfigure интеграция Azure AD с директор расходов SciQuest требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="39f96-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="39f96-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="39f96-112">An Azure AD subscription</span></span>
* <span data-ttu-id="39f96-113">подписка SciQuest Spend Director с включенным единым входом.</span><span class="sxs-lookup"><span data-stu-id="39f96-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39f96-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="39f96-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="39f96-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="39f96-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="39f96-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="39f96-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="39f96-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39f96-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="39f96-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="39f96-118">Scenario Description</span></span>
<span data-ttu-id="39f96-119">Hello цель этого учебника — tooenable tootest Azure AD единого входа в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="39f96-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="39f96-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="39f96-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39f96-121">Добавление директор расходов SciQuest из галереи hello</span><span class="sxs-lookup"><span data-stu-id="39f96-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="39f96-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39f96-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="39f96-123">Добавление директор расходов SciQuest из галереи hello</span><span class="sxs-lookup"><span data-stu-id="39f96-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="39f96-124">tooconfigure hello интеграции SciQuest директор расходов в Azure AD, вы должны tooadd SciQuest директор расходов из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="39f96-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39f96-125">**tooadd директор расходов SciQuest из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="39f96-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39f96-126">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="39f96-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="39f96-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="39f96-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="39f96-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="39f96-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Приложения][2]

4. <span data-ttu-id="39f96-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="39f96-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Приложения][3]

5. <span data-ttu-id="39f96-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="39f96-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Приложения][4]

6. <span data-ttu-id="39f96-135">Введите в поле поиска hello **sciQuest тратить директора**.</span><span class="sxs-lookup"><span data-stu-id="39f96-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![Приложения][5]

7. <span data-ttu-id="39f96-137">В области результатов hello выберите **директор расходов SciQuest**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="39f96-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Приложения][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39f96-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39f96-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39f96-140">Цель этого раздела Hello является tooshow как tooconfigure и теста Azure AD единого входа с SciQuest директор расходов на основе тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="39f96-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39f96-141">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в директор расходов SciQuest tooan пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39f96-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="39f96-142">Другими словами связи между пользователя Azure AD и связанных пользователей hello в директор расходов SciQuest должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="39f96-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="39f96-143">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в SciQuest директор расходов.</span><span class="sxs-lookup"><span data-stu-id="39f96-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="39f96-144">tooconfigure и теста Azure AD единого входа с SciQuest директор расходов, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="39f96-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39f96-145">**[Настройка Azure AD один Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="39f96-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39f96-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="39f96-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39f96-147">**[Создание тестового пользователя директор расходов SciQuest](#creating-a-halogen-software-test-user)**  -toohave аналог Саймон Britta в SciQuest тратить директора, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="39f96-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="39f96-148">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="39f96-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39f96-149">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="39f96-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="39f96-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39f96-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="39f96-151">Цель этого раздела Hello — tooenable Azure AD единого входа в hello классический портал Azure и tooconfigure единого входа в приложении SciQuest директор расходов.</span><span class="sxs-lookup"><span data-stu-id="39f96-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="39f96-152">**tooconfigure Azure AD единого входа с SciQuest директор расходов, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="39f96-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="39f96-153">В классический портал Azure, на hello hello **директор расходов SciQuest** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="39f96-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Настройка единого входа][8]

2. <span data-ttu-id="39f96-155">На hello **предпочитаемый как toosign пользователей на tooSciQuest директор расходов** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="39f96-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Единый вход в Azure AD][9]

3. <span data-ttu-id="39f96-157">На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="39f96-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Настройка параметров приложения][10]
   
     <span data-ttu-id="39f96-159">а.</span><span class="sxs-lookup"><span data-stu-id="39f96-159">a.</span></span> <span data-ttu-id="39f96-160">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используемый вашей toosign пользователей в приложении директор расходов SciQuest tooyour, используя следующий шаблон hello: *https://.* sciquest.com/.**</span><span class="sxs-lookup"><span data-stu-id="39f96-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="39f96-161">b.</span><span class="sxs-lookup"><span data-stu-id="39f96-161">b.</span></span> <span data-ttu-id="39f96-162">В hello **URL-адрес ответа** текстового поля, типа hello же значение, которое вы ввели в hello **на URL-адрес входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="39f96-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="39f96-163">c.</span><span class="sxs-lookup"><span data-stu-id="39f96-163">c.</span></span> <span data-ttu-id="39f96-164">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="39f96-164">Click **Next**.</span></span>

4. <span data-ttu-id="39f96-165">На hello **настроить единый вход в директор расходов SciQuest** нажмите кнопку **загрузить метаданные**, а затем сохраните файл метаданных hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="39f96-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![Что такое Azure AD Connect?][11]

5. <span data-ttu-id="39f96-167">Обратитесь в службу поддержки tooenable SciQuest этот метод проверки подлинности с использованием hello выше загрузки метаданных.</span><span class="sxs-lookup"><span data-stu-id="39f96-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="39f96-168">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="39f96-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![Что такое Azure AD Connect?][15]

7. <span data-ttu-id="39f96-170">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="39f96-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39f96-171">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="39f96-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="39f96-172">Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="39f96-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="39f96-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="39f96-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39f96-174">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="39f96-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Что такое Azure AD Connect?][100] 

2. <span data-ttu-id="39f96-176">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="39f96-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="39f96-177">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="39f96-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Что такое Azure AD Connect?][101] 

4. <span data-ttu-id="39f96-179">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="39f96-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Что такое Azure AD Connect?][102] 

5. <span data-ttu-id="39f96-181">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="39f96-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Что такое Azure AD Connect?][103] 
   
    <span data-ttu-id="39f96-183">а.</span><span class="sxs-lookup"><span data-stu-id="39f96-183">a.</span></span> <span data-ttu-id="39f96-184">В поле **Тип пользователя** выберите значение **Новый пользователь в вашей организации**.</span><span class="sxs-lookup"><span data-stu-id="39f96-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="39f96-185">b.</span><span class="sxs-lookup"><span data-stu-id="39f96-185">b.</span></span> <span data-ttu-id="39f96-186">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39f96-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="39f96-187">c.</span><span class="sxs-lookup"><span data-stu-id="39f96-187">c.</span></span> <span data-ttu-id="39f96-188">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="39f96-188">Click **Next**.</span></span>

6. <span data-ttu-id="39f96-189">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="39f96-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Что такое Azure AD Connect?][104] 
   
    <span data-ttu-id="39f96-191">а.</span><span class="sxs-lookup"><span data-stu-id="39f96-191">a.</span></span> <span data-ttu-id="39f96-192">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="39f96-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="39f96-193">b.</span><span class="sxs-lookup"><span data-stu-id="39f96-193">b.</span></span> <span data-ttu-id="39f96-194">В hello **Фамилия** txtbox, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="39f96-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="39f96-195">c.</span><span class="sxs-lookup"><span data-stu-id="39f96-195">c.</span></span> <span data-ttu-id="39f96-196">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="39f96-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="39f96-197">d.</span><span class="sxs-lookup"><span data-stu-id="39f96-197">d.</span></span> <span data-ttu-id="39f96-198">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="39f96-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="39f96-199">д.</span><span class="sxs-lookup"><span data-stu-id="39f96-199">e.</span></span> <span data-ttu-id="39f96-200">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="39f96-200">Click **Next**.</span></span>

7. <span data-ttu-id="39f96-201">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="39f96-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Что такое Azure AD Connect?][105]  

8. <span data-ttu-id="39f96-203">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="39f96-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Что такое Azure AD Connect?][106]   
   
    <span data-ttu-id="39f96-205">а.</span><span class="sxs-lookup"><span data-stu-id="39f96-205">a.</span></span> <span data-ttu-id="39f96-206">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="39f96-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="39f96-207">b.</span><span class="sxs-lookup"><span data-stu-id="39f96-207">b.</span></span> <span data-ttu-id="39f96-208">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="39f96-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="39f96-209">Создание тестового пользователя SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="39f96-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="39f96-210">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в SciQuest директор расходов.</span><span class="sxs-lookup"><span data-stu-id="39f96-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="39f96-211">Требуется toocontact сотрудники службы поддержки SciQuest директор расходов и предоставить им hello сведения о вашей учетной записи tooget тестирования, она создана.</span><span class="sxs-lookup"><span data-stu-id="39f96-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="39f96-212">Вы также можете использовать JIT-подготовку — функцию единого входа, поддерживаемую SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="39f96-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="39f96-213">Если функция JIT-подготовки включена, SciQuest Spend Director автоматически создает пользователей при попытке единого входа, если они еще не созданы.</span><span class="sxs-lookup"><span data-stu-id="39f96-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="39f96-214">Эта возможность устраняет необходимость hello toomanually создать аналог-пользователей.</span><span class="sxs-lookup"><span data-stu-id="39f96-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="39f96-215">Подготовка just-in-time tooget включен, необходимо toocontact вы сотрудники службы поддержки SciQuest директор расходов.</span><span class="sxs-lookup"><span data-stu-id="39f96-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="39f96-216">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="39f96-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="39f96-217">Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа, предоставляя свой доступ tooSciQuest директор расходов.</span><span class="sxs-lookup"><span data-stu-id="39f96-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![Что такое Azure AD Connect?][200]

<span data-ttu-id="39f96-219">**tooassign tooSciQuest Britta Simon директор расходов, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="39f96-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="39f96-220">Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="39f96-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Что такое Azure AD Connect?][201]

2. <span data-ttu-id="39f96-222">В списке приложений hello выберите **директор расходов SciQuest**.</span><span class="sxs-lookup"><span data-stu-id="39f96-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Что такое Azure AD Connect?][202]

3. <span data-ttu-id="39f96-224">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="39f96-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![Что такое Azure AD Connect?][203]

4. <span data-ttu-id="39f96-226">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="39f96-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Что такое Azure AD Connect?][204]

5. <span data-ttu-id="39f96-228">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="39f96-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Что такое Azure AD Connect?][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="39f96-230">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="39f96-230">Testing Single Sign-On</span></span>
<span data-ttu-id="39f96-231">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="39f96-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="39f96-232">При нажатии кнопки hello директор расходов SciQuest плитки в панели доступа hello, вы должны получить tooyour автоматически вошедшего директор расходов SciQuest приложения.</span><span class="sxs-lookup"><span data-stu-id="39f96-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39f96-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="39f96-233">Additional Resources</span></span>
* [<span data-ttu-id="39f96-234">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39f96-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39f96-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39f96-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

