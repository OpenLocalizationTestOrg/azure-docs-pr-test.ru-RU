---
title: "Руководство по интеграции Azure Active Directory с SuccessFactors | Документация Майкрософт"
description: "Узнайте, как toouse SuccessFactors с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="6ed9d-103">Руководство. Интеграция Azure Active Directory с SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="6ed9d-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="6ed9d-104">Hello цель этого учебника — tooshow вы как toointegrate SuccessFactors с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ed9d-105">Интеграция SuccessFactors с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="6ed9d-106">Можно управлять в Azure AD, имеющего доступ tooSuccessFactors</span><span class="sxs-lookup"><span data-stu-id="6ed9d-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="6ed9d-107">Можно включить на пользователей tooautomatically get вошедшего tooSuccessFactors (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed9d-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="6ed9d-108">Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="6ed9d-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="6ed9d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ed9d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6ed9d-110">Prerequisites</span></span>
<span data-ttu-id="6ed9d-111">tooconfigure интеграция Azure AD с SuccessFactors требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="6ed9d-112">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="6ed9d-112">A valid Azure subscription</span></span>
* <span data-ttu-id="6ed9d-113">клиент в SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="6ed9d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="6ed9d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="6ed9d-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="6ed9d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ed9d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6ed9d-118">Scenario description</span></span>
<span data-ttu-id="6ed9d-119">Hello цель этого учебника — tooenable tootest Azure AD единого входа в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="6ed9d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ed9d-121">Добавление SuccessFactors из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6ed9d-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="6ed9d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed9d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="6ed9d-123">Добавление SuccessFactors из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6ed9d-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="6ed9d-124">tooconfigure hello интеграции SuccessFactors в Azure AD, вы должны tooadd SuccessFactors из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6ed9d-125">**tooadd SuccessFactors из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6ed9d-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ed9d-126">В классический портал Azure, на левой навигационной панели hello hello щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Настройка единого входа][1]
2. <span data-ttu-id="6ed9d-128">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="6ed9d-129">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Настройка единого входа][2]
4. <span data-ttu-id="6ed9d-131">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Приложения][3]
5. <span data-ttu-id="6ed9d-133">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Настройка единого входа][4]
6. <span data-ttu-id="6ed9d-135">В hello **поле поиска**, тип **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Настройка единого входа][5]
7. <span data-ttu-id="6ed9d-137">В панели результатов hello выберите **SuccessFactors**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Настройка единого входа][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ed9d-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed9d-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ed9d-140">Цель этого раздела Hello является tooshow как tooconfigure и теста Azure AD единого входа с SuccessFactors на основе тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="6ed9d-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ed9d-141">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SuccessFactors tooan пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="6ed9d-142">Другими словами связи между пользователя Azure AD и hello связанных пользователей в SuccessFactors должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="6ed9d-143">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="6ed9d-144">tooconfigure и теста Azure AD единого входа с SuccessFactors, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6ed9d-145">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6ed9d-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ed9d-147">**[Создание тестового пользователя SuccessFactors](#creating-a-successfactors-test-user)**  -toohave аналог Саймон Britta в SuccessFactors, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="6ed9d-148">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ed9d-149">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ed9d-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed9d-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="6ed9d-151">В этом разделе включения Azure AD единого входа в классическом портале hello и настройки единого входа в приложение SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="6ed9d-152">**tooconfigure Azure AD единого входа с SuccessFactors, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6ed9d-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ed9d-153">В классический портал Azure, на hello hello **SuccessFactors** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Настройка единого входа][7]
2. <span data-ttu-id="6ed9d-155">На hello **предпочитаемый как toosign пользователей на tooSuccessFactors** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Настройка единого входа][8]
3. <span data-ttu-id="6ed9d-157">На hello **настроить URL-адрес приложения** страницы, выполните следующие шаги hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Настройка единого входа][9]
   
    <span data-ttu-id="6ed9d-159">а.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-159">a.</span></span> <span data-ttu-id="6ed9d-160">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя один из следующих шаблонов hello:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="6ed9d-161">b.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-161">b.</span></span> <span data-ttu-id="6ed9d-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя один из следующих шаблонов hello:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="6ed9d-163">c.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-163">c.</span></span> <span data-ttu-id="6ed9d-164">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="6ed9d-165">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="6ed9d-166">У вас tooupdate эти значения с hello фактический на URL-адрес входа и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="6ed9d-167">обратитесь в службу tooget эти значения [группы поддержки SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="6ed9d-168">На hello **настройки единого входа в SuccessFactors** щелкните **загрузки сертификата**, а затем сохраните файл сертификата hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Настройка единого входа][10]

2. <span data-ttu-id="6ed9d-170">В другом окне веб-браузера войдите на **портал администрирования SuccessFactors** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="6ed9d-171">Посетите **безопасности приложения** и собственные слишком**единого входа в компонент**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="6ed9d-172">Установите любое значение в hello **сбросить токен** и нажмите кнопку **сохранить маркера** tooenable единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Настройка единого входа на стороне приложения][11]

    > [!NOTE] 
    > <span data-ttu-id="6ed9d-174">Это значение используется только в качестве hello выключатель.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="6ed9d-175">Если любое значение сохраняется, hello единого входа SAML — ON.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="6ed9d-176">Если пустое значение сохраняется hello единого входа SAML имеет значение OFF.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="6ed9d-177">Снимок экрана собственного toobelow и выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Настройка единого входа на стороне приложения][12]
   
    <span data-ttu-id="6ed9d-179">а.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-179">a.</span></span> <span data-ttu-id="6ed9d-180">Выберите hello **единого входа SAML v2** переключатель</span><span class="sxs-lookup"><span data-stu-id="6ed9d-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="6ed9d-181">b.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-181">b.</span></span> <span data-ttu-id="6ed9d-182">Задайте hello Name(e.g. SAml issuer + company name) стороной утверждения SAML.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="6ed9d-183">c.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-183">c.</span></span> <span data-ttu-id="6ed9d-184">В hello **издатель SAML** textbox помещение значения hello **URL-адрес издателя** из мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="6ed9d-185">d.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-185">d.</span></span> <span data-ttu-id="6ed9d-186">Выберите значение **Response(Customer Generated/IdP/AP)** (Ответ (создается клиентом/IdP/AP)) для параметра **Require Mandatory Signature** (Требуется обязательная подпись).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="6ed9d-187">д.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-187">e.</span></span> <span data-ttu-id="6ed9d-188">Выберите значение **Enabled** (Включено) для параметра **Enable SAML Flag** (Включить флаг SAML).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="6ed9d-189">Е.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-189">f.</span></span> <span data-ttu-id="6ed9d-190">Выберите значение **No** (Нет) для параметра **Login Request Signature (SF Generated/SP/RP)** (Подпись запроса на вход (создается SF/SP/RP)).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="6ed9d-191">ж.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-191">g.</span></span> <span data-ttu-id="6ed9d-192">Выберите значение **Browser/Post Profile** (Браузер/пост-профилирование) для параметра **SAML Profile** (Профиль SAML).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="6ed9d-193">h.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-193">h.</span></span> <span data-ttu-id="6ed9d-194">Выберите значение **No** (Нет) для параметра **Enforce Certificate Valid Period** (Применять период действия сертификата).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="6ed9d-195">i.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-195">i.</span></span> <span data-ttu-id="6ed9d-196">Скопируйте содержимое hello файла hello загруженного сертификата и вставьте его в hello **сертификата проверки SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ed9d-197">Hello содержимого сертификата должен иметь начинаться сертификата и закрывающий теги сертификата.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="6ed9d-198">Перейдите tooSAML V2, а затем выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Настройка единого входа на стороне приложения][13]
   
    <span data-ttu-id="6ed9d-200">а.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-200">a.</span></span> <span data-ttu-id="6ed9d-201">Выберите значение **Yes** (Да) для параметра **Support SP-initiated Global Logout** (Поддержка глобального выхода, инициированного SP).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="6ed9d-202">b.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-202">b.</span></span> <span data-ttu-id="6ed9d-203">В hello **URL-адрес (назначение LogoutRequest) глобального выхода служба** textbox помещение значения hello **URL-адрес удаленного выхода** из мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="6ed9d-204">c.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-204">c.</span></span> <span data-ttu-id="6ed9d-205">Выберите значение **No** (Нет) для параметра **Require sp must encrypt all NameID element** (Требуется шифрование всех элементов NameID на стороне SP).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="6ed9d-206">d.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-206">d.</span></span> <span data-ttu-id="6ed9d-207">Выберите значение **unspecified** (Не определено) для параметра **NameID Format** (Формат идентификатора имени).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="6ed9d-208">д.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-208">e.</span></span> <span data-ttu-id="6ed9d-209">Выберите значение **Yes** (Да) для параметра **Enable sp initiated login (AuthnRequest)** (Включить вход по требованию SP).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="6ed9d-210">f.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-210">f.</span></span> <span data-ttu-id="6ed9d-211">В hello **запрос на отправку в масштабе организации издателя** textbox помещение значения hello **URL-адрес удаленного входа** из мастера настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="6ed9d-212">Выполните следующие действия, если требуется, чтобы имена входа toomake hello без учета регистра,.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="6ed9d-213">а.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-213">a.</span></span> <span data-ttu-id="6ed9d-214">Посетите **параметры компании**(нижней hello).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="6ed9d-215">b.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-215">b.</span></span> <span data-ttu-id="6ed9d-216">Установите флажок **Enable Non-Case-Sensitive Username** (Имя пользователя без учета регистра).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="6ed9d-217">в) Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-217">c.Click **Save**.</span></span>
   
    ![Настройка единого входа][29]

    > [!NOTE] 
    > <span data-ttu-id="6ed9d-219">При попытке tooenable это, hello система проверяет, если он создаст повторяющееся имя входа SAML.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="6ed9d-220">Например, если у клиента приветствия имен пользователей User1 и пользователь user1.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="6ed9d-221">Если отменить учет регистра, эти имена будут считаться одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="6ed9d-222">Hello система выдаст сообщение об ошибке и функция hello не будет разрешена.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="6ed9d-223">Hello клиента потребуется toochange один приветствия имен пользователей, фактически написано другой.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="6ed9d-224">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Приложения][14]
2. <span data-ttu-id="6ed9d-226">На hello **единого входа для подтверждения** щелкните **завершить**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Приложения][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ed9d-228">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed9d-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ed9d-229">Hello цель этого раздела — toocreate тестового пользователя вызывается Саймон Britta классическом портале hello.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][16]

<span data-ttu-id="6ed9d-231">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6ed9d-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ed9d-232">В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD][17]
2. <span data-ttu-id="6ed9d-234">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="6ed9d-235">Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD][18]
4. <span data-ttu-id="6ed9d-237">tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Создание тестового пользователя Azure AD][19]
5. <span data-ttu-id="6ed9d-239">На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][20]
   
    <span data-ttu-id="6ed9d-241">а.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-241">a.</span></span> <span data-ttu-id="6ed9d-242">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="6ed9d-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="6ed9d-243">b.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-243">b.</span></span> <span data-ttu-id="6ed9d-244">В имени пользователя hello **textbox**, тип **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="6ed9d-245">c.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-245">c.</span></span> <span data-ttu-id="6ed9d-246">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-246">Click **Next**.</span></span>
6. <span data-ttu-id="6ed9d-247">На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][21]
   
    <span data-ttu-id="6ed9d-249">а.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-249">a.</span></span> <span data-ttu-id="6ed9d-250">В hello **имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="6ed9d-251">b.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-251">b.</span></span> <span data-ttu-id="6ed9d-252">В hello **Фамилия** текстовое поле, тип, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="6ed9d-253">c.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-253">c.</span></span> <span data-ttu-id="6ed9d-254">В hello **отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="6ed9d-255">d.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-255">d.</span></span> <span data-ttu-id="6ed9d-256">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="6ed9d-257">д.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-257">e.</span></span> <span data-ttu-id="6ed9d-258">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-258">Click **Next**.</span></span>
7. <span data-ttu-id="6ed9d-259">На hello **получение временного пароля** странице диалогового окна щелкните **создания**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD][22]
8. <span data-ttu-id="6ed9d-261">На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6ed9d-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][23]
   
    <span data-ttu-id="6ed9d-263">а.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-263">a.</span></span> <span data-ttu-id="6ed9d-264">Запишите значение hello hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="6ed9d-265">b.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-265">b.</span></span> <span data-ttu-id="6ed9d-266">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="6ed9d-267">Создание тестового пользователя SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="6ed9d-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="6ed9d-268">В порядке tooenable toolog пользователей Azure AD в SuccessFactors их необходимо подготовить в SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="6ed9d-269">В случае hello объекта SuccessFactors Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="6ed9d-270">tooget создать пользователей в SuccessFactors, требуется toocontact hello [группы поддержки SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="6ed9d-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6ed9d-271">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="6ed9d-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="6ed9d-272">Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа путем предоставления ее tooSuccessFactors доступа.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Назначение пользователя][24]

<span data-ttu-id="6ed9d-274">**tooassign tooSuccessFactors Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6ed9d-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ed9d-275">Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Назначение пользователя][25]
2. <span data-ttu-id="6ed9d-277">В списке приложений hello выберите **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Настройка единого входа][26]
3. <span data-ttu-id="6ed9d-279">В меню в верхней части hello hello выберите **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Назначение пользователя][27]
4. <span data-ttu-id="6ed9d-281">В списке пользователей hello выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="6ed9d-282">В нижней hello hello инструментов, нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="6ed9d-284">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6ed9d-284">Testing single sign-on</span></span>
<span data-ttu-id="6ed9d-285">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="6ed9d-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6ed9d-286">При нажатии кнопки SuccessFactors плитки в панели доступа hello приветствия, вы должны получить tooyour автоматически подписан в приложение SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="6ed9d-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ed9d-287">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6ed9d-287">Additional resources</span></span>
* [<span data-ttu-id="6ed9d-288">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ed9d-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ed9d-289">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6ed9d-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
